# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED + CLOSED — FOUND-001C1 ACCEPTED — FOUND-001C2 CONDITIONAL (FIX2 REQUIRED)**

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
- Normal accepted behavior is a production redirect guard on `/ui`.
- The owner temporarily disabled that guard for C2 visual review; re-secure it after C2 visual acceptance and before C3 proceeds.
- Lovable embedded Preview has previously evaluated production-like, so visual review may temporarily require explicit supervised exposure.

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
**Status: CONDITIONAL — FIX2 REQUIRED BEFORE VISUAL ACCEPTANCE/C3**

### Verified implementation now present after first correction
- C2 Core forms exist under `src/components/core/forms/` and remain exported through `@/components/core`;
- Input and Textarea consume a typed FormField context rather than generic `cloneElement` injection;
- SelectTrigger consumes the same field context and receives control ID, described-by, invalid and required ARIA state;
- most invented form-token vocabulary was normalized to accepted Re:Solve authority tokens and explicit focus variables;
- Input/Textarea use mobile `text-base` with smaller typography only from the `md` breakpoint;
- invalid/error text now uses `rs-status-danger-foreground`;
- no new dependencies or lockfiles were added;
- C2 remains Radix/native based with Untitled form composition as design reference only.

### Remaining supervisor findings after first C2 correction
1. **FormField still references a missing description node when both description and error exist.** `descriptionId` is created whenever description exists and included in `describedBy`, but the description is rendered only under `description && !error`. Either render description and error together or compute `describedBy` only from nodes actually rendered.
2. **FieldGroup has the same missing-node defect.** It includes `descriptionId` whenever description exists but suppresses the description node when error exists.
3. **Checkbox touch-target fix is only visual-wrapper size.** A 24×24 non-interactive wrapper surrounds a Radix Root that remains 16×16. The actual interactive control must be at least 24×24; a smaller visible glyph may sit inside it. Remove the `as any` checked-state cast if a proper Radix checked-state type can be expressed directly.
4. **RadioGroupItem has the same wrapper-only touch-target problem.** The Radix interactive item remains 16×16 inside a 24×24 non-interactive wrapper.
5. **Switch has the same wrapper-only issue.** Its Radix Root remains 20px high inside a 24px wrapper. Make the Root itself at least 24px high and adjust thumb/translation coherently.
6. **Gallery Switch labels are still not programmatically associated.** `Automatic Backups` and `Maintenance Mode` labels still have no `htmlFor`, and Switch instances have no matching IDs.
7. **Gallery still contains stale `text-rs-text-tertiary`.** Remove it and use an accepted Re:Solve text token. The disabled checkbox label also still uses a `disabled:` variant on a `<label>`, which cannot reflect sibling disabled state; use explicit disabled text styling.
8. **Promised Select gallery evidence is missing.** Current gallery lacks a placeholder-only example, disabled trigger, disabled option and genuinely long option label. Add exactly these evidence cases without turning the gallery into a business form.
9. **Required Select native/form semantics remain incomplete.** `Select` is still a direct alias to `SelectPrimitive.Root`, so FormField `required`/`disabled` state reaches only the trigger. Wrap the Radix Root in a Core `Select` component that consumes FormField context and passes required/disabled to the Root while preserving the existing public API as much as possible.
10. **FieldGroup error evidence is still absent.** Add one small gallery example proving the group description/error association after the missing-node fix.

### Visual review status
- Pre-fix screenshots confirmed the overall desktop/mobile composition is strong and should not be redesigned.
- C2 visual acceptance is deferred until the remaining semantic/touch-target fixes above are committed.
- After implementation passes, request only focused Fields & Controls screenshots in light desktop, dark desktop, and dark/narrow mobile plus an error/select/control close-up.

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
- Untitled UI React: material Avatar incorporation accepted in C1; C2 form composition is design reference only unless later code proves a specific material adaptation.
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
- C2 described-by node consistency still needs correction;
- actual interactive touch targets for Checkbox/Radio/Switch remain undersized;
- Select Root required/disabled propagation and gallery evidence remain incomplete;
- gallery contains one stale non-canonical token and unassociated Switch labels;
- overlay/menu/dialog primitives are not yet canonical;
- application states and broader composites remain future C substeps;
- shell, PWA, CI and test foundation remain future FOUND-001 substeps by design.

## Next action
Execute supervisor-provided `FOUND-001C2-FIX2` only. Re-review repository afterward. If implementation passes, perform focused C2 visual acceptance while `/ui` is temporarily exposed, then re-secure `/ui` before starting C3.