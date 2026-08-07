# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A CONDITIONAL — FOUNDATION CORRECTION REQUIRED BEFORE FOUND-001B**

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
None yet. `FOUND-001A` is currently CONDITIONAL pending focused corrections.

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
- initial environment, formatter and UI provenance files exist;
- Lovable reported `bun run build` success and `bun run lint` success with 6 existing react-refresh warnings.

## FOUND-001A supervisor review findings
The structural direction is acceptable, but the following must be corrected before acceptance:
1. `.env.example` was created under `src/`; it must live at repository root for the app/tooling convention.
2. `.gitignore` does not currently protect `.env` / `.env.*`; add safe env ignore rules while explicitly allowing `.env.example`.
3. `src/lib/env/index.ts` mixes server `process.env` and browser `import.meta.env` in one shared module; establish explicit server/client environment boundaries so server-only secrets cannot be imported into browser code by design.
4. `src/lib/formatters/index.ts` hard-codes `en-US` and `USD` as universal defaults, contradicting the Product Bible. Locale/currency must come from runtime/user/Operating Entity context or explicit caller input; no universal business currency.
5. `src/lib/UI-PROVENANCE.md` is not sufficiently auditable: replace vague `Latest compatible` wording with source URL, license and actual package/component provenance where known. Prefer a documentation location outside runtime library code, e.g. `docs/ui-sources.md`.
6. Package/runtime metadata claimed in the completion report was not found in `package.json`; record Bun/package-manager/runtime expectation explicitly in a portable way without creating conflicting lockfiles/tooling.
7. `AGENTS.md` currently states `Cloudflare Workers / Nitro` as the runtime. Keep runtime guidance factual to the generated TanStack/Nitro-compatible stack and avoid making Cloudflare a production requirement unless the repository configuration actually establishes that decision.

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
- service/repository boundaries: `initial directories established; acceptance pending focused cleanup`

## Current Core UI inventory
None beyond stock/generated shadcn primitives. No Re:Solve Core UI components accepted yet.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring a product decision. Current issues are implementation corrections.

## Known implementation limitations
- environment boundary/security hygiene needs correction;
- locale/currency defaults violate canonical rules;
- UI provenance needs stronger auditability;
- runtime/package-manager declaration needs correction;
- no CI/tests/PWA yet by design.

## Next action
Execute supervisor-provided `FOUND-001A-FIX` only. Re-review the actual repository afterward. Do not begin FOUND-001B until FOUND-001A passes.
