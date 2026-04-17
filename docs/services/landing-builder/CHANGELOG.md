# Changelog

## Unreleased — Landing Page Builder (initial)

### Added

- Per-tenant public landing pages on auto-subdomain + custom domain.
- Three-column visual editor (`/settings/landing-page`) with:
  - SortableJS drag & drop
  - Device switcher (mobile / tablet / desktop)
  - Locale switcher (AR / EN)
  - Undo / Redo (50-step history)
  - Autosave every 5 seconds while visible
- 12 MVP blocks (hero, features-grid, cta, faq, footer, testimonials, stats,
  rich-text, image, video, contact-form, header).
- Advanced blocks pipeline (starter: custom-html) behind
  `landing.advanced_blocks` system permission.
- Domain management (`/settings/domains`) with DNS TXT verification.
- Caddy on-demand TLS gate at `GET /_caddy/ask`.
- Public renderer at `GET /` on tenant hosts, including SEO, OG, hreflang,
  and JSON-LD.

### Database

- `tenants.slug` (unique, 63 chars) — backfilled from `tenants.name`.
- `tenant_landing_pages` — one row per tenant with JSON `draft_blocks`,
  `published_blocks`, `draft_theme`, `published_theme`, `seo`, `locales`.
- `tenant_domains` — subdomain + custom domain records with verification
  and SSL status.
- `tenant_brand_settings` — logos, colors, fonts per tenant.

### Permissions

- `landing.edit`, `landing.publish`, `landing.manage_domains` (tenant scope)
- `landing.advanced_blocks` (system scope)

### Notes

- Flux components are intentionally **not** used inside the Landing
  Builder. The rest of okta-web keeps Flux unchanged.
- Tenant resolution is performed by `App\Multitenancy\CompositeTenantFinder`,
  which replaces `SessionTenantFinder` but keeps session fallback for admin
  routes.
