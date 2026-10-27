# Prompt 2 — Monorepo, foundation, auth, security

Implement Phase 1 according to docs and task IDs T010–T015.

- Set up pnpm workspace with `apps/web`, `apps/companion`, and shared packages.
- Configure strict TypeScript, lint, formatting, unit test, and build scripts.
- Configure Supabase local/dev workflow and migration process.
- Implement auth, profile provisioning, project membership, role-based server checks, and RLS.
- Create typed validation and error-response conventions.
- Add seed data for local development only, clearly marked demo.
- Add tests for non-member access denial and role escalation denial.
- Create a responsive shell with sidebar/topbar, but do not fake live data.
- Document every env variable and exact setup command.

Run all applicable checks. Fix failures. Do not proceed to advanced task/agent features until auth, migrations, and RLS are verified.
