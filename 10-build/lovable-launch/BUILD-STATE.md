# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED + CLOSED — FOUND-001C READY**

## Canonical Product Bible state
- Repository: `thathman/Re-Solve-Product-Bible`.
- Visibility: `public`.
- Product Bible planning/expansion/launch-readiness content is canonical on `main`.
- First umbrella build slice: `FOUND-001 — Re:Solve Application + Core UI Foundation`.
- FOUND-001 is supervised through bounded substeps.

## Lovable project
- Project: `Re:Solve`.
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
- Root `AGENTS.md`: `YES — accepted in FOUND-001A`.
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

Supervisor-verified foundation includes:
- TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8;
- Bun `1.3.3` as the single package manager/runtime declaration with one Bun lockfile;
- Tailwind CSS 4.2.1;
- existing shadcn `new-york` source-owned registry preserved; no re-init or base migration;
- current primitive base remains Radix + shadcn;
- TanStack Query, React Hook Form, Zod and Recharts present;
- root `AGENTS.md` established;
- safe `.env.example` and root env ignore rules established;
- public/private environment boundary uses Zod + TanStack `createServerOnlyFn`;
- locale/currency formatters do not impose a universal locale/currency;
- UI provenance ledger at `docs/ui-sources.md`;
- runtime remains portable/TanStack-Nitro compatible and not Cloudflare-locked.

### FOUND-001B — UI Stack & Design Tokens
**Status: ACCEPTED + CLOSED**

Supervisor verified implementation and visuals across light desktop, dark desktop and narrow/mobile.

Accepted foundation includes:
- Re:Solve-owned OKLCH semantic palette;
- light/dark semantic surfaces, text, borders, primary/destructive actions, selected/disabled states, semantic statuses and six chart series;
- destructive action semantics separated from soft danger-status semantics;
- shadcn destructive/sidebar/chart compatibility mapped to Re:Solve authority tokens;
- gutters, content measures, panel padding, compact/default/touch heights, density rhythm, restrained elevation, future shell reservations, focus contracts and safe-area contracts;
- Inter Variable + JetBrains Mono Variable self-hosted through Fontsource 5.3.0 with one import path;
- no Google Fonts runtime dependency;
- shared theme contract using `rs-theme`, validation, resolution and pre-hydration bootstrap generation;
- ThemeProvider uses shared resolver and supports live system-theme updates;
- reduced-motion handling;
- accessible semantic status foregrounds;
- six chart series rendered correctly via static classes;
- light/dark/system controls with accessible names/pressed state;
- responsive Actions & Status composition accepted;
- visual direction accepted as restrained, high-trust and Re:Solve-owned rather than stock shadcn/generic SaaS.

### FOUND-001B closure — 2026-08-07
- Source route remains `src/routes/__dev/ui.tsx` with generated browser path `/ui` because `__dev` is pathless in TanStack Router.
- `beforeLoad` production redirect using `import.meta.env.PROD` has been restored.
- Actual code therefore blocks `/ui` in production builds and preserves the source for future Component Gallery work.
- Important runtime fact: the same guard previously blocked Lovable's embedded Preview because Lovable Preview evaluated production-like. Do not claim `/ui` is reliably accessible in Lovable Preview while this guard is active.
- Local/non-production development can use the route normally.
- Any future Lovable visual-review exposure must be an explicit supervised temporary step rather than relying on an incorrect Preview-vs-production assumption.

## Current architecture facts
- framework/build tool: `TanStack Start v1 + Vite`;
- routing: `TanStack file-based routes`;
- React: `19.2.0`;
- package manager: `bun@1.3.3`;
- Tailwind: `4.2.1`;
- shadcn: `initialized — new-york, CSS variables, source-owned registry; do not rerun init`;
- current primitive base: `Radix + shadcn source components`;
- primary icon library: `Lucide 0.575.0`;
- typography: `Inter Variable + JetBrains Mono Variable via Fontsource 5.3.0`;
- query/server state: `TanStack Query`;
- form/validation: `React Hook Form + Zod`;
- chart foundation: `Recharts`;
- environment security: `public VITE boundary + createServerOnlyFn private boundary`;
- testing stack: `not configured`;
- PWA tooling: `not configured`;
- auth/domain setup: `not yet implemented`.

## UI-source incorporation state
- shadcn/ui: incorporated/source-owned starter foundation.
- Radix: incorporated beneath current shadcn components.
- Lucide: incorporated as primary icon family.
- Untitled UI React: `NOT INCORPORATED — DESIGN REFERENCE ONLY` as of end FOUND-001B.
- Tremor: `NOT INCORPORATED — DESIGN REFERENCE ONLY` as of end FOUND-001B.
- FOUND-001C must begin material, deliberate incorporation without creating parallel component systems.

## Current Core UI inventory
No Re:Solve-owned reusable Core UI primitive/composite set is accepted yet. FOUND-001B supplies the accepted token/theme/typography foundation. FOUND-001C now begins canonical Re:Solve Core UI components and the Component Gallery.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision.

## Known implementation limitations
- broad Core UI components are not yet accepted;
- Component Gallery is still only the token-preview foundation;
- Untitled UI and Tremor are not yet materially incorporated;
- shell, PWA, CI and test foundation remain future FOUND-001 substeps by design.

## Next action
Begin `FOUND-001C` as bounded substeps. First build a small canonical primitive set plus Component Gallery infrastructure, materially incorporate carefully selected Untitled UI and Tremor Raw patterns, verify source provenance/accessibility/responsiveness, then STOP for supervisor review before expanding the primitive set.