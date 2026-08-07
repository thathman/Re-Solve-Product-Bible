# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED + CLOSED — FOUND-001C1 CONDITIONAL (FINAL AVATAR ENV/ACCESSIBILITY CLEANUP)**

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

## FOUND-001C1 — Core UI primitive foundation + Component Gallery infrastructure
**Status: CONDITIONAL — one final Avatar correction required before C2**

### Verified C1 implementation now present
- canonical Re:Solve Core boundary exists under `src/components/core/`;
- public export surface exists at `src/components/core/index.ts`;
- C1 set exists: Button, IconButton, Badge, StatusBadge, ResolveAvatar, Tooltip, Separator, Skeleton, Metric and MetricDelta;
- Component Gallery imports through `@/components/core`;
- IconButton consumes Core Tooltip rather than stock shadcn Tooltip;
- Tooltip and Separator have explicit gallery examples;
- Button loading exposes `aria-busy`, disables interaction, uses a decorative spinner, and active scaling is motion-safe;
- MetricDelta separates `direction` (`up|down|flat`) from `sentiment` (`positive|negative|neutral`);
- gallery demonstrates positive/negative/neutral combinations and uses explicit currency codes;
- Untitled UI Avatar behavior is materially adapted: initials, placeholder icon, status indicator and normalized size/shape behavior while retaining Radix Avatar underneath;
- Tremor Card provenance is corrected to Card v1.0.0 / Apache-2.0 and Metric now carries the traceable `relative w-full text-left` structural surface contract;
- standalone Tooltip keyboard example no longer nests an IconButton-owned Tooltip;
- no new dependencies were added;
- production `/ui` guard remains in place;
- Lovable reports build/lint/type success.

### Remaining C1 supervisor finding after FIX2
1. **ResolveAvatar reintroduced shared-module `process.env` access.** `src/components/core/avatar/ResolveAvatar.tsx` currently checks `process.env.NODE_ENV` inside a client/shared UI component. This violates the environment-boundary rule accepted in FOUND-001A. Remove all ordinary `process.env` access from the component.
2. **Meaningful-vs-decorative naming should be enforced structurally, not by a development warning.** Prefer a TypeScript discriminated-union API where meaningful avatars require a full `name` and decorative avatars explicitly opt into `decorative: true`. Avoid a runtime warning as the primary enforcement mechanism.
3. **Unify status with the single accessible avatar identity.** Meaningful avatars should expose one coherent accessible name such as the person's full name plus meaningful status when status is supplied. The visual status dot should then be `aria-hidden`. Avoid a separate `sr-only` status node that may be announced independently from the image identity.
4. **Preserve the accepted visual status treatment.** Current high-contrast indicator colors and surface ring are acceptable; do not regress them while fixing semantics.

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
- form/validation: React Hook Form + Zod;
- chart foundation: Recharts;
- environment security: public VITE boundary + createServerOnlyFn private boundary;
- testing stack: not configured;
- PWA tooling: not configured;
- auth/domain setup: not yet implemented.

## UI-source incorporation state
- shadcn/ui: incorporated/source-owned starter foundation.
- Radix: incorporated beneath current shadcn and Core components.
- Lucide: incorporated as primary icon family.
- Untitled UI React: material Avatar behavior adaptation is present; final C1 acceptance depends only on the remaining Avatar env/accessibility cleanup.
- Tremor Raw: material incorporation accepted in principle for C1 after provenance correction to Card v1.0.0 / Apache-2.0 and traceable Metric structural adaptation.

## Current Core UI inventory
C1 implementation exists but is not yet frozen/canonical. Do not begin C2 until the final Avatar correction passes.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision.

## Known implementation limitations
- final ResolveAvatar env/accessibility cleanup pending;
- shell, PWA, CI and test foundation remain future FOUND-001 substeps by design.

## Next action
Execute supervisor-provided final FOUND-001C1 Avatar correction only. Re-review repository afterward. If accepted, freeze C1 as canonical and proceed to the next bounded C2 primitive set.