# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED — PREVIEW ROUTE RE-SECURE REQUIRED BEFORE FOUND-001C**

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
- current runtime remains portable/TanStack-Nitro compatible and is not locked to Cloudflare;
- no product modules, database schema, PWA, CI or broad UI shell were introduced in this slice.

### FOUND-001B — UI Stack & Design Tokens
**Status: ACCEPTED**

Supervisor verified implementation and visual behavior across light desktop, dark desktop and narrow/mobile captures.

Accepted foundation includes:
- Re:Solve-owned OKLCH semantic palette in `src/styles.css`;
- intentional light/dark values for core surfaces, text, borders, primary actions, destructive actions, selected/disabled states, semantic statuses and six chart series;
- destructive-action semantics separated from soft danger-status semantics;
- shadcn destructive/sidebar/chart compatibility mapped onto Re:Solve authority tokens;
- page gutters, content measures, panel padding, compact/default/touch heights, density rhythm, restrained elevation, future shell reservations, focus contracts and safe-area contracts;
- Inter Variable and JetBrains Mono Variable self-hosted through Fontsource, imported through one application path;
- no Google Fonts runtime dependency;
- shared theme contract at `src/lib/theme/contract.ts` using storage key `rs-theme`, validation, resolver and pre-hydration bootstrap generation;
- runtime `ThemeProvider` uses the shared resolver and preserves live system-theme updates;
- reduced-motion handling;
- explicit accessible foregrounds for semantic status surfaces;
- explicit focus-offset token;
- six chart-series tokens rendered correctly via static classes in the dev preview;
- light/dark/system controls with visible selected state and accessibility semantics;
- narrow/mobile Actions & Status layout corrected to one column at the narrowest width and wider compositions retained;
- Untitled UI and Tremor remain `NOT INCORPORATED — DESIGN REFERENCE ONLY`;
- Fontsource provenance records declared `^5.3.0` and resolved `5.3.0` versions;
- Lovable reports build/lint/type success with only standard Fast Refresh warnings.

### FOUND-001B visual acceptance — 2026-08-07
Supervisor approved:
- hierarchy and typography;
- restrained high-trust operational tone;
- light/dark coherence;
- semantic surface distinctions;
- status/destructive distinction;
- density/elevation/radius discipline;
- responsive narrow/mobile composition;
- six distinct chart-series colors in both themes;
- overall Re:Solve-owned direction rather than stock shadcn/generic SaaS.

## Development preview routing fact
- Source route/file id: `src/routes/__dev/ui.tsx` / `/__dev/ui`.
- TanStack generated browser path: `/ui` because `__dev` is pathless in the generated route tree.
- Lovable Preview evaluates the former `import.meta.env.PROD` guard as production-like, so the guard was temporarily removed for visual review.
- The `/ui` review surface is accepted as a development artifact but must now be re-secured or made unavailable in actual production before FOUND-001C begins.

## Current architecture facts
- framework/build tool: `TanStack Start v1 + Vite`;
- routing: `TanStack file-based routes`;
- React: `19.2.0`;
- package manager: `bun@1.3.3`;
- Tailwind: `4.2.1`;
- shadcn: `initialized — new-york, CSS variables, source-owned registry components; do not rerun init without explicit migration decision`;
- current primitive base: `Radix + shadcn source components`;
- primary icon library: `Lucide 0.575.0`;
- typography: `Inter Variable + JetBrains Mono Variable via Fontsource 5.3.0`;
- query/server state: `TanStack Query`;
- form/validation: `React Hook Form + Zod`;
- chart foundation: `Recharts`;
- environment security: `public VITE boundary + createServerOnlyFn private boundary`;
- testing stack: `not configured`;
- PWA tooling: `not configured`;
- auth approach: `Lovable Cloud available; no Re:Solve auth/domain setup yet`;
- service/repository boundaries: `initial FOUND-001A boundaries established`.

## Current Core UI inventory
No Re:Solve-owned reusable primitive/composite set is accepted yet. FOUND-001B provides the accepted token/theme/typography foundation on which FOUND-001C will build canonical Re:Solve Core UI primitives and the Component Gallery.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision.

## Known implementation limitations
- `/ui` is temporarily exposed for Lovable visual review and must be re-secured before FOUND-001C;
- no broad Component Gallery, shell, PWA, CI or test foundation yet by design.

## Next action
Execute the supervisor-provided `FOUND-001B-CLOSE — Re-secure UI review surface` only. Verify actual production-safe behavior without breaking Lovable development review conventions. Then begin `FOUND-001C — Core UI Primitives + Component Gallery` only after supervisor acceptance of that closure step.
