# Product Requirements Document — DevHub AI

## 1. Product vision
A single workspace for a nine-person software team to coordinate human developers and their individual OpenCode agents from one web application.

## 2. Users and roles
- Admin: workspace/project configuration, membership, integrations, security settings.
- Project Lead: create/assign tasks, manage workflow, approve designated actions.
- Developer: manage assigned tasks, connect own companion, view project docs, submit results.
- Reviewer: review agent results and PRs, approve/reject reviewable actions.
Roles can be combined for a user where the permission model explicitly allows it.

## 3. Goals
- One source of truth for tasks, project docs, agent job status, and approvals.
- Each developer runs OpenCode locally.
- Developers can work in parallel without sharing a single writable workspace.
- All agent work is reviewable and traceable.
- Start with free/low-cost infrastructure.

## 4. Non-goals for MVP
- Building a new LLM or coding engine.
- Remote desktop/control of developer laptops.
- Automatic merge/deploy to production.
- Arbitrary cloud shell access.
- Real-time collaborative code editing.
- Multi-tenant SaaS billing.
- Guaranteed compatibility with every coding agent; OpenCode only for first release.

## 5. Core user journeys
1. Admin creates project and invites members.
2. Member signs in and sees dashboard.
3. Lead creates task with acceptance criteria, owner, priority, dependencies.
4. Developer registers companion and authorizes a local repository.
5. Developer assigns a task to their own OpenCode agent.
6. Companion claims job, creates/uses isolated branch/worktree, runs OpenCode and publishes events.
7. Developer inspects summary, diff, test outcomes, and PR link.
8. Reviewer approves/rejects; task moves through review workflow.
9. Team tracks history and documents decisions.

## 6. MVP features
- Auth and membership/roles.
- Project dashboard and Kanban/list task views.
- Task CRUD, comments, labels/priority, assignee, acceptance criteria, dependencies.
- Shared Markdown documents with version conflict protection.
- Agent instance registration, heartbeat, online/idle/running/error status.
- Job queue with atomic claim, lease, cancellation, retry policy.
- OpenCode local companion for Windows/macOS/Linux where feasible.
- Agent event feed and result submission.
- GitHub repository/PR linking and verified webhook handling.
- Approval and audit trail.
- Search, filters, empty/loading/error states.
- RLS, server-side authorization, device revocation.
- Automated tests, setup docs, deployment docs.

## 7. Later features
- AI task planner, agent conflict hints, cost reporting where provider data exists, more adapters, preview deployments, advanced analytics.

## 8. UX requirements
- Sidebar: Dashboard, Tasks, Agents, Pull Requests, Documents, Repository, Activity, Settings.
- Dashboard: task counts, active agents, open PRs, task board, agent panel, recent activity, docs, progress.
- Agent page: device status, current job, session events, last heartbeat, cancel/revoke actions.
- Task detail: description, acceptance criteria, dependencies, comments, related job, branch/PR, test results.
- Responsive, accessible, clear empty/error/loading states.
- Do not show fabricated live status or invented usage metrics.

## 9. Acceptance criteria
- Nine members can use one project with role-based permissions.
- User A cannot read or mutate project data without membership.
- Duplicate job claims are prevented under concurrency.
- Companion offline does not lose job history.
- Agent works only in approved repository and assigned branch/worktree.
- Agent results are reviewable and never auto-merge.
- GitHub webhook signatures are verified.
- Tests cover authorization, job claiming, lease expiry, event ingestion, and key UI journeys.
- Clean setup from documented steps succeeds in a fresh environment.
