# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED + CLOSED — FOUND-001C1 ACCEPTED — FOUND-001C2 CONDITIONAL**

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
- Component Gallery consumes the public Core boundary;
- Button loading/accessibility/reduced-motion behavior accepted;
- IconButton requires an accessible label and consumes Core Tooltip;
- Tooltip, Separator, StatusBadge and Avatar gallery evidence accepted;
- ResolveAvatar uses a discriminated meaningful/decorative accessibility contract and a single accessible identity;
- Metric materially adapts Tremor Card v1.0.0 structural behavior with Apache-2.0 provenance;
- MetricDelta separates direction from sentiment;
- Untitled UI Avatar and Tremor Card provenance is auditable;
- no new parallel design system, package manager or lockfile was introduced.

C1 APIs are canonical and frozen for downstream use.

## FOUND-001C2 — Canonical form and control primitives
**Status: CONDITIONAL — correction required before C3**

### Verified implementation present
- new Core form/control files exist under `src/components/core/forms/`;
- public `@/components/core` export surface now includes Input, Textarea, Checkbox, RadioGroup/RadioGroupItem, Switch, Select primitives, FormField and FieldGroup;
- native Input/Textarea plus Radix Checkbox/Radio/Switch/Select foundations are used;
- FormField uses generated IDs and attempts label/description/error association;
- FieldGroup uses fieldset/legend semantics;
- Component Gallery includes a Fields & Controls section with text fields, required/error/read-only/disabled states, Select, Checkbox, RadioGroup and Switch examples;
- no new dependencies or lockfiles were added;
- production `/ui` guard remains unchanged.

### Remaining C2 supervisor findings
1. **Invented/non-canonical token names are used throughout the new controls.** Examples include `rs-text-tertiary`, `rs-focus-ring`, `rs-focus-offset`, `rs-outline`, `rs-surface-overlay`, `rs-surface-secondary`, and `rs-text-primary-inverse`. These are not defined by the accepted FOUND-001B token authority in `src/styles.css`. Forms must use the accepted Re:Solve tokens/explicit focus-variable contract rather than silently introducing a second vocabulary.
2. **Invalid/error styling uses the soft danger surface token as text/border.** Error text and invalid borders currently use `rs-status-danger` in places where the dedicated semantic foreground/indicator token is required for contrast. Use `rs-status-danger-foreground` or another accepted explicit semantic foreground as appropriate.
3. **FormField `aria-describedby` construction is unsafe and can reference missing nodes.** It uses the Tailwind/class merge helper `cn()` to join IDs, and when both description and error exist it can include the description ID while the description node is not rendered because `description && !error`. Build described-by IDs with a plain string join and render/associate only nodes that actually exist.
4. **FormField cloneElement is not a reliable label/ARIA bridge for composite controls.** Cloning a Radix `Select.Root` and injecting `id`/`aria-describedby`/`aria-invalid` does not place those attributes on the actual trigger control. The Select examples therefore do not satisfy the claimed FormField label/error association contract. Establish an explicit supported integration path for composite controls, preferably by letting SelectTrigger receive the actual control ID and ARIA state via a lightweight Core field context or another typed canonical mechanism. Do not couple to React Hook Form.
5. **Switch gallery labels are not programmatically associated.** Visible labels such as `Automatic Backups` are plain labels without `htmlFor`/control IDs. Fix the gallery and canonical usage pattern so Switch has a real accessible name.
6. **Touch targets are undersized.** Checkbox and Radio items are 16×16px and Switch is 20px high. The C2 requirement explicitly calls for appropriate touch targets. Preserve compact visuals if desired, but provide at least a 24×24 interaction target (and preferably a comfortable row/label hit area) without breaking density.
7. **Compact text inputs can fall below the mobile-safe 16px font size.** `Input size="compact"` applies `text-xs` at narrow widths, contradicting the reported iOS-zoom safeguard. Keep mobile text at 16px and reduce typography only at an appropriate breakpoint.
8. **Select state/surface styling references undefined tokens.** Trigger/content/item focus/disabled/placeholder styling must be normalized to existing `rs-surface-*`, `rs-border-*`, `rs-text-*`, semantic status, and explicit focus tokens.
9. **Untitled reference claim is not reflected in the provenance ledger.** `docs/ui-sources.md` has not changed from the accepted C1 state. If C2 only used Untitled as visual reference, that is acceptable, but the implementation report must not claim a provenance update that does not exist. Do not invent a new material-incorporation entry unless actual source/API behavior was adapted.

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
- form/validation libraries already available: React Hook Form + Zod;
- chart foundation: Recharts;
- environment security: public VITE boundary + createServerOnlyFn private boundary;
- testing stack: not configured;
- PWA tooling: not configured;
- auth/domain setup: not yet implemented.

## UI-source incorporation state
- shadcn/ui: incorporated/source-owned starter foundation.
- Radix: incorporated beneath current shadcn and Core components.
- Lucide: incorporated as primary icon family.
- Untitled UI React: material Avatar incorporation accepted in C1; C2 currently uses form composition as reference only unless later code proves a specific material adaptation.
- Tremor Raw: material Metric incorporation accepted in C1.

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

C2 exists but is not canonical/frozen yet:
- Input
- Textarea
- Checkbox
- RadioGroup / RadioGroupItem
- Switch
- Select family
- FormField
- FieldGroup

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision.

## Known implementation limitations
- C2 token vocabulary and invalid-state styling need normalization;
- FormField composite-control semantics need correction;
- Switch labeling and small-control touch targets need correction;
- compact mobile font sizing needs correction;
- overlay/menu/dialog primitives are not yet canonical;
- application states and broader composites remain future C substeps;
- shell, PWA, CI and test foundation remain future FOUND-001 substeps by design.

## Next action
Execute one narrowly scoped FOUND-001C2 correction covering token normalization, field semantics, composite Select integration, control labeling/touch targets and mobile-safe sizing. Re-review repository afterward. Do not begin FOUND-001C3 until C2 passes.
