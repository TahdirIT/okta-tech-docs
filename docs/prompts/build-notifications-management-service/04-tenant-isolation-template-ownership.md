# Task 04: Enforce Tenant Isolation for Template Update/Delete

## Goal
Close tenant isolation gaps in template update/delete flows to prevent cross-tenant access.

## Read First
- `docs/services/notifications-management/tech/tenancy.md`
- `docs/services/notifications-management/tech/permissions.md`

## Current Gap
- Tenant scope is applied on list/create, but update/delete ownership checks are incomplete.

## Required Work
1. In template update/delete use-cases:
   - enforce scope-aware query (`admin` vs `tenant`)
   - when tenant scope, load template by id + `tenant_id = current tenant`
2. Add explicit forbidden response on ownership mismatch.
3. Ensure platform templates are not mutable from tenant scope.
4. Add regression tests for cross-tenant attack scenarios.

## Acceptance Criteria
- Tenant A cannot update/delete Tenant B template.
- Tenant cannot alter platform template through tenant endpoints.
- Admin scope behavior remains correct.
- All failures return proper HTTP status (403/404 per policy design).

## Deliverables
- Service and controller hardening.
- Additional request/context checks if needed.
- Feature tests covering isolation and negative cases.
