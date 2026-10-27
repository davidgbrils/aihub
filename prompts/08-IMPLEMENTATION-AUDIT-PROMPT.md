# Prompt 8 — Audit implementation against docs

Act as an independent senior engineer. Do not assume previous agent claims are true.

Compare the actual codebase against:
- `docs/PRD.md`
- `docs/ARCHITECTURE.md`
- `docs/DATABASE.md`
- `docs/API.md`
- `docs/AGENT_PROTOCOL.md`
- `docs/SECURITY.md`
- `docs/TESTING.md`
- `docs/DEPLOYMENT.md`
- `docs/TASKS.md`

For every requirement, classify it as:
- VERIFIED: implemented and supported by a passing test or reproducible manual check;
- IMPLEMENTED-UNVERIFIED: code exists but verification is missing;
- PARTIAL: some behavior exists;
- MISSING: absent;
- BLOCKED: needs credentials or external access.

Inspect actual routes, database migrations, RLS policies, UI controls, OpenCode adapter, companion security, GitHub webhook handling, job concurrency, error handling, and docs. Create `docs/IMPLEMENTATION_AUDIT.md` with evidence (file paths, tests, commands), severity, and remediation tasks. Then fix critical/high issues in small increments and rerun affected checks. Never mark an item verified based on source-code presence alone.
