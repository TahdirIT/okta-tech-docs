# Task 06: Add Rate Limits, Batching, and Configurable Retry Policy

## Goal
Implement operational controls for notification dispatch per documented expectations.

## Read First
- `docs/services/notifications-management/tech/service_functions/schedulers.md`
- `docs/services/notifications-management/tech/data_handling/*.md`
- `docs/services/notifications-management/tech/models/channel.md`

## Current Gap
- Basic retry exists, but no complete rate limiting strategy and no batching support.
- Retry policy is not sufficiently configurable.

## Required Work
1. Add rate-limiting controls:
   - API trigger throttling
   - channel/provider dispatch limits
2. Add batching mode for eligible notifications.
3. Implement configurable retry policy (attempt caps, delay strategy, backoff).
4. Persist retry metadata for observability and safe rescheduling.
5. Ensure scheduler jobs process retries/batches safely with tenancy awareness.

## Acceptance Criteria
- Rate limits actively protect API and dispatch pipeline.
- Batch dispatch can be enabled for supported use-cases.
- Retry behavior follows configured policies and is test-verified.
- No duplicate sends for same idempotency key.

## Deliverables
- Config additions + job/service updates.
- Any needed schema additions for retry/batch metadata.
- Feature tests for throttle, retry, and idempotency behavior.
