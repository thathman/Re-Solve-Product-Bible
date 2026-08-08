# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED + CLOSED — FOUND-001C1 ACCEPTED — FOUND-001C2 ACCEPTED + CLOSED — FOUND-001C3 ACCEPTED + CLOSED — FOUND-001C4 CONDITIONAL (CORE CONTRACT FIX REQUIRED)**

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

Normal Component Gallery behavior:
- source route: `src/routes/__dev/ui.tsx`;
- browser path: `/ui` because `__dev` is pathless;
- production guard: TanStack `beforeLoad` + `import.meta.env.PROD` redirect to `/`;
- local/non-production development access remains intended.

### FOUND-001C1 — Core UI primitive foundation
**Status: ACCEPTED — CANONICAL/FROZEN**

Accepted Core inventory:
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

Key accepted contracts:
- public Core boundary under `src/components/core/` and `src/components/core/index.ts`;
- Button loading/a11y/reduced-motion contract;
- IconButton accessible-label + Core Tooltip contract;
- ResolveAvatar meaningful/decorative discriminated accessibility API;
- Metric materially adapts Tremor Card v1.0.0 structural behavior with Apache-2.0 provenance;
- MetricDelta separates direction from sentiment;
- Untitled Avatar and Tremor provenance is auditable.

### FOUND-001C2 — Canonical form and control primitives
**Status: ACCEPTED + CLOSED — CANONICAL/FROZEN**

Accepted Core inventory:
- Input
- Textarea
- Checkbox
- RadioGroup / RadioGroupItem
- Switch
- Select family
- FormField
- FieldGroup

Key accepted contracts:
- typed `FormFieldContext`; no generic cloneElement bridging;
- coherent control ID, required, disabled, invalid and described-by semantics;
- descriptions/errors render consistently when referenced;
- native fieldset/legend behavior for FieldGroup;
- Checkbox and Radio actual controls are 24×24; Switch actual Root is at least 24px high;
- mobile text-entry/select typography remains at least 16px;
- accepted Re:Solve token vocabulary and explicit focus-variable contract;
- high-contrast danger foreground for invalid/error text;
- Select Root and Trigger consume field context correctly;
- C2 visual hierarchy/readability/responsiveness owner-approved;
- Untitled influence for C2 is design reference only.

### FOUND-001C3 — Interaction & Overlay Core UI Pack
**Status: ACCEPTED + CLOSED — CANONICAL/FROZEN**

Accepted Core inventory:
- Dialog
- AlertDialog
- Sheet / SheetBody
- Drawer / DrawerBody
- Popover
- HoverCard
- DropdownMenu
- ContextMenu
- Accordion
- Collapsible
- Tabs
- ScrollArea / ScrollBar

Verified accepted contracts:
- Radix/shadcn remains the accessible source foundation; Vaul 1.1.2 is used for Drawer;
- Vaul was already present before C3 and was first consumed by Re:Solve in C3; C3 did not install it;
- shared `--rs-backdrop`/`bg-rs-backdrop` contract exists with restrained light/dark scrim opacity;
- major overlay surfaces use explicit Re:Solve raised surfaces, borders and `shadow-rs-overlay`;
- Dialog/AlertDialog use constrained narrow-screen width/max-height and restrained transition timing;
- AlertDialog action/cancel treatment consumes canonical Core Button variants;
- Sheet uses Header → independently scrollable SheetBody → non-overlapping Footer composition and right/bottom safe-area treatment;
- Drawer uses viewport max-height, independently scrollable DrawerBody and bottom safe-area footer treatment;
- DropdownMenuItem and ContextMenuItem expose canonical `variant="destructive"` with high-contrast danger foreground and soft danger focus background;
- Popover/HoverCard use Re:Solve raised surface/border/elevation treatment;
- Accordion and Tabs use accepted focus-variable contract;
- Tabs long-label overflow is demonstrated through Core ScrollArea + visible horizontal ScrollBar; canonical TabsList does not hide its scrollbar;
- Component Gallery proves both vertical and horizontal ScrollArea behavior;
- accepted C1 Skeleton gallery evidence remains present;
- `/ui` production guard remains secured;
- no Vue runtime/package or parallel component system was introduced;
- no new dependency or lockfile was added in the C3 normalization/closure work.

