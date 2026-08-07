# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B CONDITIONAL — UI FOUNDATION CORRECTIONS REQUIRED BEFORE FOUND-001C**

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
- Root `AGENTS.md`: `YES — created and accepted in FOUND-001A`.
- Canonical-name transition performed: `NO`.

## Backend
- Development backend: `Lovable Cloud enabled`.
- Custom database tables: `NONE`.
- RLS policies: `NONE`.
- Migrations initialized: `NO`.
- Demo seed/reset initialized: `NO`.

Never store credentials/secrets in this file.

## Accepted slices
### FOUND-001A — Stack & Repository Foundation
**Status: ACCEPTED**

Supervisor verified on application-repository `main`:
- TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8;
- Bun `1.3.3` is the single package manager/runtime declaration, with `packageManager: bun@1.3.3` and one Bun lockfile;
- Tailwind CSS 4.2.1 using `@tailwindcss/vite`;
- existing shadcn `new-york` source-owned registry setup preserved; no re-initialization or base migration;
- current primitive foundation remains Radix-based;
- TanStack Query, React Hook Form, Zod and Recharts already present;
- root `AGENTS.md` established;
- root `.env.example` contains only current foundation variables;
- root `.gitignore` protects `.env` / `.env.*` while allowing `.env.example`;
- public/server environment boundary established with Zod and TanStack `createServerOnlyFn`; `process.env` access is contained inside the server-only function;
- locale/currency formatting utilities do not impose a universal locale or currency;
- UI-source provenance ledger lives at `docs/ui-sources.md`;
- production runtime remains portable/TanStack-Nitro compatible and is not locked to Cloudflare;
- no product modules, database schema, PWA, CI or broad UI shell were introduced in this slice.

## FOUND-001B — UI Stack & Design Tokens
**Status: CONDITIONAL**

Implemented direction verified:
- Re:Solve-owned OKLCH token naming has begun in `src/styles.css`;
- stock shadcn semantic variables are being mapped to Re:Solve authority tokens;
- provisional light/dark palette exists;
- Inter + JetBrains Mono typography intent is present;
- development token-preview route exists at `/__dev/ui`;
- no new UI dependency was added;
- existing Radix/shadcn foundation remains intact;
- build/lint/type were reported successful.

### FOUND-001B supervisor correction findings
1. **Remote font runtime dependency:** `src/routes/__root.tsx` loads Inter and JetBrains Mono from `fonts.googleapis.com` / `fonts.gstatic.com`. This contradicts the slice requirement that introduced fonts not require a third-party runtime font request. Self-host now through a portable bundled/source-controlled approach, or remove the remote font usage and use a local/system stack until self-hosting is implemented.
2. **Theme infrastructure incomplete:** `/__dev/ui` stores theme only in React state, does not persist the non-sensitive preference, and `system` mode reads the OS preference only when the effect runs; it does not subscribe to later OS theme changes. Establish a small reusable light/dark/system theme utility/provider with local preference persistence and `matchMedia` change handling. Avoid a flash of the wrong theme where practical for the current foundation.
3. **Development route not actually development-only:** `/__dev/ui` is always registered and currently has no environment guard. Ensure production access is prevented/disabled in a portable way while preserving the dev QA route.
4. **Incorrect provenance wording:** Untitled UI and Tremor have influenced design only; no code has been copied/installed. Record them as `NOT INCORPORATED — DESIGN REFERENCE ONLY`, not `PARTIALLY INCORPORATED`.
5. **Reduced motion incomplete:** token preview demonstrates transform/shadow/opacity motion without explicit `prefers-reduced-motion` handling. Add a global/reusable reduced-motion treatment and make the preview honor it.
6. **Required semantic token gaps:** add explicit tokens for selected state, disabled state, focus treatment as a complete contract, and chart/data-visualization series. Keep status semantics label-driven, not color-only.
7. **Required layout/density token gaps:** establish reusable tokens for page gutters, content measures, panel padding, compact/default/touch control heights, density rhythm, reserved future shell dimensions, responsive/safe-area behavior and restrained elevation. Do not build the shell itself.
8. **Preview coverage:** update `/__dev/ui` to visibly demonstrate warning/critical/selected/disabled/focus/chart-series states, density/control-height tokens, reduced-motion behavior, and locale-neutral representative numeric data. Do not imply USD is universal product truth.
9. **Root metadata cleanup:** since `__root.tsx` is already being touched for font/theme foundation, remove remaining generic `Lovable App` / `Lovable Generated Project` / `@Lovable` metadata and replace it with provisional Re:Solve metadata. Do not invent final marketing copy.

## Current architecture facts
- framework/build tool: `TanStack Start v1 + Vite`
- routing: `TanStack file-based routes`
- React: `19.2.0`
- package manager: `bun@1.3.3`
- Tailwind: `4.2.1`
- shadcn: `initialized — new-york, CSS variables, source-owned registry components; do not rerun init without explicit migration decision`
- current primitive base: `Radix + shadcn source components`
- primary icon library: `Lucide 0.575.0`
- query/server state: `TanStack Query`
- form/validation: `React Hook Form + Zod`
- chart foundation: `Recharts`
- environment security: `public VITE boundary + createServerOnlyFn private boundary`
- testing stack: `not configured`
- PWA tooling: `not configured`
- auth approach: `Lovable Cloud available; no Re:Solve auth/domain setup yet`
- service/repository boundaries: `initial FOUND-001A boundaries established`

## Current Core UI inventory
No Re:Solve-owned reusable primitive/composite set is accepted yet. FOUND-001B token/theme foundation is under correction. Full canonical primitives and Component Gallery breadth begin only after FOUND-001B acceptance.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision. Current FOUND-001B issues are implementation/acceptance corrections.

## Known implementation limitations
- remote Google Fonts runtime dependency exists;
- light/dark/system theme behavior is not yet persistent/reactive enough;
- dev preview route is not yet production-blocked;
- reduced-motion treatment is incomplete;
- semantic/layout/density token contracts are incomplete;
- Untitled UI/Tremor provenance overstates incorporation;
- no broad Component Gallery, shell, PWA, CI or test foundation yet by design.

## Next action
Execute the supervisor-provided focused `FOUND-001B-FIX` only. Re-review actual repository and preview afterward. Do not begin FOUND-001C until FOUND-001B passes.
