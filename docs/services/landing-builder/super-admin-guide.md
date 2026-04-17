# Super Admin Guide

Super admins (users holding a role with the system-scope permission
`landing.advanced_blocks`) get two extra capabilities.

## 1. Advanced blocks

The editor's block picker reveals an **Advanced** category:

- **Custom HTML** — inserts raw HTML into the page. Output is not sanitised.
- **Custom Script** (planned) — `<script>` tag with attributes.
- **Embed** (planned) — third-party iframes with controlled allow-list.

These are gated server-side: `Editor::addBlock()` rejects advanced types
unless `canUseAdvanced` is true, and the block registry's
`all($includeAdvanced = false)` filters them out of the picker entirely for
regular tenants.

## 2. Impersonation hooks

The tenant resolver trusts `session('context.tenant_id')` for admin routes
and the request host for public routes. If you need to edit another tenant's
landing page, switch your active tenant context via the existing
Impersonation mechanism — the editor will re-mount against the new
`tenant_id` on next render.

## 3. Platform-level settings

Only super admins should edit:

- `landing.base_domain` — via the existing Platform Settings UI, or
  `PlatformSetting::setValue('landing.base_domain', 'okta.sa')`.

## 4. SSL failures

If Caddy's issuance repeatedly fails for a custom domain, inspect logs:

```bash
journalctl -u caddy | grep <hostname>
```

Common causes:

- DNS not yet pointing at the Caddy IP
- HTTP/01 challenge blocked by an upstream firewall
- Rate limit with Let's Encrypt — retry later or switch to a different CA

You can also force-revalidate a domain manually:

```bash
php artisan tinker
> $d = App\Models\TenantDomain::find(42);
> app(App\LandingBuilder\Services\DomainVerificationService::class)->verify($d);
```