C3 closure hygiene:
- leaked Lovable/supervisor prompt text was removed from the current home route;
- current `/` remains only a temporary starter placeholder and no product homepage was built;
- current home placeholder is clean but not byte-for-byte identical to the older C2 baseline; this trivial wrapper/alt-text deviation was reviewed and accepted as non-blocking;
- Skeleton evidence was restored after an intermediate gallery regression;
- dedicated horizontal ScrollArea evidence now lives under C3 Layout Utilities;
- `docs/ui-sources.md` records the shadcn Drawer wrapper and correct Vaul history/license without duplication.

## FOUND-001C4 — Utility, Feedback & Composition Core Pack
**Status: CONDITIONAL — CORE CONTRACT FIX REQUIRED BEFORE C5**

### Verified implementation present on application `main`
- C4 exports exist through `src/components/core/index.ts` for Alert, Empty, Spinner, Progress, Toast/Toaster, Item family, ButtonGroup, InputGroup family, Kbd/KbdGroup, Toggle/ToggleGroup, Breadcrumb and StatePanel;
- StatePanel is a presentation-only composition above Empty with `empty`, `error`, `permission`, `offline` and `not-built` variants;
- Radix primitives are used for Progress, Toggle and ToggleGroup; Sonner 2.0.7 is already present and consumed by the Core Toast boundary;
- no new dependency is visible in `package.json` for C4;
- Component Gallery contains a C4 section and existing C1-C3 sections remain present;
- the home route remains the clean temporary starter placeholder; C4 did not reintroduce prompt leakage;
- `/ui` production guard remains part of the gallery route.

### Remaining verified C4 findings
1. **Progress accessible state is broken.** `Progress.tsx` destructures `value` but does not pass `value={value}` to `ProgressPrimitive.Root`; Radix therefore cannot expose the actual determinate value/state. The visible label is also not programmatically bound to the progress root.
2. **C4 reintroduced non-canonical token names.** New files use utilities such as `border-rs-border`, `divide-rs-border`, `bg-rs-border` and `ring-rs-ring`, which are not accepted Re:Solve authority names. Use `rs-border-normal`/`rs-border-strong` and the explicit accepted focus-variable contract instead.
3. **InputGroup does not fully inherit FormField state.** The inner Input/Textarea consumes FormField context, but the group wrapper owns the visible border/focus ring and does not consume field invalid state; an errored FormField can therefore lose the intended group-level invalid treatment. The current focus treatment also uses non-canonical `ring-rs-ring` instead of the frozen focus-variable contract.
4. **InputGroup action composition is hand-styled in gallery code.** A plain Core Button is manually given group-specific radius/height/border classes. Add a canonical InputGroupButton (or equivalent current-shadcn-aligned Core piece) that composes the accepted Core Button contract. Also prove the requested textarea + block/footer/action composition rather than only inline input arrangements.
5. **Spinner reduced-motion behavior is backwards.** `motion-reduce:animate-[spin_2s_linear_infinite]` explicitly requests continued spinning for reduced-motion users. Meaningful Spinner should expose one polite loading announcement; decorative Spinner should be hidden from assistive technology and used when visible surrounding text already communicates loading.
6. **Toast boundary is too porous and weakly typed.** It disables `no-explicit-any`, casts option objects to `any`, and exposes raw `sonnerToast` through `custom`, allowing callers to bypass the Core contract. Keep a typed wrapper API and do not expose the raw Sonner callable. Toast border/action/status icon styling also uses non-canonical or semantically incorrect tokens.
7. **Status foreground/surface semantics drift.** Alert icons and Toast status icons use soft status-surface tokens as text colors; Progress success also uses the soft success surface as the bar. Status surfaces should remain backgrounds and high-contrast `*-foreground` tokens should carry icon/text/indicator color where appropriate.
8. **Item interactive semantics are invalid.** `interactive=true` only adds `cursor-pointer` to a `<div>`. The gallery shows these rows as interactive even though they are not keyboard-focusable buttons/links. Replace the cursor-only interaction flag with an `asChild`/semantic interactive composition or another accessible contract; do not create nested interactive controls.
9. **Item/Empty media use cloneElement solely to force icon sizing.** This can overwrite child className and is unnecessary for presentation. Prefer structural CSS child selectors for SVG sizing while allowing Avatar/custom media to preserve their own contract.
10. **Empty uses non-canonical border token and 500ms entrance motion.** Normalize token usage and keep motion within the accepted restrained contract; do not make reduced-motion users animate.
11. **ButtonGroup is incomplete against the requested composition contract.** It has the group container but no canonical separator/text/addon pieces, gallery groups have no accessible group names, and the split-button demo hand-writes a white border. Adapt the current React shadcn Button Group composition more materially while still consuming accepted Core Button/IconButton.
12. **Toggle focus/pressed treatment is incomplete.** It uses non-canonical focus/border tokens and the visual pressed state is essentially color-only. Preserve Radix `aria-pressed` while adding a non-color visual distinction such as canonical border/elevation/outline treatment. Gallery should prove an explicitly pressed standalone Toggle and labelled ToggleGroups.
13. **Breadcrumb has an unused `separator` prop and incomplete long-label evidence.** Either implement that prop or remove it from the API; preserve explicit BreadcrumbSeparator. Add a genuinely long/collapsed mobile-safe evidence case without horizontal page overflow.
14. **Gallery evidence is incomplete.** There is no standalone standard Empty demonstration; Spinner meaningful/decorative usage is ambiguous/duplicative; ButtonGroups are unlabelled; no InputGroup textarea footer/action example exists; standalone Toggle pressed evidence is absent; Breadcrumb evidence is collapsed but not genuinely long.
15. **C4 provenance is incomplete.** `docs/ui-sources.md` records Alert/Progress/Toggle/Toggle Group/Breadcrumb but omits material C4 intake for Empty, Spinner, Item, Button Group, Input Group, Kbd and Sonner/Toast. Record the actual Sonner package/version and distinguish shadcn source-pattern adaptation from runtime package use accurately.

