# Prompt 7 — End-to-end QA and release hardening

Implement T051–T056. Read all docs before starting.

Run and fix:
- lint, typecheck, unit tests, integration tests, database/RLS tests, build;
- Playwright flows for auth, project, tasks, comments, documents, agent pairing, dispatch, event display, result review, approval, and PR display;
- concurrency tests for atomic job claims and idempotency;
- security tests for cross-project access, revoked devices, expired leases, invalid webhook signatures, path traversal, and secret leakage;
- responsive and accessibility checks.

Rehearse a fresh clone setup using only documented instructions. Verify migrations apply from a clean database. Confirm the UI has no dead buttons, fake production metrics, unhandled errors, or placeholder core functionality.

Update `docs/TASKS.md`, `docs/TESTING.md`, and `docs/DEPLOYMENT.md`. Report:
1. commands actually executed;
2. pass/fail results;
3. known limitations;
4. external integrations not tested because credentials were unavailable;
5. exact manual steps required before inviting all nine users.

Do not claim production-ready if any critical acceptance criterion is unverified.
