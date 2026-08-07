# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED + CLOSED — FOUND-001C1 CONDITIONAL (FINAL PROVENANCE/AVATAR CLEANUP)**

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
**Status: CONDITIONAL — final correction required before C2**

### Verified C1 implementation now present
- canonical Re:Solve Core boundary exists under `src/components/core/`;
- public export surface exists at `src/components/core/index.ts`;
- C1 set exists: Button, IconButton, Badge, StatusBadge, ResolveAvatar, Tooltip, Separator, Skeleton, Metric and MetricDelta;
- Component Gallery imports through `@/components/core`;
- IconButton now consumes Core Tooltip rather than stock shadcn Tooltip;
- Tooltip and Separator now have explicit gallery examples;
- Button loading exposes `aria-busy`, disables interaction, uses a decorative spinner, and active scaling is motion-safe;
- MetricDelta now separates `direction` (`up|down|flat`) from `sentiment` (`positive|negative|neutral`);
- gallery demonstrates positive/negative/neutral combinations and uses explicit currency codes;
- Untitled Avatar behavior has been materially adapted: initials, placeholder icon, status indicator and normalized size/shape behavior while retaining Radix Avatar underneath;
- no new dependencies were added;
- production `/ui` guard remains in place;
- Lovable reports build/lint/type success.

### Remaining C1 supervisor findings after FIX
1. **Tremor provenance is factually wrong.** The current official Tremor Raw Card page identifies the source as `Tremor Card [v1.0.0]`, not `v0.1.1`. The current `tremorlabs/tremor` repository is licensed Apache-2.0, not MIT. Correct both `Metric.tsx` comments and `docs/ui-sources.md` to the verified current source/version/license.
2. **Tremor material adaptation is still too generic to freeze.** `Metric` currently contains a normal card-shaped wrapper and a source comment, but does not clearly preserve a distinctive documented Card contract. Adapt an identifiable part of current Tremor Card v1.0.0 source structure/behavior that is useful for Re:Solve without adding a parallel Card system or forcing an inappropriate API. Re:Solve tokens remain authoritative.
3. **Avatar accessibility/decorative edge case needs one final contract.** `ResolveAvatar` now accepts `name`/`alt`, but still permits a nameless placeholder without intentionally declaring it decorative. Establish a clear non-decorative accessible-name contract and an explicit decorative mode. Prefer the Avatar root as the single accessible image identity; avoid duplicate image/fallback announcements. If status is meaningful, include it in a robust accessible status/name contract rather than relying on `aria-label` on an otherwise-semanticless dot span.
4. **Avatar status-dot visual semantics:** current online/busy/away dots use soft status-surface colors. Use an intentionally visible semantic foreground/action/status indicator color suitable for a small dot and preserve a surface ring for separation.
5. **Gallery Tooltip nesting cleanup:** the keyboard-tooltip example currently wraps an `IconButton` (which already owns a Tooltip) inside another Tooltip trigger. Avoid nested/duplicated tooltips; use a plain Core Button or other focusable trigger for the standalone Tooltip keyboard example.

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
- Untitled UI React: material Avatar behavior adaptation is present; final C1 acceptance depends only on the remaining cleanup above.
- Tremor Raw: claimed material incorporation is not accepted until current Card v1.0.0 / Apache-2.0 provenance is corrected and the adaptation is traceable in code.

## Current Core UI inventory
C1 implementation exists but is not yet frozen/canonical. Do not begin C2 until the final correction passes.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision.

## Known implementation limitations
- final Tremor source/version/license/adaptation correction pending;
- final Avatar accessible/decorative contract cleanup pending;
- one nested Tooltip gallery example pending cleanup;
- shell, PWA, CI and test foundation remain future FOUND-001 substeps by design.

## Next action
Execute supervisor-provided `FOUND-001C1-FIX2` only. Re-review repository afterward. If accepted, freeze C1 as canonical and proceed to the next bounded C2 primitive set.