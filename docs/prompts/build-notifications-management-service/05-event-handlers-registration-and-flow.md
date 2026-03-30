# Task 05: Complete Event Handlers Wiring and Trigger Flow

## Goal
Wire domain/system events to Notifications Management so event-driven dispatch is fully operational.

## Read First
- `docs/services/notifications-management/tech/service_functions/event_handlers.md`
- `docs/services/notifications-management/tech/architecture.md`
- `docs/services/notifications-management/overview.md`

## Current Gap
- Listener class exists, but event registration and full event mapping are incomplete.

## Required Work
1. Register event listeners in the correct provider/bootstrap location.
2. Define event-to-notification-definition mapping strategy.
3. Ensure each event flow runs:
   - resolve definition
   - resolve effective locale
   - render template
   - create sent records and queue jobs
4. Add robust failure handling/logging for malformed payloads or missing definitions.
5. Add tests for at least one domain event and one system event.

## Acceptance Criteria
- Emitting mapped events creates queued notifications correctly.
- Unmapped events fail gracefully without breaking producer flows.
- Delivery logs capture attempts/failures for event-driven notifications.

## Deliverables
- Event registration and mapping implementation.
- Listener/service updates.
- Event-driven feature tests.
