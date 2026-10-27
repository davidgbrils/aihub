# Prompt 9 — Final UI polish against the dashboard mockup

Review the approved DevHub AI dashboard mockup and `docs/PRD.md`.

Polish the real app without changing business logic:
- navy sidebar with clear active state;
- project header and global search;
- summary cards backed by real queries;
- task board with clear status/priority tags;
- Team Agents panel with truthful online/idle/running state;
- recent activity, pull requests, documents, project progress;
- consistent spacing, typography, borders, responsive behavior, and keyboard focus;
- skeletons, empty states, errors, retry controls, and confirmations;
- avoid overcrowded columns on smaller screens;
- preserve accessibility and reduced-motion preferences.

Do not use fabricated profile activity, PR numbers, metrics, or agent status in production. Demo fixtures must be visibly labeled. Ensure all buttons work and add/update Playwright smoke tests for major pages.
