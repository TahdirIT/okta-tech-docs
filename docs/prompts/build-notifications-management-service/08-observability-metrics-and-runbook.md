# Task 08: Observability, Metrics, and Local Runbook

## Goal
Add production-grade observability and operational documentation for notifications management.

## Read First
- `docs/services/notifications-management/tech/service_functions/schedulers.md`
- `docs/prompts/build-notifications-management-service.md`

## Current Gap
- Delivery logs exist, but counters/timers/reporting and clear local run instructions are missing.

## Required Work
1. Add metrics instrumentation for:
   - notifications triggered
   - sent/failed/retried counts
   - per-channel success/failure rates
   - dispatch/render latency timers
2. Add structured logs with stable fields (definition key, tenant, channel, provider, outcome).
3. Add export/report endpoint or command for delivery summaries per tenant/channel/definition.
4. Document local operations:
   - queue worker startup
   - scheduler startup
   - retry flow checks
   - troubleshooting common failures

## Acceptance Criteria
- Operators can inspect service health and failure patterns quickly.
- Metrics and logs are consistent and actionable.
- Local runbook enables a developer to run and verify the full pipeline.

## Deliverables
- Metrics/logging implementation updates.
- Reporting/export implementation (endpoint or artisan command).
- Documentation file(s) for local run and monitoring workflow.
