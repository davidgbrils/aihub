# Architecture — DevHub AI

## 1. Architecture decisions
- Monorepo with pnpm workspaces.
- `apps/web`: Next.js App Router, UI, server route handlers.
- `apps/companion`: Node.js local agent worker.
- `packages/contracts`: shared API types and schemas.
- Supabase Auth/Postgres/Realtime for MVP.
- GitHub is canonical for source control and PRs.
- OpenCode runs locally; web app never opens a public connection to a developer laptop.
- Companion initiates outbound HTTPS polling; no inbound port forwarding.
- Keep architecture modular, not microservices, until scale requires it.

## 2. Components
1. Browser/PWA: authenticated UI.
2. Next.js server: authorization, domain logic, job queue API, webhook endpoints.
3. Supabase: identity, data, RLS, realtime events.
4. GitHub: repository, branches, commits, pull requests, CI.
5. Local companion: device identity, repository allowlist, polling, job lease, local policy, OpenCode integration, Git operations, redaction.
6. OpenCode: local coding session and tools.

## 3. Data flow
- User creates task -> server persists task.
- User dispatches task -> server creates queued agent job.
- Companion polls -> server atomically claims job and returns short-lived lease.
- Companion validates repository/branch/policy -> invokes OpenCode locally.
- Companion sends bounded progress events and final result.
- Web UI subscribes to safe project events.
- Developer reviews diff and opens/links PR.
- GitHub webhook updates PR/check status after signature validation.

## 4. Failure handling
- Heartbeat and expiring leases.
- Idempotency keys for dispatch and event/result submissions.
- Retry only after checking whether local work has started or changed files.
- Reconcile job status after reconnect.
- Store concise error summaries; never log secrets.
- Event ingestion must be bounded and rate limited.

## 5. Realtime
Realtime is a UI notification mechanism, not the source of truth. Persist state first; UI can reload from API after reconnect.

## 6. Deployment
- Web app hosted on a provider supporting Next.js.
- Supabase managed project.
- Companion distributed separately for each supported OS.
- GitHub Actions runs lint/typecheck/test/build.
- Provide `.env.example` with names and descriptions only, no secrets.