### Review classification
C4 is structurally sound enough for one bounded correction. Preserve the current component inventory and frozen C1-C3 APIs. Do not begin C5 until the semantic, token, accessibility, composition and provenance issues above are corrected and re-reviewed.

## shadcn ecosystem direction now canonical
- `shadcn-vue` is approved as a visual/composition/block-pattern source only; Re:Solve remains React/TanStack and must use React shadcn equivalents where available rather than Vue runtime code.
- approved future intake includes core interaction/utility primitives, advanced controls, conversation/Àríyá primitives, questionnaire/review-style composition and QR presentation patterns subject to exact source verification.
- two-column form + cover-image auth blocks are the preferred composition reference for desktop login/signup/recovery/OTP/step-up surfaces with a deliberate single-column mobile transformation.
- shadcn dashboard blocks are approved composition references but do not override Re:Solve dashboard, Attention Engine, TanStack DataTable, Tremor/Recharts or navigation architecture.
- Questionnaire is intended as a higher-order review/form composition above canonical FormField/FieldGroup primitives, not a separate forms framework.
- QR is an approved utility/presentation pattern; security-sensitive QR flows must use signed/short-lived references rather than raw secrets.

## Current architecture facts
- framework/build tool: TanStack Start v1 + Vite;
- routing: TanStack file-based routes;
- React: 19.2.0;
- package manager: bun@1.3.3;
- Tailwind: 4.2.1;
- shadcn: initialized `new-york`, source-owned registry; do not rerun init;
- current primitive base: Radix + shadcn source components;
- Drawer primitive: Vaul 1.1.2;
- Toast runtime: Sonner 2.0.7 (pre-existing dependency first consumed through Re:Solve Core in C4);
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
- shadcn/ui: incorporated/source-owned starter foundation and materially normalized through Re:Solve Core across C1-C3; C4 current-source utility/composition intake is present but not yet accepted.
- shadcn-vue: approved visual/composition/block reference only; never a runtime dependency.
- Radix: incorporated beneath current shadcn and Core components.
- Vaul: pre-existing dependency first consumed by Drawer in C3; MIT; Re:Solve surface/scroll/safe-area normalization accepted.
- Sonner: pre-existing 2.0.7 dependency first consumed through the Re:Solve Core Toast boundary in C4; final typed/styling contract pending C4 correction.
- Lucide: incorporated as primary icon family.
- Untitled UI React: material Avatar incorporation accepted in C1; C2 form composition is design reference only.
- Tremor Raw: material Metric incorporation accepted in C1.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision.

## Known implementation limitations
- C4 utility/composition primitives require one bounded contract correction before acceptance;
- Questionnaire/review and QR patterns are approved future source candidates but exact React/source implementations have not yet been selected;
- advanced input/scheduling, conversation/Àríyá primitives, auth, application shell, PWA, CI and testing remain future FOUND-001 substeps by design.

## Next action
Execute the supervisor-provided `FOUND-001C4-FIX` only. Correct Progress semantics, token drift, InputGroup/FormField integration, Spinner/Toast accessibility, Item interaction semantics, ButtonGroup/Toggle/Breadcrumb composition and C4 provenance/evidence. Re-review repository afterward. Do not begin FOUND-001C5.