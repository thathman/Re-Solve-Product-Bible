# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED + CLOSED — FOUND-001C1 CONDITIONAL**

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
- `beforeLoad` production redirect using `import.meta.env.PROD` is restored.
- Actual code blocks `/ui` in production builds and preserves the source for future Component Gallery work.
- Important runtime fact: the same guard previously blocked Lovable's embedded Preview because Lovable Preview evaluated production-like. Do not claim `/ui` is reliably accessible in Lovable Preview while this guard is active.
- Local/non-production development can use the route normally.
- Any future Lovable visual-review exposure must be an explicit supervised temporary step.

## FOUND-001C1 — Core UI primitive foundation + Component Gallery infrastructure
**Status: CONDITIONAL — correction required before C2**

### Verified implementation present
- Re:Solve-owned Core UI files now exist under `src/components/core/`;
- initial set includes Button, IconButton, Badge, StatusBadge, ResolveAvatar, Tooltip, Separator, Skeleton, Metric and MetricDelta;
- gallery source imports and demonstrates most new Core components;
- Button variants/sizes/loading/disabled examples exist;
- StatusBadge uses semantic status tokens and text labels;
- ResolveAvatar has image/fallback and xs–xl sizing;
- Metric/MetricDelta examples exist;
- no new dependencies were required;
- production `/ui` guard remains in place.

### Remaining C1 supervisor findings
1. **Core boundary leak:** `src/components/core/button/IconButton.tsx` imports stock `@/components/ui/tooltip` instead of the Re:Solve Core Tooltip that was created in this slice. Core components should consume Core components where the canonical pattern exists.
2. **Gallery evidence incomplete:** Core Tooltip is not demonstrated in the gallery, and Core Separator is imported but not actually rendered. Every C1 component needs representative gallery evidence before acceptance.
3. **Avatar accessible-name contract incomplete:** `ResolveAvatar` supports image alt text and visible fallback text, but fallback/initials-only states do not provide a reliable explicit full accessible name. `?` is not an acceptable identity label.
4. **Untitled UI provenance/material incorporation is not sufficiently traceable:** the ledger points to the Untitled homepage, describes the license vaguely as `Free/Open Version (Reference)`, and claims material incorporation from generic size/shape/pill patterns. Current official Untitled UI free/open-source React components are MIT licensed. Record an exact free component source/CLI target and adapt a specific identifiable Avatar or Badge behavior/API pattern into Re:Solve while preserving the current Radix foundation unless a dependency is truly required.
5. **Tremor Raw provenance/material incorporation is not sufficiently traceable:** the ledger points only to a broad components page, while `Metric`/`MetricDelta` contain only generic `Inspired by` comments. Tremor Raw is a copy-and-paste source model; adapt from an exact named/versioned Raw component source (for example the current Card source if appropriate), then document the exact source/component/version and Re:Solve modifications.
6. **MetricDelta conflates direction with sentiment:** current `up` always maps to success and `down` always maps to danger. A reusable operations primitive must separate movement direction from positive/negative/neutral meaning because lower can be good and higher can be bad.
7. **Loading/reduced-motion semantics need tightening:** Button loading should expose meaningful busy/loading semantics, and transform-based active feedback must honor the accepted reduced-motion contract.
8. **Gallery currency example should use explicit currency code:** avoid bare `$` in a canonical reusable gallery; use an explicit code such as `USD 42,850.00` or another clearly labeled fictional example.

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
- Radix: incorporated beneath current shadcn and Core components.
- Lucide: incorporated as primary icon family.
- Untitled UI React: C1 claims material incorporation, but supervisor acceptance is pending exact traceable source/license/adaptation evidence.
- Tremor Raw: C1 claims material incorporation, but supervisor acceptance is pending exact traceable source/version/adaptation evidence.

## Current Core UI inventory
C1 implementation exists but is not yet accepted. Do not treat these components as frozen/canonical until the C1 correction passes.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision.

## Known implementation limitations
- C1 Core ownership boundary needs one internal import correction;
- gallery coverage is incomplete for Tooltip/Separator;
- Avatar accessible naming needs correction;
- Untitled/Tremor material-source provenance needs to become exact/auditable;
- MetricDelta direction/sentiment semantics need correction;
- loading/reduced-motion semantics need tightening;
- shell, PWA, CI and test foundation remain future FOUND-001 substeps by design.

## Next action
Execute a narrowly scoped `FOUND-001C1-FIX` correction. Re-review repository and provenance afterward. Do not begin FOUND-001C2 until C1 passes.