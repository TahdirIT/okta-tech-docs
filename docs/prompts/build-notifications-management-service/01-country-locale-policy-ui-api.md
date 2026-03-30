# Task 01: Complete Country Locale Policy (UI + API)

## Goal
Implement the missing "locale policy by country" capability end-to-end for Notifications Management.

## Read First
- `docs/services/notifications-management/pages/platform-settings.md`
- `docs/services/notifications-management/tech/tenancy.md`
- `docs/services/notifications-management/tech/permissions.md`
- `docs/services/notifications-management/tech/service_functions/api_endpoints.md`

## Current Gap
- Platform notifications settings currently supports platform default/fallback locale only.
- Country-level locale policy management and inheritance visibility are still incomplete.

## Required Work
1. Add country locale policy APIs:
   - list/get country policy
   - create/update country default/fallback locale
2. Add route protection using `can:` middleware and in-controller authorization.
3. Build UI in platform notifications settings for:
   - selecting a country
   - editing default/fallback locale per country
   - viewing inheritance behavior to tenant level
4. Ensure locale resolution service uses platform -> country -> tenant hierarchy consistently.
5. Add validation and clear error messages for invalid locale codes.

## Acceptance Criteria
- Admin can update locale policy for each country from UI.
- Country policy is persisted and retrieved via API.
- Effective locale resolution respects hierarchy and fallback rules.
- Permission checks are enforced on routes, controller actions, and Blade actions.
- No cross-country or cross-tenant policy leakage.

## Deliverables
- Controllers, services, request validation, routes.
- Livewire/Blade updates in platform notifications page.
- Seeded/used permission codes aligned with docs.
- Feature tests for country locale policy flows.
