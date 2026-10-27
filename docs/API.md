# API Contract — DevHub AI

All routes use `/api/v1`. Use Zod schemas (or equivalent runtime validation) from `packages/contracts`. Return consistent JSON and HTTP status codes.

## Error format
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Request could not be validated",
    "request_id": "..."
  }
}
```
Do not expose stack traces, secrets, internal tokens, or raw provider output.

## Project/task routes
- `GET /projects/:projectId`
- `GET /projects/:projectId/members`
- `GET /projects/:projectId/tasks`
- `POST /projects/:projectId/tasks`
- `GET /tasks/:taskId`
- `PATCH /tasks/:taskId`
- `POST /tasks/:taskId/comments`
- `GET /projects/:projectId/documents`
- `POST /projects/:projectId/documents`
- `PUT /documents/:documentId` — requires expected version
- `GET /projects/:projectId/activity`

## Companion routes
- `POST /agents/register`
- `POST /agents/heartbeat`
- `POST /agents/:agentId/revoke`
- `GET /agents/jobs/next` — atomically claims a compatible queued job and returns a lease.
- `POST /agents/jobs/:jobId/heartbeat`
- `POST /agents/jobs/:jobId/events`
- `POST /agents/jobs/:jobId/result`
- `POST /agents/jobs/:jobId/cancel`

## Approval routes
- `POST /jobs/:jobId/approvals`
- `POST /approvals/:approvalId/decision`

## GitHub
- `POST /webhooks/github`
- Verify `X-Hub-Signature-256` before parsing/processing payload.
- Process webhook events idempotently.
- Do not trust a URL, repository, or actor merely because it appears in a payload.

## API requirements
- Authenticate every private route.
- Authorize resource access on the server.
- Use rate limits and request size limits for companion endpoints.
- Use idempotency keys for job dispatch/result submissions.
- Validate job lease and device ownership on every companion write.
- Return `409 CONFLICT` for stale document versions or invalid state transitions.
- Use pagination for event feeds and task lists.
- Document all implemented request/response schemas; don't document routes that don't exist as working behavior.
