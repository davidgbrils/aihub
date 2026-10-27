# Testing Strategy

## Layers
- Unit: domain logic, schemas, permission helpers, status transitions.
- Database: migrations, RLS, constraints, transactional job claim.
- Integration: API, Supabase, webhook signature validation, companion protocol.
- Companion: mocked OpenCode adapter plus a manual test against installed OpenCode.
- E2E: sign in, create task, dispatch job, observe events, inspect result, review/approve.
- Security: cross-project access, revoked device, expired lease, path traversal, webhook forgery.
- Resilience: laptop disconnect, server timeout, duplicate events, repeated result submissions.

## Required commands
The actual repository must define and document package scripts for lint, typecheck, test, test:e2e, and build. Never list a command as supported until it exists.

## Test data
Use synthetic data only. Seed data must be clearly identified as demo/test data and must never appear as real live metrics.

## Release criteria
- Required tests pass in CI.
- No unhandled promise rejections or silently swallowed failures.
- Error states are visible and actionable.
- A clean clone can be configured by following docs.
