# Database Design — DevHub AI

Use UUID primary keys, `timestamptz` timestamps, foreign keys, indexes, check constraints, and migrations. Every project-owned record must carry `project_id` directly or through a relation that can be securely authorized.

## Tables
### profiles
- `id uuid primary key references auth.users(id) on delete cascade`
- `display_name text not null`
- `avatar_url text null`
- `created_at timestamptz not null default now()`

### projects
- `id uuid primary key default gen_random_uuid()`
- `name text not null`
- `slug text unique not null`
- `description text`
- `github_repo_owner text`
- `github_repo_name text`
- `created_by uuid references profiles(id)`
- timestamps

### project_members
- `project_id uuid references projects(id) on delete cascade`
- `user_id uuid references profiles(id) on delete cascade`
- `role text check in ('admin','lead','developer','reviewer')`
- `joined_at timestamptz default now()`
- primary key `(project_id,user_id)`

### tasks
- `id uuid primary key`
- `project_id uuid not null references projects(id)`
- `title text not null`
- `description text`
- `status text check in ('backlog','ready','in_progress','blocked','in_review','done','cancelled')`
- `priority text check in ('low','medium','high','urgent')`
- `assignee_id uuid references profiles(id)`
- `created_by uuid references profiles(id)`
- `acceptance_criteria jsonb not null default '[]'`
- `due_at timestamptz`
- `version integer not null default 1`
- timestamps

### task_dependencies
- `task_id uuid references tasks(id) on delete cascade`
- `depends_on_task_id uuid references tasks(id) on delete cascade`
- primary key `(task_id, depends_on_task_id)`
- enforce same-project dependency and prevent cycles in transactional application logic or a database trigger.

### task_comments
- id, task_id, author_id, body, created_at

### documents
- id, project_id, title, document_type, content text, version integer default 1, updated_by, updated_at
- Use optimistic concurrency: update only when expected version matches.

### agent_instances
- id, project_id, user_id, device_name, agent_type, status, capabilities jsonb, last_seen_at, revoked_at, created_at
- Never store raw long-lived secrets in readable columns. Store hashes for device tokens if using bearer tokens.

### agent_jobs
- id, project_id, task_id, agent_instance_id, requested_by, status, prompt_snapshot, branch_name, idempotency_key, lease_expires_at, started_at, finished_at, error_summary, result jsonb, timestamps
- unique `(requested_by, idempotency_key)` where appropriate.
- indexes on `(status, created_at)`, `(agent_instance_id,status)`, `(task_id,created_at)`.

### agent_events
- id, job_id, event_type, summary, metadata jsonb, created_at
- index `(job_id, created_at)`.
- Do not store full unredacted terminal output by default.

### approvals
- id, project_id, job_id, requested_by, reviewed_by, action_type, status, reason, created_at, reviewed_at
- status check: pending/approved/rejected/cancelled.
- enforce reviewer authorization server-side.

### pull_requests
- id, project_id, task_id, github_pr_number, github_url, branch_name, state, checks_state, updated_at
- unique `(project_id, github_pr_number)`.

### audit_logs
- id, project_id, actor_id, action, resource_type, resource_id, metadata jsonb, created_at
- append-only for application roles; never store secrets.

## Job status
`queued`, `claimed`, `running`, `awaiting_approval`, `succeeded`, `failed`, `cancelled`, `expired`.

## RLS requirements
- Enable RLS on all project/user-owned tables.
- Membership must be checked for SELECT/INSERT/UPDATE/DELETE.
- Only authorized roles can manage membership, approve actions, or change project settings.
- Device operations must verify both device ownership and project membership.
- Never expose service-role credentials to browser or companion.
- Add tests proving cross-project access is denied.
