# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED + CLOSED — FOUND-001C1 ACCEPTED — FOUND-001C2 ACCEPTED + CLOSED — FOUND-001C3 ACCEPTED + CLOSED — FOUND-001C4 CONDITIONAL (FINAL C4 CONTRACT CLEANUP REQUIRED)**

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
- Current Lovable application: `thathman/re-solve-c560d62c`.
- Visibility: `private`.
- Default branch: `main`.
- Legacy reference repository remains `thathman/Re-Solve`.
- Product Bible is specification/reference only, not application source.
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

Accepted foundation includes Re:Solve-owned semantic OKLCH tokens, light/dark/system theming, self-hosted Inter Variable + JetBrains Mono Variable, density/layout/elevation/focus/safe-area/motion contracts, accessible status/destructive semantics, chart tokens and shadcn compatibility mappings.

Component Gallery contract:
- source: `src/routes/__dev/ui.tsx`;
- browser path: `/ui` because `__dev` is pathless;
- production guard: TanStack `beforeLoad` + `import.meta.env.PROD` redirect to `/`;
- local/non-production access remains intended.

### FOUND-001C1 — Core UI Primitive Foundation
**Status: ACCEPTED — CANONICAL/FROZEN**

Accepted inventory:
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

Key contracts:
- public Core boundary under `src/components/core/` + `src/components/core/index.ts`;
- Button loading/a11y/reduced-motion behavior accepted;
- IconButton requires accessible label and consumes Core Tooltip;
- ResolveAvatar has meaningful/decorative accessibility contract;
- Metric materially adapts Tremor Card structure with provenance;
- MetricDelta separates direction from sentiment.

### FOUND-001C2 — Canonical Form & Control Primitives
**Status: ACCEPTED + CLOSED — CANONICAL/FROZEN**

Accepted inventory:
- Input
- Textarea
- Checkbox
- RadioGroup / RadioGroupItem
- Switch
- Select family
- FormField
- FieldGroup

Key contracts:
- typed FormField context and coherent ID/required/disabled/invalid/described-by semantics;
- description/error IDs always map to rendered nodes;
- native fieldset/legend semantics retained;
- Checkbox/Radio actual controls are 24×24; Switch actual Root is at least 24px high;
- narrow/mobile text-entry/select typography remains at least 16px;
- accepted token vocabulary and explicit focus-variable contract;
- Select Root/Trigger integrate with FormField context;
- C2 owner-approved visually.

### FOUND-001C3 — Interaction & Overlay Core UI Pack
**Status: ACCEPTED + CLOSED — CANONICAL/FROZEN**

Accepted inventory:
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

Key contracts:
- Radix/shadcn foundation retained; Vaul 1.1.2 used for Drawer;
- shared Re:Solve backdrop and raised/elevation treatment;
- Core Button-backed AlertDialog actions;
- Sheet and Drawer long-content/safe-area contracts;
- destructive menu variants use high-contrast danger foreground semantics;
- Accordion/Tabs accepted focus contract;
- Tabs overflow remains discoverable through Core ScrollArea + horizontal ScrollBar;
- `/ui` production guard secured;
- no Vue runtime/package or parallel component system introduced.

C3 closure hygiene also removed leaked prompt text from the home route and restored accepted Skeleton gallery evidence.

## FOUND-001C4 — Utility, Feedback & Composition Core Pack
**Status: CONDITIONAL — FINAL C4 CONTRACT CLEANUP REQUIRED BEFORE C5**

### Current C4 inventory present on application `main`
- Alert
- Empty
- Spinner
- Progress
- Toast / Toaster
- Item family
- ButtonGroup / ButtonGroupSeparator
- InputGroup family / InputGroupButton
- Kbd / KbdGroup
- Toggle / ToggleGroup
- Breadcrumb family
- StatePanel

### Verified improvements after C4-FIX and C4-FIX2
- non-canonical C4 border/ring token drift was materially normalized to accepted authority tokens;
- Progress now forwards the determinate `value` to Radix and uses generated IDs/ARIA naming support;
- Spinner uses `motion-safe:animate-spin`; decorative mode uses `aria-hidden`, meaningful mode exposes status text;
- InputGroup consumes FormField invalid/disabled state via nullish override semantics;
- InputGroupButton composes Core Button and inherits FormField disabled state;
- Item removed the cursor-only `interactive` prop and uses `asChild` for semantic button/link composition;
- ItemMedia/EmptyMedia use direct-child SVG selectors rather than cloneElement sizing;
- Empty no longer forces a 400px minimum and entrance motion is motion-safe;
- Toast no longer exposes raw Sonner and no `any` suppression/cast remains;
- Toggle pressed state now has non-color ring/elevation feedback and accepted focus variables;
- Breadcrumb dead separator prop was removed and long wrapping evidence exists;
- gallery contains Warning Toast, standalone Empty, InputGroupText, InputGroupButton, textarea footer, pressed Toggle and long Breadcrumb evidence;
- Sonner provenance now lives under Runtime UI Dependencies;
- Sonner 2.0.7 and Vaul 1.1.2 remain pre-existing dependencies;
- `package.json` and the temporary home route remain unchanged;
- `/ui` remains production guarded.

