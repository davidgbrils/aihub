# Implementation Backlog

Use task IDs and keep this file updated. A task is complete only when its acceptance criteria and tests pass.

## Phase 0 — Specification
- [ ] T000 Read and reconcile all docs.
- [ ] T001 Record architecture decisions and assumptions.
- [ ] T002 Define exact environment variables and setup prerequisites.
- [ ] T003 Confirm OpenCode API against installed version's official docs.

## Phase 1 — Foundation
- [ ] T010 Create pnpm monorepo and apps/packages.
- [ ] T011 Set up Next.js, TypeScript, lint, format, typecheck, test, build.
- [ ] T012 Set up Supabase config and migrations.
- [ ] T013 Implement auth and profile provisioning.
- [ ] T014 Implement project membership and role checks.
- [ ] T015 Implement RLS and cross-project access tests.

## Phase 2 — Project management
- [ ] T020 Dashboard UI with real data and empty/loading/error states.
- [ ] T021 Task CRUD, filters, statuses, priority, assignee.
- [ ] T022 Task dependencies with cycle prevention.
- [ ] T023 Comments and activity feed.
- [ ] T024 Markdown documents with optimistic concurrency.
- [ ] T025 Repository and pull request views.

## Phase 3 — GitHub
- [ ] T030 GitHub connection strategy and least-privilege permissions.
- [ ] T031 Repository/PR status synchronization.
- [ ] T032 Verify webhook signatures and idempotent event processing.
- [ ] T033 CI and branch protection documentation.

## Phase 4 — Companion and OpenCode
- [ ] T040 Companion pairing and device revocation.
- [ ] T041 Repository allowlist and safe path handling.
- [ ] T042 Heartbeat and polling with backoff.
- [ ] T043 Atomic job claim and lease.
- [ ] T044 OpenCode adapter verified against actual installed API.
- [ ] T045 Event streaming, redaction, reconnect/reconciliation.
- [ ] T046 Git worktree/branch creation and cleanup safeguards.
- [ ] T047 Result submission, cancellation, retry safety.

## Phase 5 — Approval and quality
- [ ] T050 Approval flow and audit logs.
- [ ] T051 Unit/integration tests.
- [ ] T052 Playwright end-to-end tests.
- [ ] T053 Concurrency and offline recovery tests.
- [ ] T054 Accessibility and responsive checks.
- [ ] T055 Fresh-install deployment rehearsal.
- [ ] T056 Pilot with 2 members, then all 9.

## Release gate
- [ ] No critical security findings.
- [ ] No fake production metrics or nonfunctional controls.
- [ ] All mandatory checks pass.
- [ ] Docs match actual implementation.
- [ ] Known limitations are documented.
