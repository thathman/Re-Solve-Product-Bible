# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**SETUP COMPLETE — CLEAN STARTER VERIFIED — FOUND-001A NEXT**

## Canonical Product Bible state
- Repository: `thathman/Re-Solve-Product-Bible`.
- Visibility: `public`.
- Product Bible planning/expansion/launch-readiness content is canonical on `main`.
- First umbrella build slice: `FOUND-001 — Re:Solve Application + Core UI Foundation`.
- FOUND-001 is supervised through bounded substeps.

## Lovable project
- Project: `Re:Solve`
- Project Knowledge installed: `YES`.
- Canonical workspace Skills installed: `YES — all 30 Re:Solve skills plus self-host-check`.
- Platform default skill active: `design-taste-frontend`.
- Obsolete `airix-*` skills: `NONE`.
- Duplicate `.agents/skills/` drafts: `REMOVED`.

## Application repository
- Lovable-created application repository: `thathman/re-solve-c560d62c`.
- Visibility: `private`.
- Default branch: `main`.
- GitHub access verified independently by supervisor.
- Legacy reference repository remains: `thathman/Re-Solve`.
- Product Bible repository is specification/reference only, not application source.
- Root `AGENTS.md`: `NO — create during FOUND-001A`.
- Canonical-name transition performed: `NO`.

## Backend
- Development backend: `Lovable Cloud enabled`.
- Custom database tables: `NONE`.
- RLS policies: `NONE`.
- Migrations initialized: `NO`.
- Demo seed/reset initialized: `NO`.

Never store credentials/secrets in this file.

## Accepted slices
None yet.

## Verified starter baseline
- clean-starter classification: `A — safe to begin supervised foundation sequence`;
- framework/build stack: `TanStack Start v1`;
- React: `19.2.0`;
- package manager: `bun`;
- Tailwind: `4.2.1` using `@tailwindcss/vite`;
- TypeScript: `5.8.3`;
- Vite: `8.2.0`;
- shadcn: already initialized (`new-york`, CSS variables, Lucide icon library, standard `src/components/ui/` aliases);
- primitive base currently represented by installed Radix packages; do not reinitialize shadcn blindly;
- TanStack Query already installed (`@tanstack/react-query`);
- React Hook Form + Zod already installed;
- Recharts already installed;
- routes: only `src/routes/__root.tsx` and placeholder `src/routes/index.tsx`;
- Re:Solve-specific UI/components: none;
- business functionality: none;
- PWA files: none;
- tests/CI: none;
- no database migrations/schema yet;
- starter builds cleanly (`BUILD_SUCCESS`).

## Current architecture facts
- framework/build tool: `TanStack Start v1 + Vite`
- routing: `TanStack file-based routes`
- React: `19.2.0`
- package manager: `bun`
- Tailwind: `4.2.1`
- shadcn: `initialized; do not rerun init without an explicit migration decision`
- current UI primitives: `Radix + shadcn source components`
- primary icon library: `Lucide`
- query/server state: `TanStack Query already installed`
- form/validation: `React Hook Form + Zod already installed`
- chart foundation: `Recharts already installed`
- testing stack: `not configured`
- PWA tooling: `not configured`
- auth approach: `Lovable Cloud available; no Re:Solve auth/domain setup yet`
- service/repository boundaries: `not established`

## Current Core UI inventory
None beyond stock/generated shadcn primitives. No Re:Solve Core UI components accepted yet.

## Current database/domain inventory
None.

## Open Product Bible deltas
None currently blocking FOUND-001A.

## Known implementation limitations
- no CI/tests/PWA/AGENTS.md/Re:Solve architecture foundation yet;
- shadcn is already configured around the generated Radix-based starter, so any React Aria migration must be deliberate rather than automatic.

## Next action
Execute `FOUND-001A — Stack & Repository Preflight` only.
