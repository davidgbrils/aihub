# Prompt 3 — Build functional project UI and task workflow

Implement T020–T025 according to `docs/PRD.md`, `docs/DATABASE.md`, and `docs/API.md`.

Create the DevHub AI interface inspired by the approved mockup:
- Navy sidebar: Dashboard, Tasks, Agents, Pull Requests, Documents, Repository, Activity, Settings.
- Top search, member presence, project selector, quick-create.
- Dashboard summary cards, real task board, agent panel, recent activity, PR list, project docs, progress.
- Task board with backlog, ready, in progress, in review, done; filters and list view.
- Task detail with owner, priority, acceptance criteria, dependencies, comments, linked jobs and PRs.
- Documents view with Markdown editing and optimistic concurrency.
- Agent page may show a true empty state until companion integration exists.

Use real database-backed state. Every control must have implemented behavior, loading/empty/error states, keyboard access, and responsive layout. No hardcoded counts or fake live statuses in production. Create Playwright tests for primary task flows and authorization tests for APIs.
