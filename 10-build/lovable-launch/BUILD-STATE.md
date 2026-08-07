# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B CONDITIONAL — FINAL THEME/FONT/ACCESSIBILITY CLEANUP + VISUAL ACCEPTANCE REQUIRED BEFORE FOUND-001C**

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
**Status: CONDITIONAL — final implementation cleanup required, then visual acceptance**

### Verified implementation now present
- Re:Solve-owned OKLCH semantic palette in `src/styles.css`;
- light/dark values for core surfaces, text, borders, actions, statuses, selected, disabled and 6 Re:Solve chart series;
- shadcn sidebar compatibility vocabulary restored and mapped onto Re:Solve authority tokens;
- shadcn chart `chart-1..5` compatibility restored and mapped onto Re:Solve chart tokens;
- page gutter, content measure, panel padding, compact/default/touch control height, density rhythm, restrained elevation, shell reservation and safe-area contracts now exist;
- self-hosted Fontsource dependencies are installed for Inter Variable and JetBrains Mono Variable;
- no Google Fonts runtime links remain;
- reusable `ThemeProvider` supports light/dark/system, localStorage persistence and live `prefers-color-scheme` updates after hydration;
- root shell contains a pre-hydration theme bootstrap attempt;
- `/__dev/ui` has a production `beforeLoad` guard;
- root metadata uses provisional Re:Solve strings rather than Lovable starter metadata;
- reduced-motion media handling exists;
- Untitled UI and Tremor provenance is correctly `NOT INCORPORATED — DESIGN REFERENCE ONLY`;
- font provenance records declared `^5.3.0` ranges;
- build/lint/type success reported by Lovable.

### Remaining FOUND-001B supervisor findings after FIX2
1. **Pre-hydration `system` logic is wrong and storage validation is duplicated.** `src/routes/__root.tsx` currently treats OS dark mode only when there is no stored value. A valid stored value of `system` therefore resolves light even when the OS is dark until hydration. Invalid non-empty stored values also resolve as light rather than falling back to `system`. The bootstrap hard-codes the storage key/validation separately from `ThemeProvider`, directly creating the drift the previous correction was intended to prevent. Establish one shared theme storage key/validation/resolution contract usable by both bootstrap generation and runtime provider logic.
2. **Fontsource CSS is still imported twice.** `src/styles.css` imports both Fontsource packages and `src/routes/__root.tsx` imports the same packages again. Keep exactly one canonical import path.
3. **Focus-offset contract is incomplete.** Focus ring width/color and offset width exist, but there is no explicit Re:Solve focus-offset color/surface token. Add one and use it in the preview/canonical focus treatment rather than implicitly hard-wiring canvas as the offset surface.
4. **Status foreground accessibility is not established.** `/__dev/ui` uses `text-rs-text-inverse` on every status-color icon block. With the current bright light-mode success/warning tokens, a single inverse foreground is not a safe universal contrast treatment. Define/use accessible status foreground or soft-status treatment so information/success/warning/danger/critical states remain legible and WCAG-safe; do not rely on one foreground color for every status background.
5. **Preview dropped Re:Solve chart series 6.** The token exists and should remain visibly represented in the foundation preview even though shadcn compatibility only requires chart 1–5.
6. **Font provenance should record resolved versions when available from `bun.lock`.** Keep the declared range and add the truthful lockfile-resolved version rather than implying the range is the installed version.

### Visual acceptance still required after code cleanup
Before FOUND-001B becomes ACCEPTED, supervisor will review actual `/__dev/ui` appearance in at least:
- light desktop;
- dark desktop;
- a narrow/mobile viewport.

The visual review will check hierarchy, density, palette restraint, focus visibility, status semantics, typography, long-content behavior, responsive composition and whether the foundation feels like a high-trust operations workspace rather than stock shadcn/generic SaaS.

## Current architecture facts
- framework/build tool: `TanStack Start v1 + Vite`
- routing: `TanStack file-based routes`
- React: `19.2.0`
- package manager: `bun@1.3.3`
- Tailwind: `4.2.1`
- shadcn: `initialized — new-york, CSS variables, source-owned registry components; do not rerun init without explicit migration decision`
- current primitive base: `Radix + shadcn source components`
- primary icon library: `Lucide 0.575.0`
- typography packages: `@fontsource-variable/inter`, `@fontsource-variable/jetbrains-mono`;
- query/server state: `TanStack Query`
- form/validation: `React Hook Form + Zod`
- chart foundation: `Recharts`
- environment security: `public VITE boundary + createServerOnlyFn private boundary`
- testing stack: `not configured`
- PWA tooling: `not configured`
- auth approach: `Lovable Cloud available; no Re:Solve auth/domain setup yet`
- service/repository boundaries: `initial FOUND-001A boundaries established`.

## Current Core UI inventory
No Re:Solve-owned reusable primitive/composite set is accepted yet. FOUND-001B token/theme foundation remains conditional. Full canonical primitives and Component Gallery breadth begin only after FOUND-001B acceptance.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision. Current FOUND-001B issues are implementation/acceptance corrections.

## Known implementation limitations
- pre-hydration theme bootstrap disagrees with runtime theme behavior for stored `system`/invalid values;
- Fontsource CSS remains imported twice;
- focus offset/status foreground contracts need final accessibility cleanup;
- visual acceptance screenshots are still pending;
- no broad Component Gallery, shell, PWA, CI or test foundation yet by design.

## Next action
Execute supervisor-provided final FOUND-001B implementation correction only. Re-review repository afterward, then perform visual acceptance of `/__dev/ui`. Do not begin FOUND-001C until FOUND-001B passes.
