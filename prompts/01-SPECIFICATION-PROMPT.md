# Prompt 1 — Create/Review all specification documents

Read `AGENTS.md` and `prompts/00-MASTER-PROMPT.md`.

Before writing code, inspect the repository. Create or reconcile these files:
- `README.md`
- `AGENTS.md`
- `docs/PRD.md`
- `docs/ARCHITECTURE.md`
- `docs/DATABASE.md`
- `docs/API.md`
- `docs/AGENT_PROTOCOL.md`
- `docs/SECURITY.md`
- `docs/TASKS.md`
- `docs/TESTING.md`
- `docs/DEPLOYMENT.md`
- `docs/DECISIONS.md`
- `docs/ROADMAP.md`
- `CONTRIBUTING.md`
- `.env.example`

Use the supplied docs as baseline. Make all docs consistent with one another. Add exact role permissions, API request/response schemas, state transition rules, error codes, job lease behavior, event schema, webhook verification, RLS policy matrix, and acceptance tests. Do not invent unsupported OpenCode endpoints: identify the installed version and use its official docs. Mark any unresolved decision explicitly.

Do not implement application features in this step. Validate links/paths and produce a docs consistency report. Update `docs/TASKS.md` only for specification tasks completed.
