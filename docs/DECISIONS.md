# Architecture Decision Records

## ADR-001 — Web app/PWA first
Status: Accepted
Decision: Build Next.js web app/PWA before any desktop wrapper.
Reason: Easier deployment and updates for nine members; local companion handles filesystem access.

## ADR-002 — Local execution
Status: Accepted
Decision: OpenCode runs on each developer laptop.
Reason: Avoid cloud compute cost and keep repositories local.
Consequence: Companion lifecycle, device security, and OS compatibility are required.

## ADR-003 — OpenCode first
Status: Accepted
Decision: Support OpenCode only in the first release.
Reason: Reduces adapter complexity and makes integration testable.

## ADR-004 — GitHub is source of truth
Status: Accepted
Decision: GitHub owns code, branches, commits, PRs, and CI status.
Reason: Avoid building a custom Git hosting system.

## ADR-005 — Polling first
Status: Accepted
Decision: Companion polls outbound over HTTPS with leases and backoff.
Reason: Avoid inbound ports, tunnels, and complex networking.
Consequence: Job pickup is near-real-time, not instantaneous.

## ADR-006 — Human approval for risky actions
Status: Accepted
Decision: No automatic merge/deploy or destructive privileged action in MVP.
Reason: Reduce risk from autonomous coding tools.

## ADR-007 — Free tier is for pilot
Status: Accepted
Decision: Start on free tier, but document limits and pause behavior.
Reason: Minimize cost while validating usefulness.
