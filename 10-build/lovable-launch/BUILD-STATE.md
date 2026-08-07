# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**SETUP-001 REQUIRED — CLEAN STARTER VERIFIED — FOUND-001 NOT YET STARTED**

## Canonical Product Bible state
- Product Bible planning/expansion/launch-readiness content is consolidated on `main`.
- Repository: `thathman/Re-Solve-Product-Bible`.
- Visibility: `public`.
- Public GitHub skill import is the preferred Lovable workspace-skill installation path.
- No open Product Bible pull requests remain from the initial planning stack.
- Pre-consolidation safety branch: `backup/pre-lovable-consolidation-main`.
- First umbrella build slice: `FOUND-001 — Re:Solve Application + Core UI Foundation`.
- FOUND-001 will be supervised through bounded substeps rather than one giant implementation prompt.

## Lovable project
- Workspace: `<record when confirmed>`
- Project: `Re:Solve`
- Project Knowledge installed in Project settings: `YES — owner confirmed`
- Canonical workspace Skills installed: `YES — all 30 canonical Re:Solve skills plus self-host-check verified active by Lovable`
- Platform default skill also active: `design-taste-frontend`.
- No obsolete `airix-*` skills reported.
- Duplicate project-local copies exist under `.agents/skills/`; remove them during SETUP-001 after workspace-skill verification.

## Application repository
- Legacy reference repository: `thathman/Re-Solve`
- Lovable-created application repository: `UNVERIFIED`.
- Lovable audit reported `thathman/Re-Solve-Product-Bible`, but explicitly stated this was derived from context because direct git remotes were not exposed. Do not treat that as application-repository truth.
- Application repository visibility/default branch: `UNVERIFIED` until Lovable/GitHub integration reports the actual synced app repository.
- Root AGENTS.md: `NO`
- Canonical-name transition performed: `NO`

## Backend
- Development backend: `Lovable Cloud enabled`
- Custom database tables: `NONE`
- RLS policies: `NONE`
- Migrations initialized: `NO`
- Demo seed/reset initialized: `NO`

Never store credentials/secrets in this file.

## Accepted slices
None yet.

## Setup/restart audit observations
Verified by Lovable restart audit:
- clean-starter classification: `A — safe to begin supervised foundation sequence`;
- framework/build stack: `TanStack Start v1`;
- React: `19.2.0`;
- package manager: `bun`;
- lockfile: `bun.lockb` expected/current platform convention;
- Tailwind: `4.2.1` using `@tailwindcss/vite`;
- shadcn: initialized with standard primitives in `src/components/ui/`;
- current dependencies include standard TanStack Start, Radix UI, Lucide, Zod and React Hook Form;
- routes: only `src/routes/__root.tsx` and placeholder `src/routes/index.tsx`;
- Re:Solve-specific UI/components: none;
- business functionality: none;
- PWA files: none;
- tests/CI: none;
- AGENTS.md: none;
- no database migrations/schema yet;
- 30 canonical project-local skill drafts remain redundant under `.agents/skills/`.

## Current architecture facts
- framework/build tool: `TanStack Start v1`
- routing: `TanStack file-based routes`
- React: `19.2.0`
- package manager: `bun`
- Tailwind: `4.2.1`
- shadcn: `already initialized; exact primitive base still to be inspected during FOUND-001A/B`
- current UI dependencies: `Radix UI + Lucide + standard shadcn primitives`
- query/state libraries: `inspect during FOUND-001A`
- testing stack: `not configured`
- PWA tooling: `not configured`
- auth approach: `Lovable Cloud available; no Re:Solve auth/domain setup yet`
- service/repository boundaries: `not established`
- major source directories: `starter only; inspect during FOUND-001A`

## Current Core UI inventory
None beyond stock/generated shadcn primitives. No Re:Solve Core UI components accepted yet.

## Current database/domain inventory
None.

## Open Product Bible deltas
None currently blocking FOUND-001.

## Known implementation limitations
- actual application GitHub repository identity is not yet verified;
- duplicate `.agents/skills/` drafts remain and should be removed once workspace skills are reconfirmed;
- no CI, tests, PWA, AGENTS.md or Re:Solve foundation exists yet.

## Next action
1. Run `SETUP-001` cleanup/repository-identity verification.
2. Remove duplicate `.agents/skills/` Re:Solve skill drafts only after reconfirming workspace skills are active.
3. Confirm the real Lovable-created application GitHub repository/default branch from Lovable's GitHub integration state; do not infer it from Product Bible context.
4. Begin `FOUND-001A — Stack & Repository Preflight` only after SETUP-001 passes.
