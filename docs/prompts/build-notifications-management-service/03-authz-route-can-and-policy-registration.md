# Task 03: Harden Authorization (Route `can:` + Policy Registration)

## Goal
Bring authorization implementation to full compliance with project permission standards.

## Read First
- `docs/services/notifications-management/tech/permissions.md`
- `docs/tech-standards/permissions-naming.md`

## Current Gap
- Many checks are done in controllers only.
- API routes are not consistently protected with `can:*`.
- Notification policies exist but are not fully wired/used centrally.

## Required Work
1. Add `can:` middleware to notifications API routes where applicable.
2. Keep controller `Gate::authorize(...)` as defense-in-depth.
3. Register notification-related policies in the app provider.
4. Verify Blade `@can` usage for all buttons/actions.
5. Ensure permission names exactly match naming standard and seeded values.

## Acceptance Criteria
- Unauthorized users fail early at route layer.
- Policy mapping is active and used consistently.
- No route allows privileged notifications actions without proper permission.
- Existing authorized scenarios continue to pass.

## Deliverables
- Route updates, provider policy registration updates.
- Controller and Blade cleanup for consistency.
- Tests proving forbidden/allowed behavior per role.
