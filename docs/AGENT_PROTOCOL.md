# Local Agent Protocol

## Purpose
Define a safe protocol between the web control plane and a companion process running on each developer laptop.

## Device lifecycle
1. User signs in to web app.
2. User creates a one-time pairing code in web app.
3. Companion exchanges the code through an authenticated flow.
4. Server issues a revocable device credential; store it in OS credential storage where available.
5. User explicitly allowlists local repository paths.
6. Companion sends heartbeat with version, capabilities, and safe status metadata.
7. User can revoke device; revoked devices must be rejected immediately.

Pairing codes must expire quickly, be single-use, and be rate limited.

## Polling and job leases
- Companion polls with exponential backoff and jitter.
- Claim is atomic: only one companion may claim a job.
- Claimed jobs have a lease expiry and heartbeat.
- Every mutation verifies device ownership, project membership, job state, and lease.
- Use idempotency keys for events/results.
- Do not re-run an interrupted job blindly; inspect local workspace state first.

## Job payload
Must include job ID, task ID, task description, acceptance criteria, relevant doc excerpts/version identifiers, allowed repository identifier, requested branch, policy profile, lease expiry, and cancellation state. Never include provider secrets.

## OpenCode adapter
- Check the installed OpenCode version and use its official server API/SDK docs for that version.
- Bind OpenCode server to loopback only.
- Use a random local port where possible; do not expose unauthenticated server endpoints.
- Start/stop process safely and handle crashes.
- Create session, send task prompt, consume events, fetch messages/diff as supported by the installed version.
- Keep endpoint and schema assumptions isolated in `apps/companion/src/opencode/`.
- Treat events as untrusted data; bound event size and redact secrets.
- If the API version differs, fail clearly rather than silently using guessed endpoints.

## Git/workspace policy
- Repository path must be allowlisted by the user.
- Validate path containment and symlinks; never accept arbitrary path from server.
- Create a unique branch/worktree per job by default.
- Never checkout or write to protected main branch.
- Do not run destructive Git commands automatically.
- Detect dirty worktrees before starting.
- Provide cancellation and cleanup that preserve user changes.
- Run only configured commands; privileged/destructive commands require local approval.

## Events
Allowed event types include `job.claimed`, `job.started`, `agent.message`, `tool.started`, `tool.completed`, `check.started`, `check.completed`, `approval.required`, `job.completed`, `job.failed`, `job.cancelled`.
Store concise summaries and metadata, not unlimited raw logs.

## Result
Include status, summary, branch, changed file list, checks executed/results, known limitations, and PR URL only if verified. Never claim tests passed if they did not run.
