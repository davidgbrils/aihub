# Security Threat Model

## Assets
- User sessions and project membership
- GitHub installation credentials
- Device credentials
- Local source code and filesystem
- Provider API keys and environment secrets
- Job prompts, events, diffs, and audit logs

## Trust boundaries
- Browser is untrusted.
- Repository content and task descriptions are untrusted.
- Cloud server cannot be trusted to execute arbitrary local commands.
- Local companion is a privileged bridge and must enforce local policy.
- OpenCode and its tools may read/write files and execute commands within configured permissions.

## Required controls
- Supabase RLS plus server-side authorization.
- Least-privilege GitHub App permissions.
- Verify GitHub webhook signatures and deduplicate delivery IDs.
- Device pairing code expires and is single-use; credentials are revocable.
- Store tokens securely; hash server-side device tokens where feasible.
- Never expose Supabase service-role key to client or companion.
- Never expose OpenCode server on public interfaces.
- Restrict companion to allowlisted repository roots and branch/worktree rules.
- Require local confirmation for destructive commands, deployment, merge, and secret changes.
- Redact tokens, passwords, `.env` contents, and credential-like strings from logs.
- Limit request body, event length, polling rate, and retention.
- Audit membership changes, device revocation, approval decisions, and job dispatch.
- Add CSRF protection where cookie-authenticated mutation routes require it.
- Use secure cookies, CSP, input validation, dependency scanning, and secret scanning.
- Protect default branch and require review/CI checks.

## Incident response
- Revoke affected device credentials and GitHub installation token.
- Disable affected agent instance/jobs.
- Rotate exposed secrets.
- Preserve sanitized audit records.
- Document incident and remediation in `docs/DECISIONS.md` or a dedicated incident record.

## Security acceptance tests
- Non-member cannot read project/task/document/job.
- Developer cannot change roles or approve unauthorized action.
- Revoked device cannot heartbeat, claim, or report results.
- Invalid webhook signature is rejected.
- Expired lease cannot update job.
- Path traversal/symlink escape is rejected.
- Secrets are not present in logs or browser bundle.
