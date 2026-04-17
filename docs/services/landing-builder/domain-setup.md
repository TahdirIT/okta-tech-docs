# Domain Setup

A tenant can publish its landing page under two kinds of hostname:

1. **Auto-subdomain** — `{tenant-slug}.{platform-base-domain}`
   (e.g. `al-ryan.okta.sa`). Created automatically the first time the tenant
   opens `/settings/domains`. Never needs DNS verification because the
   platform already controls the parent zone.
2. **Custom domain** — any hostname the tenant owns (e.g. `landing.ryan.com`).
   Must be DNS-verified before it becomes live.

## 1. Configure the platform base domain

One-time, system-wide. Under platform settings, set:

```
landing.base_domain = okta.sa
```

Or via tinker:

```php
App\Models\PlatformSetting::setValue('landing.base_domain', 'okta.sa');
```

The `DomainTenantResolver` reads this at runtime with a short cache. After
the change, clear the cache:

```bash
php artisan cache:clear
```

## 2. DNS for the platform base domain

Point a wildcard `A`/`AAAA` record at the Caddy host that fronts okta-web:

```
*.okta.sa.    IN A  203.0.113.10
```

All `{slug}.okta.sa` hosts now resolve to the same server.

## 3. Add a custom domain

A tenant admin with `landing.manage_domains` does:

1. Settings → Domains → **Add custom domain**
2. Enter hostname (e.g. `landing.ryan.com`)
3. Back-office shows a DNS record to publish:

   ```
   _okta-verify.landing.ryan.com.  IN TXT  "abc123...def"
   ```

4. After publishing the TXT, click **Verify**. The server runs
   `dns_get_record()` against the FQDN and marks the domain verified if the
   token matches.
5. Point the actual traffic:

   ```
   landing.ryan.com.  IN CNAME  okta.sa.
   ```

   (Or an `A` record to Caddy's IP — CNAME is recommended.)

## 4. Caddy (on-demand TLS)

Caddy is the default edge. Caddyfile:

```caddy
{
    on_demand_tls {
        ask https://okta.sa/_caddy/ask
    }
}

*.okta.sa, https:// {
    tls {
        on_demand
    }
    reverse_proxy 127.0.0.1:8080
}
```

Caddy calls `GET /_caddy/ask?domain=<host>` before attempting to obtain a
certificate. Our controller responds `200` only when the hostname maps to a
verified domain or an existing tenant slug — so Caddy won't attempt issuance
for arbitrary traffic.

## 5. SSL status in the admin

The `ssl_status` column on `tenant_domains` is updated by
`CaddyAskController` when Caddy asks for issuance. The Domains Manager UI
shows three states: `pending` / `active` / `failed`.

## Alternative SSL providers

Replace the binding in `LandingBuilderServiceProvider::register()`:

```php
$this->app->bind(SslProvider::class, VercelSslProvider::class);
```

See `App\LandingBuilder\Ssl\SslProvider` for the contract.
