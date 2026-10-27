# DevHub AI

Pusat kolaborasi development untuk satu tim berisi 9 orang. Setiap developer menjalankan OpenCode di laptop masing-masing, sementara web app mengelola project, task, dokumentasi, status agent, approval, dan integrasi GitHub.

## Prinsip utama
- Web app adalah control plane; laptop developer adalah execution plane.
- GitHub adalah sumber kebenaran source code dan pull request.
- Satu task memiliki satu penanggung jawab utama.
- Agent tidak boleh melakukan merge/deploy berisiko tanpa approval.
- Status "agent selesai" bukan berarti task otomatis selesai.
- Jangan mengklaim fitur selesai sebelum implementasi dan test benar-benar berhasil.

## Stack awal
- Next.js App Router + TypeScript
- Tailwind CSS + shadcn/ui
- Supabase Auth + PostgreSQL + Realtime
- GitHub App/webhooks atau integrasi GitHub yang terdokumentasi
- Local companion Node.js + TypeScript
- OpenCode server/SDK melalui dokumentasi resmi versi yang dipasang
- pnpm workspace monorepo
- Vitest dan Playwright
- GitHub Actions

## Quick start
Instruksi instalasi final harus dilengkapi oleh implementasi aktual. Jangan mengarang env var, command, atau endpoint. Lihat `docs/DEPLOYMENT.md`.

## Dokumentasi wajib
Mulai dari `docs/PRD.md`, `docs/ARCHITECTURE.md`, `docs/DATABASE.md`, `docs/API.md`, `docs/AGENT_PROTOCOL.md`, dan `docs/SECURITY.md`.
