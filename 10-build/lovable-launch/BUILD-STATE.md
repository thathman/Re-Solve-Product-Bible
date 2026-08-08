# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED + CLOSED — FOUND-001C1 ACCEPTED — FOUND-001C2 ACCEPTED + CLOSED — FOUND-001C3 ACCEPTED + CLOSED — FOUND-001C4 CONDITIONAL (FINAL C4 CLOSURE HYGIENE REQUIRED)**

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
**Status: CONDITIONAL — FINAL C4 CLOSURE HYGIENE REQUIRED BEFORE C5**

### Current C4 inventory present on application `main`
- Alert
- Empty
- Spinner
- Progress
- Toast / Toaster
- Item family
- ButtonGroup / ButtonGroupSeparator / ButtonGroupText
- InputGroup family / InputGroupButton
- Kbd / KbdGroup
- Toggle / ToggleGroup
- Breadcrumb family
- StatePanel

### Verified C4 contracts now materially correct after FIX/FIX2/FIX3
- Progress forwards determinate `value` to Radix and has generated-ID/ARIA naming support without requiring an explicit ID;
- Spinner uses `motion-safe:animate-spin`; decorative mode is `aria-hidden`, meaningful mode exposes status text;
- InputGroup consumes FormField invalid/disabled state with nullish override semantics and includes `min-w-0`;
- InputGroupButton composes Core Button and inherits FormField disabled state;
- InputGroupAddon exposes `inline-start`, `inline-end`, `block-start`, `block-end` visual alignment values;
- Item removed the cursor-only `interactive` prop; noninteractive rows no longer carry clickable hover/focus treatment;
- ItemMedia/EmptyMedia use direct-child SVG selectors rather than cloneElement sizing;
- Empty sizes naturally and entrance motion is motion-safe;
- Toast public API now exposes typed `message`, `info`, `success`, `warning`, `error`, `loading`, `dismiss` methods without raw Sonner exposure or broad callable-object assertions;
- Toast action foreground now uses `text-rs-text-inverse` and status icons use foreground semantics;
- ButtonGroupText now exists and is exported through the Core boundary;
- ButtonGroupSeparator orientation names now correspond to the rendered line;
- Toggle pressed state has explicit non-color ring/elevation feedback and accepted focus variables;
- Breadcrumb dead separator prop was removed and long wrapping evidence exists;
- gallery contains Warning Toast, standalone Empty, InputGroupText, InputGroupButton, textarea footer, pressed Toggle and long Breadcrumb evidence;
- gallery ToggleGroup examples now use `aria-labelledby` on both group roots;
- Sonner provenance lives under Runtime UI Dependencies and ButtonGroupText is recorded in shadcn source-pattern intake;
- Sonner 2.0.7 and Vaul 1.1.2 remain pre-existing dependencies;
- `package.json` and the temporary home route remain unchanged;
- `/ui` remains production guarded.

### Remaining verified C4 blockers after FIX3
1. **Item still violates the explicit no-cast closure criterion.** `src/components/core/layout/Item.tsx` still renders `<Comp ref={ref as any}>`. The completion report said the ref/asChild contract was corrected, but `main` still contains `as any`. Remove the cast and use a truthful Slot/polymorphic ref strategy. This is a blocker because FIX3 explicitly required `no as any`.
2. **InputGroup gallery DOM order is still wrong in two examples.** `Search Domain` still renders an addon before the input, and `Assign User` still renders the inline-start addon before the input. The accepted C4 contract requires the input/textarea first in DOM order and `align` to control visual position.
3. **InputGroup block-end gallery still uses a layout hack.** `Note with Footer` still renders `<InputGroup className="flex-col">`. The C4 contract explicitly requires `align="block-end"` to produce the composition without adding `flex-col` to the group.
4. **ButtonGroupText is imported/exported but not actually demonstrated in the C4 gallery.** Add one compact evidence example so the new public primitive is reviewable rather than dead intake.
5. **ButtonGroup separator gallery orientation is still semantically wrong.** The horizontal `Publish options` ButtonGroup uses `ButtonGroupSeparator orientation="horizontal"`, which now correctly renders a horizontal line. In a horizontal group this should be a vertical separator (or omit the prop if vertical is the default).
6. **ButtonGroupText border treatment is incomplete.** Its class includes `border-rs-border-normal` but no border width utility, so the declared border color does not create a visible border. Add an actual restrained border where the composition requires it, normalized to the accepted token.

### Review classification
The implementation is close enough that no further architecture work is needed. Execute one closure-hygiene fix covering only the six findings above. If clean, freeze C4 immediately and proceed to C5.

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
- shadcn/ui: source-owned starter foundation, materially normalized through Re:Solve Core; C4 remains conditional pending final closure hygiene.
- shadcn-vue: visual/composition/block reference only; no runtime dependency.
- Radix: incorporated beneath shadcn/Core.
- Vaul: pre-existing dependency first consumed by Drawer in C3; accepted.
- Sonner: pre-existing 2.0.7 dependency first consumed through Core Toast in C4; wrapper/action contract now materially corrected.
- Lucide: primary icon family.
- Untitled UI React: material Avatar incorporation accepted in C1; later use remains selective.
- Tremor Raw: material Metric incorporation accepted in C1.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision.

## Known implementation limitations
- C4 requires one final closure-hygiene fix before acceptance;
- Questionnaire/review and QR remain approved later source candidates;
- advanced input/scheduling, conversation/Àríyá, auth, application shell, PWA, CI and tests remain future FOUND-001 substeps.

## Next action
Execute supervisor-provided `FOUND-001C4-FIX4` only. Remove the remaining Item `as any`, correct InputGroup gallery DOM order and block-end evidence, demonstrate ButtonGroupText, correct Publish separator orientation, and give ButtonGroupText a real restrained border treatment. Re-review afterward. Do not begin FOUND-001C5.
