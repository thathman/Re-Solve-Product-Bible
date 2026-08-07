# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A CONDITIONAL — FINAL FOUNDATION CLEANUP REQUIRED BEFORE FOUND-001B**

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
None yet. `FOUND-001A` remains CONDITIONAL pending one final focused cleanup.

## Verified starter / FOUND-001A baseline
- framework/build stack: `TanStack Start v1 + Vite`;
- React: `19.2.0`;
- package manager: `bun`;
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
- `AGENTS.md` exists;
- root `.env.example` now exists;
- formatter layer no longer hard-codes universal locale/currency defaults;
- UI provenance ledger moved to `docs/ui-sources.md`;
- `.bun-version` exists;
- Lovable reported `bun run build` success and `bun run lint` success with 6 existing react-refresh warnings.

## Remaining FOUND-001A supervisor review findings
Most earlier findings were corrected, but GitHub verification found these remaining issues:
1. `.gitignore` is unchanged and still does not ignore `.env` / `.env.*`; this must be committed, with `.env.example` explicitly allowed.
2. The current env module uses a manual `typeof window` guard in shared code. For TanStack Start, server-only environment access should use the framework's server-only execution boundary such as `createServerOnlyFn` / `createServerFn`, and server env should be read in server-only/per-request execution. Avoid shared-module secret access that can drift into client bundles.
3. Root `.env.example` still contains speculative future provider variables (`CHATWOOT_WEBHOOK_SECRET`, `STRIPE_SECRET_KEY`) despite the instruction not to invent future provider variables. Remove them until a real slice introduces them.
4. `docs/ui-sources.md` contains incorrect Lucide version provenance (`^0.475.0`), while `package.json` currently has `^0.575.0`. Correct provenance from the actual repository. For source-owned shadcn registry components, do not invent a singular package version when none exists.
5. Bun metadata is inconsistent: `.bun-version` currently contains `1.3.3`, while Lovable reported `1.2.2`. Verify with `bun --version` in the actual build environment and then align `.bun-version` and any package/runtime declaration to that verified value. Do not guess.

## Current architecture facts
- framework/build tool: `TanStack Start v1 + Vite`
- routing: `TanStack file-based routes`
- React: `19.2.0`
- package manager: `bun`
- Tailwind: `4.2.1`
- shadcn: `initialized; do not rerun init without explicit migration decision`
- current UI primitives: `Radix + shadcn source components`
- primary icon library: `Lucide`
- query/server state: `TanStack Query`
- form/validation: `React Hook Form + Zod`
- chart foundation: `Recharts`
- testing stack: `not configured`
- PWA tooling: `not configured`
- auth approach: `Lovable Cloud available; no Re:Solve auth/domain setup yet`
- service/repository boundaries: `initial directories established; acceptance pending final cleanup`

## Current Core UI inventory
None beyond stock/generated shadcn primitives. No Re:Solve Core UI components accepted yet.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring a product decision. Current issues are implementation corrections.

## Known implementation limitations
- `.gitignore` env protection still not committed;
- server-only env boundary needs a TanStack-native implementation;
- speculative env examples remain;
- UI provenance contains a version mismatch;
- Bun runtime metadata is inconsistent;
- no CI/tests/PWA yet by design.

## Next action
Execute supervisor-provided final `FOUND-001A-FIX2` only. Re-review the actual repository afterward. Do not begin FOUND-001B until FOUND-001A passes.
