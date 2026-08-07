# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B CONDITIONAL — FINAL TOKEN/THEME COMPATIBILITY CLEANUP REQUIRED BEFORE VISUAL ACCEPTANCE**

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
**Status: CONDITIONAL — implementation cleanup required, then visual acceptance**

### Verified implementation now present
- Re:Solve-owned OKLCH semantic palette in `src/styles.css`;
- light/dark values for core surfaces, text, borders, actions, statuses, selected, disabled and 6 chart series;
- Fontsource dependencies for self-hosted Inter Variable and JetBrains Mono Variable (`@fontsource-variable/*`);
- no Google Fonts runtime links remain in root metadata;
- reusable `ThemeProvider` supports light/dark/system, localStorage persistence and live `prefers-color-scheme` updates;
- `/__dev/ui` has a production `beforeLoad` guard;
- root metadata now uses provisional Re:Solve strings rather than Lovable starter metadata;
- reduced-motion media handling exists;
- Untitled UI and Tremor provenance is correctly `NOT INCORPORATED — DESIGN REFERENCE ONLY`;
- build/lint/type success reported by Lovable.

### Remaining FOUND-001B supervisor findings
1. **Existing shadcn compatibility was partially broken by the token rewrite.** The generated `src/components/ui/sidebar.tsx` still consumes `bg-sidebar`, `text-sidebar-foreground`, `border-sidebar-border`, `ring-sidebar-ring` and related sidebar vocabulary. `src/styles.css` no longer defines the corresponding Tailwind/shadcn compatibility mappings. Restore these compatibility tokens by mapping them onto Re:Solve authority tokens; do not create a separate sidebar design system.
2. **shadcn chart compatibility is incomplete.** Re:Solve has `rs-chart-1..6`, but preserve/map the existing shadcn `chart-1..5` vocabulary so source-owned chart primitives remain usable without a parallel palette.
3. **Layout contract still incomplete.** The requested restrained elevation levels, mobile safe-area inset tokens, focus-offset token/treatment and explicit compact/default/touch density rhythm tokens are not yet present. Add these as contracts only; do not build shell/components yet.
4. **Initial theme flash remains.** `ThemeProvider` applies the stored/system theme in `useEffect`, after first render/hydration. Add a small pre-hydration theme bootstrap so stored dark/system-dark does not visibly flash light where practical in TanStack Start. Keep it portable and CSP-aware/documentable; do not build Appearance settings yet.
5. **Font CSS is imported twice.** Fontsource is imported both from `src/styles.css` and from `src/routes/__root.tsx`. Choose one canonical bundled import path and remove the duplicate.
6. **Font provenance still lacks package versions.** `docs/ui-sources.md` records package names/licenses but not version declarations/resolved versions. Record truthful package version provenance from the repository; do not invent values.
7. **Theme storage should validate persisted values.** Avoid trusting an arbitrary localStorage string as a `Theme`; invalid/corrupted values should fall back safely to `system`.

### Visual acceptance still required after code cleanup
Before FOUND-001B becomes ACCEPTED, supervisor will review actual `/__dev/ui` appearance in at least:
- light mode;
- dark mode;
- a narrow/mobile viewport.

The visual review will check hierarchy, density, palette restraint, focus visibility, status semantics, typography, long-content behavior and whether the foundation feels like a high-trust operations workspace rather than stock shadcn/generic SaaS.

## Current architecture facts
- framework/build tool: `TanStack Start v1 + Vite`
- routing: `TanStack file-based routes`
- React: `19.2.0`
- package manager: `bun@1.3.3`
- Tailwind: `4.2.1`
- shadcn: `initialized — new-york, CSS variables, source-owned registry components; do not rerun init without explicit migration decision`
- current primitive base: `Radix + shadcn source components`
- primary icon library: `Lucide 0.575.0`
- typography packages: `@fontsource-variable/inter`, `@fontsource-variable/jetbrains-mono` (version provenance cleanup pending)
- query/server state: `TanStack Query`
- form/validation: `React Hook Form + Zod`
- chart foundation: `Recharts`
- environment security: `public VITE boundary + createServerOnlyFn private boundary`
- testing stack: `not configured`
- PWA tooling: `not configured`
- auth approach: `Lovable Cloud available; no Re:Solve auth/domain setup yet`
- service/repository boundaries: `initial FOUND-001A boundaries established`

## Current Core UI inventory
No Re:Solve-owned reusable primitive/composite set is accepted yet. FOUND-001B token/theme foundation remains conditional. Full canonical primitives and Component Gallery breadth begin only after FOUND-001B acceptance.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision. Current FOUND-001B issues are implementation/acceptance corrections.

## Known implementation limitations
- shadcn sidebar/chart token compatibility needs restoration;
- elevation/safe-area/focus-offset/density contracts need completion;
- pre-hydration theme bootstrap is not yet established;
- Fontsource is imported twice and provenance versions are incomplete;
- no broad Component Gallery, shell, PWA, CI or test foundation yet by design.

## Next action
Execute supervisor-provided final `FOUND-001B-FIX2` implementation cleanup only. Re-review repository afterward, then perform visual acceptance of `/__dev/ui`. Do not begin FOUND-001C until FOUND-001B passes.
