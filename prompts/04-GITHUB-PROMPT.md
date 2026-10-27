# Prompt 4 — GitHub integration

Implement T030–T033 according to `docs/API.md`, `docs/SECURITY.md`, and `docs/DEPLOYMENT.md`.

First inspect the current GitHub integration options and choose the least-privilege approach suitable for one repository. Document required permissions and setup steps. Implement repository association, PR listing/details, branch and check status, and webhook event processing where credentials are configured.

Requirements:
- Verify webhook signature before processing.
- Deduplicate delivery IDs and make processing idempotent.
- Validate repository identity against configured project repository.
- Never trust actor/URL/repository solely from payload.
- Store only required metadata; GitHub remains source of truth.
- Show disconnected/configuration-required states rather than fake data.
- Add tests for valid/invalid signatures, duplicate deliveries, and repository mismatch.
- If credentials are absent, use mocked payloads only in tests and clearly label the integration unconfigured in UI.
