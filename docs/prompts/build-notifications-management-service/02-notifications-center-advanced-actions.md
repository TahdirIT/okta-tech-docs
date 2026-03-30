# Task 02: Complete Notifications Center Advanced Features

## Goal
Implement all missing notifications center states, filters, and user actions defined in docs.

## Read First
- `docs/services/notifications-management/pages/notifications-center.md`
- `docs/services/notifications-management/tech/permissions.md`

## Current Gap
- Current center supports only `all/unread`, mark single read, mark all read.
- Missing pinned, archived, type filters, and actions (pin/archive/delete).

## Required Work
1. Extend data model (if needed) to support:
   - `is_pinned`
   - `is_archived`
   - soft/hard delete behavior policy
   - notification type/category filtering
2. Add APIs and Livewire actions for:
   - pin/unpin
   - archive/unarchive
   - delete (according to role/policy)
3. Add UI filters/tabs:
   - unread/read/pinned/archived/by-type
4. Add details panel or view for notification content + contextual links/data.
5. Keep unread counter accurate after each action.

## Acceptance Criteria
- User can filter notifications by required states and type.
- User can execute pin/archive/delete actions and see immediate UI updates.
- Permission checks apply to sensitive actions.
- API and UI remain tenant-safe and user-scoped.

## Deliverables
- Migration/model updates if needed.
- Controller/endpoint and Livewire action updates.
- Notifications center Blade updates.
- Feature tests for actions, filters, and unread count integrity.
