# Task 07: Build Full Feature Test Coverage

## Goal
Add missing feature tests required by the main implementation plan.

## Read First
- `docs/prompts/build-notifications-management-service.md`
- `docs/services/notifications-management/tech/tenancy.md`
- `docs/services/notifications-management/tech/permissions.md`

## Current Gap
- No dedicated test suite covers notifications management end-to-end requirements.

## Required Work
1. Add tests for trigger flows:
   - API trigger path
   - event-trigger path
2. Add tests for locale behavior:
   - hierarchy resolution (platform/country/tenant/user)
   - fallback behavior
3. Add queue/retry tests:
   - failed send -> retry scheduled -> eventual status transition
4. Add permission tests:
   - admin vs tenant manager vs end user
   - forbidden responses for missing permissions
5. Add tenancy isolation tests:
   - cross-tenant update/delete/reads are blocked
6. Add notifications center behavior tests for key user actions.

## Acceptance Criteria
- Test suite covers all major plan requirements and passes reliably.
- Positive and negative paths are both covered.
- Critical regressions (authz/tenancy/duplicates) are protected by tests.

## Deliverables
- New test classes under `tests/Feature/NotificationsManagement`.
- Factories/helpers/fixtures required for maintainable tests.
- Clear naming and scenario grouping.
