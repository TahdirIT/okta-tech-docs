# API Reference

## Routes

| Method | Path                           | Middleware                                               | Handler                                                              |
|--------|--------------------------------|----------------------------------------------------------|----------------------------------------------------------------------|
| GET    | `/settings/landing-page`       | `auth`, `context`, `tenant.scope`, `permission:landing.edit`            | `App\Livewire\TenantLanding\Editor`                                   |
| GET    | `/settings/domains`            | `auth`, `context`, `tenant.scope`, `permission:landing.manage_domains`  | `App\Livewire\TenantLanding\DomainsManager`                            |
| GET    | `/_caddy/ask`                  | —                                                        | `App\Http\Controllers\TenantLanding\CaddyAskController`               |
| GET    | `/`  *(on a tenant host)*       | `ResolveTenantLandingHost`                               | `App\Http\Controllers\TenantLanding\PublicLandingController`          |

## Middleware

### `App\Http\Middleware\ResolveTenantLandingHost`

Prepended to the `web` middleware group. On the main app host, passes through;
on any other host, resolves the tenant via `DomainTenantResolver` and:

- `/`     → `PublicLandingController`
- other   → 404

## Livewire components

- `App\Livewire\TenantLanding\Editor`
- `App\Livewire\TenantLanding\DomainsManager`

Both use `layouts.dashboard` as the outer layout.

### Livewire events

| Event name                  | Direction  | Payload               | Purpose |
|-----------------------------|------------|-----------------------|---------|
| `landing-editor:reorder`    | client → server | `{ orderedIds: string[] }` | SortableJS reorder commit |
| `landing-editor:saved`      | server → client | —                      | After a successful autosave |
| `landing-editor:published`  | server → client | —                      | After publish succeeds |
| `landing-editor:unpublished`| server → client | —                      | After unpublish succeeds |
| `domain-added`              | server → client | —                      | After `addCustomDomain` |

## Services & bindings

| Binding                                                  | Default implementation                                    |
|----------------------------------------------------------|-----------------------------------------------------------|
| `App\LandingBuilder\BlockRegistry` (singleton)            | Registers all blocks at boot via `LandingBuilderServiceProvider` |
| `App\Multitenancy\DomainTenantResolver` (singleton)       | Cached host → tenant resolver                              |
| `App\LandingBuilder\Ssl\SslProvider` (interface)          | `CaddyOnDemandSslProvider`                                 |
| `App\LandingBuilder\Services\DomainVerificationService`   | DNS TXT verification                                       |

## Block contract

```php
abstract class App\LandingBuilder\Contracts\Block
{
    abstract public function type(): string;
    abstract public function category(): string;
    abstract public function icon(): string;
    abstract public function labels(): array;
    abstract public function rendererView(): string;
    abstract public function editorView(): string;
    abstract public function defaultContent(string $locale): array;

    public function defaultSettings(): array;
    public function superAdminOnly(): bool;
    public function validate(array $content, string $locale): array;
}
```

## Models

- `App\Models\TenantLandingPage`
  - `isPublished(): bool`
  - `effectiveBlocks(bool $preferDraft = false): array`
  - `effectiveTheme(bool $preferDraft = false): array`
  - `publish(): void`
  - `unpublish(): void`
- `App\Models\TenantDomain`
  - `isVerified(): bool`
  - `isSslActive(): bool`
  - `expectedDnsRecord(): array`
  - `markVerified(): void`
  - `markVerificationFailed(): void`
- `App\Models\TenantBrandSettings::defaults(): array`

## Permissions

| Name                       | Scope  | Default role             |
|----------------------------|--------|--------------------------|
| `landing.edit`             | tenant | `tenant-admin`           |
| `landing.publish`          | tenant | `tenant-admin`           |
| `landing.manage_domains`   | tenant | `tenant-admin`           |
| `landing.advanced_blocks`  | system | `superadmin`             |
