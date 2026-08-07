# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B IMPLEMENTATION PASS — VISUAL CONDITIONAL — FINAL PREVIEW CORRECTION REQUIRED BEFORE FOUND-001C**

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
- production runtime remains portable/TanStack-Nitro compatible and is not locked to Cloudflare;
- no product modules, database schema, PWA, CI or broad UI shell were introduced in this slice.

## FOUND-001B — UI Stack & Design Tokens
**Status: IMPLEMENTATION PASS — VISUAL CONDITIONAL**

### Supervisor-verified implementation
- Re:Solve-owned OKLCH semantic palette in `src/styles.css`;
- intentional light/dark values for core surfaces, text, borders, primary actions, destructive actions, selected/disabled states, semantic statuses and six chart series;
- destructive action semantics are separate from soft danger-status semantics;
- shadcn `destructive` / `destructive-foreground` map to Re:Solve destructive-action tokens;
- shadcn sidebar compatibility vocabulary maps onto Re:Solve authority tokens;
- shadcn `chart-1..5` vocabulary maps onto Re:Solve chart tokens while Re:Solve retains series 6;
- page gutters, content measures, panel padding, compact/default/touch heights, density rhythm, restrained elevation, future shell reservations, focus contracts and safe-area contracts exist;
- Inter Variable and JetBrains Mono Variable are self-hosted through Fontsource and imported through a single application path;
- no Google Fonts runtime links remain;
- `src/lib/theme/contract.ts` is the shared theme contract with `rs-theme`, validation, resolver and bootstrap generation;
- runtime `ThemeProvider` uses the shared `resolveTheme()` contract and preserves live system-theme updates;
- root shell runs the generated pre-hydration theme bootstrap;
- reduced-motion handling exists;
- semantic status surfaces use explicit accessible foreground tokens rather than one universal inverse foreground;
- focus offset has an explicit Re:Solve token;
- Untitled UI and Tremor remain `NOT INCORPORATED — DESIGN REFERENCE ONLY`;
- Fontsource provenance records declared `^5.3.0` and resolved `5.3.0` versions;
- Lovable reports build, lint and type-check success, with only standard Fast Refresh warnings.

### Development preview routing fact
- Source route id/file: `src/routes/__dev/ui.tsx` / `/__dev/ui`.
- TanStack generated browser path: `/ui` because `__dev` is pathless in the generated route tree.
- Lovable Preview evaluates the prior production guard as production-like, so the route guard was temporarily removed for visual acceptance.
- `/ui` must be re-secured or removed from production access after visual acceptance is complete.

### Visual review — 2026-08-07
Supervisor reviewed light desktop, dark desktop and narrow/mobile captures.

**Direction approved:**
- light/dark hierarchy is coherent and restrained;
- operational typography reads clearly;
- semantic surfaces and selected/disabled distinction are legible;
- primary/destructive/status semantics are visually distinguishable;
- density/elevation treatment is restrained rather than card-heavy;
- narrow/mobile layout fundamentally reflows without horizontal overflow;
- overall foundation feels materially more like a high-trust operations workspace than a stock starter.

**Final visual-gate findings:**
1. **Chart-series swatches are not visually showing six distinct series colors.** In both light and dark captures the six Data Visualization cards appear effectively neutral/surface-colored. The preview currently constructs `bg-rs-chart-${i}` dynamically, which is not a reliable Tailwind static class source. Render the six chart swatches from an explicit static class map or another token-safe implementation so all six actual colors are visible.
2. **Theme toggle accessibility:** icon-only light/dark/system buttons need accessible names and selected/pressed state (`aria-label`, `aria-pressed` or equivalent) while preserving the compact visual treatment.
3. **Narrow Actions & Status density:** the two-column grid at the captured mobile width forces token identifiers into cramped wrapping. Use one column at the narrowest width, then two columns when space permits, without changing desktop composition.
4. **Temporary preview exposure:** keep `/ui` available only long enough to verify the final visual correction, then restore an appropriate production-safe guard/removal strategy after FOUND-001B is accepted.

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
No Re:Solve-owned reusable primitive/composite set is accepted yet. FOUND-001B implementation has passed code review, but visual acceptance remains conditional on the small preview corrections above. Full canonical primitives and Component Gallery breadth begin only after FOUND-001B acceptance.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision.

## Known implementation limitations
- chart-series preview colors are not rendering distinctly;
- theme toggle accessible names/selection semantics need correction;
- narrow mobile Actions & Status density needs one small responsive adjustment;
- `/ui` is temporarily exposed for Lovable visual review and must be re-secured after acceptance;
- no broad Component Gallery, shell, PWA, CI or test foundation yet by design.

## Next action
Execute the supervisor-provided final FOUND-001B visual-gate correction only. Re-review the corrected `/ui` preview, then either accept FOUND-001B or issue one narrowly scoped visual correction. Do not begin FOUND-001C until FOUND-001B passes.
