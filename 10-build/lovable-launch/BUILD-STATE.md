# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED + CLOSED — FOUND-001C1 ACCEPTED — FOUND-001C2 READY**

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
- Legacy reference repository remains: `thathman/Re-Solve`.
- Product Bible repository is specification/reference only, not application source.
- Root `AGENTS.md`: accepted in FOUND-001A.
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

Accepted foundation includes TanStack Start v1 + React 19.2, Vite 8.2, TypeScript 5.8, Bun 1.3.3, Tailwind 4.2.1, preserved Radix-based shadcn source setup, environment/config boundaries, locale/currency-safe formatters, provenance ledger, portability guardrails and no business/domain implementation.

### FOUND-001B — UI Stack & Design Tokens
**Status: ACCEPTED + CLOSED**

Accepted foundation includes Re:Solve-owned semantic OKLCH tokens, light/dark/system theming, self-hosted Inter Variable + JetBrains Mono Variable, density/layout/elevation/focus/safe-area/motion contracts, accessible status/destructive semantics, chart tokens, shadcn compatibility mappings and visually approved responsive token preview.

### FOUND-001B closure
- Source route remains `src/routes/__dev/ui.tsx`; TanStack browser path is `/ui` because `__dev` is pathless.
- `beforeLoad` with `import.meta.env.PROD` blocks `/ui` in production builds.
- The same guard has previously blocked Lovable embedded Preview, so do not claim Preview access while the guard is active.
- Local/non-production development can use the route.

### FOUND-001C1 — Core UI primitive foundation + Component Gallery infrastructure
**Status: ACCEPTED — CANONICAL/FROZEN FOR DOWNSTREAM USE**

Supervisor verified on application-repository `main`:
- canonical Re:Solve Core boundary exists under `src/components/core/`;
- public export surface exists at `src/components/core/index.ts`;
- accepted C1 set: Button, IconButton, Badge, StatusBadge, ResolveAvatar, Tooltip, Separator, Skeleton, Metric and MetricDelta;
- Component Gallery consumes the public Core boundary rather than importing low-level source components directly;
- Button supports Re:Solve variants/sizing, disabled/loading behavior, `aria-busy`, decorative spinner semantics and motion-safe pressed feedback;
- IconButton requires an accessible label and consumes Core Tooltip;
- Core Tooltip remains Radix-backed and has pointer/keyboard/long-content gallery evidence;
- Separator supports horizontal/vertical use and is demonstrated;
- StatusBadge uses semantic color plus visible label/dot rather than color-only meaning;
- ResolveAvatar materially adapts documented Untitled UI Avatar behavior while retaining Radix underneath: initials fallback, placeholder behavior, size/shape composition and visible status indicators;
- ResolveAvatar uses a discriminated accessibility contract: meaningful avatars require `name`; decorative avatars explicitly use `decorative: true`;
- meaningful avatar root owns the single accessible identity and includes status in the label when supplied; image/fallback/status children are hidden from assistive technology;
- decorative avatars are removed from the accessibility tree;
- no ordinary `process.env` access remains in ResolveAvatar;
- Metric materially adapts Tremor Card v1.0.0 structural `relative w-full text-left` surface behavior while retaining a Re:Solve-owned API/tokens;
- Tremor source provenance is recorded as Apache-2.0;
- MetricDelta separates movement `direction` (`up|down|flat`) from semantic `sentiment` (`positive|negative|neutral`);
- gallery demonstrates direction/sentiment combinations and explicit currency codes;
- Untitled UI Avatar and Tremor Card provenance is auditable in `docs/ui-sources.md`;
- no new parallel design system, package manager or lockfile was introduced;
- Lovable reports build/lint/type success with only unrelated existing Fast Refresh warnings.

C1 APIs are now the canonical Re:Solve Core consumption path. Future slices should extend these components deliberately rather than bypassing them with duplicate source-library primitives.

## Current architecture facts
- framework/build tool: TanStack Start v1 + Vite;
- routing: TanStack file-based routes;
- React: 19.2.0;
- package manager: bun@1.3.3;
- Tailwind: 4.2.1;
- shadcn: initialized `new-york`, source-owned registry; do not rerun init;
- current primitive base: Radix + shadcn source components;
- primary icon family: Lucide 0.575.0;
- typography: Inter Variable + JetBrains Mono Variable via Fontsource 5.3.0;
- query/server state: TanStack Query;
- form/validation: React Hook Form + Zod already present;
- chart foundation: Recharts;
- environment security: public VITE boundary + createServerOnlyFn private boundary;
- testing stack: not configured;
- PWA tooling: not configured;
- auth/domain setup: not yet implemented.

## UI-source incorporation state
- shadcn/ui: incorporated/source-owned starter foundation.
- Radix: incorporated beneath current shadcn and Core components.
- Lucide: incorporated as primary icon family.
- Untitled UI React: materially incorporated through documented Avatar behavior/API adaptation; free/open-source source recorded in provenance ledger.
- Tremor Raw: materially incorporated through Tremor Card v1.0.0 structural adaptation into Re:Solve Metric; Apache-2.0 provenance recorded.

## Current Core UI inventory
Accepted/frozen C1:
- Button
- IconButton
- Badge
- StatusBadge
- ResolveAvatar
- Tooltip
- Separator
- Skeleton
- Metric
- MetricDelta

Next Core work should expand this inventory in bounded slices while preserving the public `@/components/core` boundary and accepted token/accessibility conventions.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision.

## Known implementation limitations
- form/control primitives are not yet canonical;
- overlay/menu/dialog primitives are not yet canonical;
- application states and broader composites remain future C substeps;
- shell, PWA, CI and test foundation remain future FOUND-001 substeps by design.

## Next action
Begin `FOUND-001C2` as a bounded form/control primitive slice. Build only the initial canonical field/control set plus Component Gallery evidence, preserve the accepted Core boundary, and STOP for supervisor review before overlays or additional primitive categories.