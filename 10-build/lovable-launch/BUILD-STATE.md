# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A CONDITIONAL — ONE VERIFIED ENVIRONMENT-BOUNDARY ITEM REMAINS BEFORE FOUND-001B**

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
- Root `AGENTS.md`: `YES — created in FOUND-001A`.
- Canonical-name transition performed: `NO`.

## Backend
- Development backend: `Lovable Cloud enabled`.
- Custom database tables: `NONE`.
- RLS policies: `NONE`.
- Migrations initialized: `NO`.
- Demo seed/reset initialized: `NO`.

Never store credentials/secrets in this file.

## Accepted slices
None yet. `FOUND-001A` remains CONDITIONAL pending one final implementation correction.

## Verified starter / FOUND-001A baseline
- framework/build stack: `TanStack Start v1 + Vite`;
- React: `19.2.0`;
- package manager: `bun`;
- verified Bun runtime: `1.3.3`;
- `packageManager`: `bun@1.3.3`;
- Tailwind: `4.2.1` using `@tailwindcss/vite`;
- TypeScript: `5.8.3`;
- Vite: `8.2.0`;
- shadcn: already initialized (`new-york`, CSS variables, Lucide icon library, standard `src/components/ui/` aliases);
- primitive base: generated Radix-based starter; do not reinitialize shadcn blindly;
- TanStack Query already installed;
- React Hook Form + Zod already installed;
- Recharts already installed;
- routes remain starter-only;
- Re:Solve business functionality: none;
- PWA/tests/CI: not yet configured;
- database migrations/schema: none;
- `AGENTS.md` exists and no longer locks production to Cloudflare;
- root `.env.example` exists and contains only current foundation variables;
- root `.gitignore` now correctly contains `.env`, `.env.*`, `!.env.example`;
- formatter layer no longer hard-codes universal locale/currency defaults;
- UI provenance ledger is `docs/ui-sources.md` and correctly records `lucide-react@0.575.0`, source-owned shadcn registry components, granular Radix provenance, and Untitled UI/Tremor as not incorporated;
- `.bun-version` is `1.3.3` and aligns with package metadata;
- Lovable reported build/type/lint success, with only stock shadcn react-refresh warnings.

## Remaining FOUND-001A supervisor review finding
GitHub verification after FIX3 found only one remaining issue:
1. `getServerEnv` reverted to a manual `typeof window` runtime guard. This does not use TanStack Start's compiler-recognized server-only execution boundary. Use `createServerOnlyFn` from `@tanstack/react-start` (or an equivalent true server-only mechanism provided by the installed version) so the server implementation is removed/replaced in the client bundle and client-side invocation fails by design. Keep `createServerFn` for deliberate RPC endpoints, not for exposing a reusable private environment reader.

## Current architecture facts
- framework/build tool: `TanStack Start v1 + Vite`
- routing: `TanStack file-based routes`
- React: `19.2.0`
- package manager: `bun@1.3.3`
- Tailwind: `4.2.1`
- shadcn: `initialized; do not rerun init without explicit migration decision`
- current UI primitives: `Radix + shadcn source components`
- primary icon library: `Lucide 0.575.0`
- query/server state: `TanStack Query`
- form/validation: `React Hook Form + Zod`
- chart foundation: `Recharts`
- testing stack: `not configured`
- PWA tooling: `not configured`
- auth approach: `Lovable Cloud available; no Re:Solve auth/domain setup yet`
- service/repository boundaries: `initial directories established; acceptance pending one final environment-boundary correction`

## Current Core UI inventory
None beyond stock/generated shadcn primitives. No Re:Solve Core UI components accepted yet.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring a product decision. Current issue is an implementation correction only.

## Known implementation limitations
- private env reader still uses a manual runtime guard rather than a TanStack compiler-recognized server-only environment function;
- no CI/tests/PWA yet by design.

## Next action
Execute supervisor-provided final environment-boundary correction only. Re-review the actual repository afterward. Do not begin FOUND-001B until FOUND-001A passes.
