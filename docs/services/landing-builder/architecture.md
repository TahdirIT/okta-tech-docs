# Architecture

## High-level flow

```
Request → ResolveTenantLandingHost (middleware)
  │
  ├── Host == APP_URL host      → passthrough to admin/marketing routes
  │
  └── Host is a tenant host     → DomainTenantResolver::resolve(host)
         │                         ├── verified custom domain match
         │                         └── subdomain of platform base domain
         │
         ├── unknown             → 404 "Domain not configured"
         ├── path == '/'         → PublicLandingController
         └── other paths         → 404 (tenant hosts expose landing only)
```

## Tenant resolution

`App\Multitenancy\CompositeTenantFinder` replaces the old
`SessionTenantFinder` in `config/multitenancy.php`:

```php
public function findForRequest(Request $request): ?IsTenant
{
    $byHost = $this->resolver->resolve($request->getHost());

    if ($byHost !== null) {
        return $byHost;
    }

    $tenantId = session('context.tenant_id');

    return $tenantId ? Tenant::find($tenantId) : null;
}
```

This preserves the existing admin flow (session-based context) while adding
host-based resolution for public landing pages. Both flows can coexist on
separate requests; a single request only needs one.

Lookups are cached for 60 seconds in `Cache::` under the key
`landing:tenant_by_host:<host>` to protect the database from per-request hits.

## Content storage

One row per tenant in `tenant_landing_pages`:

```json
{
  "status": "draft | published",
  "draft_blocks":     [ /* Block[] */ ],
  "published_blocks": [ /* Block[] */ ],
  "draft_theme":      { "colors": {...}, "fonts": {...} },
  "published_theme":  { ... },
  "seo":              { "ar": {"title": "...", "description": "..."}, "en": {...} },
  "default_locale":   "ar",
  "locales":          ["ar", "en"]
}
```

Publishing is a simple copy:

```php
$page->published_blocks = $page->draft_blocks;
$page->published_theme  = $page->draft_theme;
$page->status           = 'published';
$page->published_at     = now();
$page->save();
```

## Block shape

Each block is a single JSON object, persisted in the `draft_blocks` /
`published_blocks` arrays:

```json
{
  "id": "9f1a...",
  "type": "hero",
  "order": 0,
  "content": {
    "ar": { "title": "...", "subtitle": "...", "primary_cta": {...} },
    "en": { "title": "...", ... }
  },
  "settings": {
    "padding": { "top": 80, "bottom": 80 },
    "background": { "type": "color", "value": "transparent" },
    "max_width": "normal",
    "align": "center"
  },
  "visibility": { "mobile": true, "tablet": true, "desktop": true }
}
```

Blocks are registered at boot in `LandingBuilderServiceProvider`. Each block
contributes two Blade partials under
`resources/views/landing-builder/blocks/{type}/`:

- `renderer.blade.php` — used by both the editor canvas and the public page
- `editor.blade.php`   — used by the inspector panel

`App\LandingBuilder\BlockRegistry::sanitize()` validates and normalises block
payloads before they are persisted — this is the only entry point that writes
to the DB.

## Editor state

`App\Livewire\TenantLanding\Editor` holds the whole editor state in Livewire
properties (`blocks`, `theme`, `seo`, `locale`, `device`,
`selectedBlockId`, `history`, `historyIndex`).

- **Drag & drop**: SortableJS on the client emits a
  `landing-editor:reorder` Livewire event with the ordered id list, which the
  server re-applies via `Editor::reorder()`.
- **Autosave**: Livewire `wire:poll.visible.5s="saveDraft"` + manual save
  button. Only writes when `$isDirty` is true.
- **Undo/redo**: simple in-component stack, capped at 50 snapshots.

## Public rendering

`App\Http\Controllers\TenantLanding\PublicLandingController::__invoke()` loads
the tenant's landing page, picks a locale (default or `?lang=` query) and
renders `resources/views/tenant-landing/public.blade.php`. That template:

- Sets `<html dir="rtl|ltr" lang="ar|en">`
- Writes full SEO meta, Open Graph, Twitter Card, hreflang, and JSON-LD
- Injects theme tokens as CSS variables on `:root`
- Iterates blocks and `@include`s each block's renderer view

## SSL

Abstracted behind the `SslProvider` interface. The default binding is
`CaddyOnDemandSslProvider`, which defers to Caddy's on-demand TLS feature.
See [Domain setup](./domain-setup.md) for the Caddyfile recipe.
