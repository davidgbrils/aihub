# Deployment and Operations

## Environments
- Local development
- Preview/staging
- Production

Use separate Supabase projects for staging and production if the app becomes operationally important.

## Required configuration
Maintain `.env.example` with variable names, purpose, and whether each is server-only. Never include actual values. The implementation must document the precise variables it uses; do not invent variables without code.

Likely categories:
- Public Supabase URL and anon/publishable key
- Server-side Supabase configuration where needed
- GitHub App ID, private key, webhook secret, installation/repository identifiers as applicable
- Public app URL
- Companion pairing/API configuration
- Logging and feature flags

## Deploy web
1. Create Supabase project and apply migrations.
2. Configure Auth redirect URLs.
3. Configure hosting environment variables.
4. Configure GitHub App/webhook only after endpoint is deployed.
5. Run lint, typecheck, tests, build.
6. Verify auth, RLS, task CRUD, webhook signature, and Realtime.
7. Confirm secrets are absent from browser bundles and logs.

## Companion distribution
- Provide per-OS installation instructions and signed binaries only when signing pipeline is implemented.
- For MVP, document a trusted local development install from source.
- Explain how to pair, allowlist repository, update, inspect logs, and revoke device.

## Operations
- Monitor application errors, failed jobs, stale heartbeats, webhook failures, and database usage.
- Document backup/export and recovery.
- Review free-tier limits before inviting all users.
- Never promise uptime or backup guarantees provided by a free tier.
