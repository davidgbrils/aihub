# Prompt 6 — Approvals, audit, events, resilience

Implement T050 and related missing reliability work.

- Build a real approval queue and decision flow.
- Enforce reviewer role and ownership server-side.
- Audit task dispatch, device registration/revocation, permission changes, approval decisions, and job outcomes.
- Persist job state before broadcasting Realtime events.
- Add pagination, bounded payloads, safe error messages, event redaction, and rate limiting.
- Add lease expiry handling, duplicate event/result idempotency, and stale-job recovery.
- Ensure UI clearly distinguishes queued, running, awaiting approval, succeeded, failed, cancelled, and expired.
- Add tests for unauthorized approval, revoked device, expired lease, duplicate result, offline companion, and concurrent job claims.
- Do not represent an agent as running based only on stale presence; derive status using heartbeat freshness.
