# Prompt 5 — Local companion and OpenCode integration

Implement T040–T047. Read `docs/AGENT_PROTOCOL.md`, `docs/SECURITY.md`, and `docs/API.md` first.

Build a Node.js/TypeScript companion with:
- pairing flow using expiring single-use codes;
- revocable device identity;
- OS credential storage where practical, documented fallback otherwise;
- user-approved repository allowlist;
- safe path and symlink containment validation;
- outbound HTTPS polling with backoff/jitter;
- atomic job claim and lease heartbeat;
- job cancellation and safe reconnect/reconciliation;
- unique branch/worktree per job;
- configurable allowlist of commands/checks;
- redacted bounded event reporting;
- structured result submission.

OpenCode:
- Inspect the installed OpenCode version and official API/SDK docs.
- Isolate all OpenCode-specific calls in an adapter.
- Bind server to loopback only; never expose it publicly.
- Handle server process startup, health check, session creation, prompt dispatch, event consumption, result/diff retrieval, cancellation, timeout, and crash recovery as supported by the real API.
- Do not guess endpoint names or response schemas.
- Provide unit tests using a mocked adapter and a manual integration test procedure against a real local OpenCode installation.

Never execute arbitrary cloud-provided shell commands. Enforce local policy and require local confirmation for destructive/privileged actions. Do not automatically merge or deploy.