### Remaining verified C4 blockers after FIX2
1. **InputGroup alignment/DOM-order contract is still incomplete.** `InputGroupAddon.align` only changes addon styling. The parent does not automatically recompose for block addons, so the gallery still requires `className="flex-col"`. Inline-start examples also place addons before the input in DOM order. Current React shadcn guidance requires addons to remain after Input/InputGroupTextarea in DOM order and `align` to control visual placement. The Core implementation should make this true without gallery-only layout hacks.
2. **ToggleGroup roots remain unnamed.** Gallery labels individual ToggleGroupItem controls, but the single-selection and multiple-selection ToggleGroup roots still lack `aria-label` or `aria-labelledby`.
3. **Toast action foreground is semantically wrong.** Toaster primary action uses `text-rs-status-success-foreground` with `bg-rs-action-primary`. It must use the same inverse/action foreground contract as canonical Core Button rather than a success-status foreground.
4. **Toast wrapper typing is still misleading.** `toast.message` is asserted to `typeof sonnerToast`, a callable object type with attached methods; the wrapper function does not actually carry those runtime properties. Replace broad callable-object assertions with method-specific `Parameters<>` / `ReturnType<>` wrappers or equivalent accurate typing.
5. **ButtonGroupText is still absent.** Current React shadcn Button Group treats ButtonGroupText as a first-class composition primitive and it is useful for labels/prefixes. Add it through the Core boundary rather than omitting part of the selected source pattern.
6. **ButtonGroupSeparator orientation should match a clear canonical contract.** Prefer the current shadcn meaning where separator orientation describes the separator line (`vertical` in a horizontal button group, `horizontal` in a vertical group), or derive it from ButtonGroup context. Avoid an API where `orientation="horizontal"` renders a vertical line without clear context semantics.
7. **Progress naming should be hardened for optional labels.** If `showLabel=true` but `label` is absent and the caller supplies `aria-label`, do not also generate an empty `aria-labelledby` target that can take naming precedence. Only bind the visible label ID when an actual visible label exists and no explicit accessible-name prop overrides it.
8. **Item polymorphic ref typing should not lie.** `Item` now renders semantic controls through Slot, but its forwarded ref is still typed as `HTMLDivElement`; an `asChild` button/link can therefore produce an incorrect ref type contract. Align the implementation with a safe current-shadcn-style `asChild`/Slot typing strategy without casts.
9. **InputGroup responsive foundation should include the current-source `min-w-0` behavior** so grouped controls do not force avoidable overflow in constrained layouts.

### Review classification
C4 remains structurally sound. One final narrow `FOUND-001C4-FIX3` should address only the remaining blockers above. No redesign or new component family is required. If clean, freeze C4 and proceed to C5.

## shadcn ecosystem direction now canonical
- `shadcn-vue` is a visual/composition/block reference only; Re:Solve remains React/TanStack and uses React shadcn equivalents where available.
- approved future intake includes advanced controls, conversation/Àríyá primitives, Questionnaire/review composition and QR presentation patterns subject to exact source verification.
- two-column form + cover-image auth blocks are the preferred desktop composition reference for login/signup/recovery/OTP/step-up with deliberate single-column mobile transformation.
- shadcn dashboard blocks are composition references only and do not override Re:Solve dashboard, Attention Engine, TanStack DataTable, Tremor/Recharts or navigation architecture.
- Questionnaire is a higher-order review/form composition above canonical FormField/FieldGroup, not a second forms framework.
- security-sensitive QR flows must use signed/short-lived references rather than raw secrets.

## Current architecture facts
- framework/build: TanStack Start v1 + Vite;
- routing: TanStack file routes;
- React: 19.2.0;
- package manager: Bun 1.3.3;
- Tailwind: 4.2.1;
- shadcn: initialized `new-york`, source-owned; do not rerun init;
- primitive base: Radix + shadcn source components;
- Drawer: Vaul 1.1.2;
- Toast runtime: Sonner 2.0.7;
- icons: Lucide 0.575.0;
- typography: Inter Variable + JetBrains Mono Variable via Fontsource 5.3.0;
- query/server state: TanStack Query;
- forms/validation available: React Hook Form + Zod;
- chart foundation: Recharts;
- testing stack: not configured;
- PWA tooling: not configured;
- auth/domain setup: not yet implemented.

## UI-source incorporation state
- shadcn/ui: source-owned starter foundation, materially normalized through Re:Solve Core; C4 remains conditional pending final composition/type cleanup.
- shadcn-vue: visual/composition/block reference only; no runtime dependency.
- Radix: incorporated beneath shadcn/Core.
- Vaul: pre-existing dependency first consumed by Drawer in C3; accepted.
- Sonner: pre-existing 2.0.7 dependency first consumed through Core Toast in C4; final wrapper/action contract pending.
- Lucide: primary icon family.
- Untitled UI React: material Avatar incorporation accepted in C1; later use remains selective.
- Tremor Raw: material Metric incorporation accepted in C1.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision.

## Known implementation limitations
- C4 requires one final narrow closure fix before acceptance;
- Questionnaire/review and QR remain approved later source candidates;
- advanced input/scheduling, conversation/Àríyá, auth, application shell, PWA, CI and tests remain future FOUND-001 substeps.

## Next action
Execute supervisor-provided `FOUND-001C4-FIX3` only. Correct InputGroup visual alignment/DOM order, ToggleGroup naming, Toast action/type contract, ButtonGroupText/separator semantics, Progress optional-label naming, Item polymorphic ref typing and InputGroup min-width behavior. Re-review afterward. Do not begin FOUND-001C5.
