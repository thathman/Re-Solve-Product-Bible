# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED + CLOSED — FOUND-001C1 ACCEPTED/FROZEN — FOUND-001C2 ACCEPTED/FROZEN — FOUND-001C3 ACCEPTED/FROZEN — FOUND-001C4 ACCEPTED/FROZEN — FOUND-001C5A READY**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — public, specification/planning only.
- Current Lovable app: `thathman/re-solve-c560d62c` — private, `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Lovable project
- Project Knowledge installed: `YES`.
- Canonical workspace Skills installed: `YES — 30 Re:Solve skills + self-host-check`.
- Platform default skill active: `design-taste-frontend`.
- Duplicate `.agents/skills/` drafts: removed.
- Obsolete `airix-*` skills: none.

## Backend state
- Lovable Cloud enabled for development.
- Custom database tables: none.
- RLS policies: none.
- Migrations: not initialized.
- Demo seed/reset: not initialized.

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
- Button / IconButton
- Badge / StatusBadge
- ResolveAvatar
- Tooltip
- Separator
- Skeleton
- Metric / MetricDelta

Key contracts include Core ownership boundary, accessible Button/IconButton behavior, meaningful/decorative Avatar semantics, Tremor-informed Metric structure and direction-vs-sentiment MetricDelta.

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

Key contracts include typed FormField context, coherent ID/required/disabled/invalid/described-by semantics, native fieldset/legend behavior, real touch-size controls, 16px narrow-screen entry typography, accepted focus-variable contract and FormField-aware Select behavior.

### FOUND-001C3 — Interaction & Overlay Core UI Pack
**Status: ACCEPTED + CLOSED — CANONICAL/FROZEN**

Accepted inventory:
- Dialog / AlertDialog
- Sheet / SheetBody
- Drawer / DrawerBody
- Popover / HoverCard
- DropdownMenu / ContextMenu
- Accordion / Collapsible
- Tabs
- ScrollArea / ScrollBar

Key contracts include Radix/shadcn foundation, Vaul 1.1.2 for Drawer, shared Re:Solve backdrop/elevation, Core Button-backed destructive confirmation, long-content Sheet/Drawer composition, destructive menu variants, accepted focus treatment, discoverable Tabs overflow and secured `/ui` production behavior.

### FOUND-001C4 — Utility, Feedback & Composition Core Pack
**Status: ACCEPTED + CLOSED — CANONICAL/FROZEN**

Accepted inventory:
- Alert
- Empty
- StatePanel
- Spinner
- Progress
- Toaster / typed `toast` boundary
- Item family
- ButtonGroup / ButtonGroupSeparator / ButtonGroupText
- InputGroup / InputGroupAddon / InputGroupText / InputGroupInput / InputGroupTextarea / InputGroupButton
- Kbd / KbdGroup
- Toggle / ToggleGroup
- Breadcrumb family

Verified accepted contracts:
- Progress forwards determinate values to Radix and supports visible/hidden accessible naming without requiring consumer IDs;
- Spinner uses reduced-motion-safe animation; decorative mode is hidden from assistive tech;
- InputGroup consumes FormField invalid/disabled state, uses nullish override semantics and `min-w-0`;
- InputGroupAddon supports visual `inline-start`, `inline-end`, `block-start`, `block-end` alignment while gallery evidence keeps the input/textarea first in DOM order;
- block-end textarea composition works without a parent `flex-col` gallery hack;
- InputGroupButton composes Core Button and inherits FormField disabled state;
- Empty sizes naturally, is motion-safe and StatePanel remains presentation-only;
- Toast uses Sonner 2.0.7 behind a typed Core-owned API with message/info/success/warning/error/loading/dismiss methods and Re:Solve action/status semantics;
- Item interaction is opt-in through `asChild`; structural rows remain noninteractive and media uses direct-child SVG sizing;
- ButtonGroup is programmatically nameable, separator orientation describes the rendered line, and ButtonGroupText is a noninteractive labelled composition primitive;
- Toggle pressed state has non-color feedback and ToggleGroup gallery roots are programmatically named;
- Breadcrumb keeps semantic nav/list/current-page behavior, asChild link support and narrow-safe wrapping;
- gallery preserves C1-C3 evidence and includes all accepted C4 evidence;
- no new dependency was added for C4; package state and temporary home route remained unchanged;
- `/ui` remains production guarded;
- no prompt/task leakage exists in current source.

Non-blocking known limitation accepted at C4 close:
- `Item` no longer contains the unsafe `as any` cast, but its public forwarded ref remains div-biased even when `asChild` renders another semantic element. Runtime/semantic behavior is correct; do not rely on polymorphic Item refs until this is revisited. A future widening/removal of that ref contract is allowed as a non-breaking Core hardening change.

## Current architecture facts
- TanStack Start v1 + Vite 8.2 + React 19.2.
- Bun 1.3.3 is the only package manager.
- Tailwind 4.2.1.
- shadcn source setup is initialized `new-york`; do not rerun init.
- Current primitive base: Radix + shadcn source components.
- Drawer: Vaul 1.1.2, pre-existing dependency first consumed in C3.
- Toast: Sonner 2.0.7, pre-existing dependency first consumed in C4.
- Icons: Lucide 0.575.0.
- Typography: Inter Variable + JetBrains Mono Variable via Fontsource 5.3.0.
- Query/server state: TanStack Query.
- Forms/validation available: React Hook Form + Zod.
- Chart foundation: Recharts; Tremor remains chart/composition influence.
- Testing stack: not configured.
- PWA tooling: not configured.
- Auth/domain setup: not yet implemented.

## UI-source direction
- Re:Solve Core is the public UI boundary; feature code must not bypass it casually.
- shadcn/ui is source-owned and normalized into Re:Solve.
- shadcn-vue is visual/composition/block reference only; never a Vue runtime dependency.
- Radix remains the current primitive base; no wholesale React Aria/Base UI migration.
- Untitled UI remains selectively incorporated/reference-driven.
- Tremor Raw remains selectively incorporated/reference-driven.
- Current React shadcn patterns are preferred over translating Vue equivalents when available.

## Planned future source intake
- Advanced inputs/scheduling: Combobox, OTP/PIN, Number Field, Tags Input, Slider, Calendar, Date Picker/Date Range, Pagination, Resizable and Stepper where justified.
- Questionnaire/review composition remains a higher-order form/review layer above FormField/FieldGroup, not a second forms framework.
- QR remains an approved utility/presentation candidate; security-sensitive QR flows must encode signed/short-lived references, never raw secrets.
- Conversation/Àríyá primitives remain later intake: Message, Bubble, Message Scroller, Attachment, Marker.
- Two-column image auth blocks remain the preferred desktop auth composition direction with deliberate single-column mobile transformation.
- Dashboard/sidebar blocks remain composition references only; Re:Solve navigation, Attention Engine, TanStack DataTable and Tremor/Recharts architecture remain authoritative.

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision.

## Known implementation limitations
- Item polymorphic ref typing caveat recorded above;
- advanced inputs/scheduling are not yet canonical;
- Questionnaire/review and QR exact implementations are not yet selected;
- conversation/Àríyá primitives, auth, application shell, PWA, CI and testing remain future FOUND-001 substeps.

## Next action
Begin bounded `FOUND-001C5A — Advanced Input Primitives`. Preserve frozen C1-C4 APIs. Implement only the first advanced-input subset, expand the Component Gallery, verify accessibility/responsiveness/provenance, and STOP for supervisor review before scheduling/date, Questionnaire, QR, shell or auth work.
