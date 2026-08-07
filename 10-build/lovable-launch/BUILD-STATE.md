# Re:Solve Lovable Build State

Keep this file updated after each accepted build slice so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED + CLOSED — FOUND-001C1 ACCEPTED — FOUND-001C2 ACCEPTED + CLOSED — FOUND-001C3 CONDITIONAL (FINAL CONTRACT CLEANUP REQUIRED)**

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
- Lovable embedded Preview has previously evaluated production-like, so supervised visual review may temporarily require explicit exposure.

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

### FOUND-001C2 — Canonical form and control primitives
**Status: ACCEPTED + CLOSED — CANONICAL/FROZEN FOR DOWNSTREAM USE**

Supervisor verified on application `main` and owner accepted the rendered visual result:
- C2 components remain under `src/components/core/forms/` and are exported through `@/components/core`;
- accepted C2 set: Input, Textarea, Checkbox, RadioGroup / RadioGroupItem, Switch, Select family, FormField and FieldGroup;
- FormField uses typed context rather than cloneElement injection;
- Input/Textarea consume field control ID, described-by, invalid, required and disabled semantics while still supporting standalone use;
- FormField renders description and error together when both exist so every ID in `aria-describedby` maps to a real node;
- FieldGroup preserves fieldset/legend semantics and likewise renders/associates description and error consistently;
- Checkbox Root itself is 24×24 and supports checked/indeterminate/disabled states;
- RadioGroupItem itself is 24×24;
- Switch Root itself is 24px high with coherent thumb sizing/movement;
- Input/Textarea and Select triggers keep 16px text on narrow/mobile viewports and reduce typography only from the larger breakpoint;
- form controls use accepted Re:Solve token vocabulary and explicit accepted focus-variable contract;
- invalid/error treatment uses `rs-status-danger-foreground`;
- Select is a Re:Solve wrapper around Radix Root and consumes FormField required/disabled context;
- SelectTrigger consumes field ID, described-by, invalid, required and disabled semantics;
- gallery includes selected Select, required placeholder/error Select, disabled trigger, disabled option and a long option label;
- gallery Switch labels use stable IDs/htmlFor association and explicit disabled text styling;
- gallery includes FieldGroup description + error evidence;
- Untitled UI influence for C2 remains DESIGN REFERENCE ONLY;
- no new dependencies or lockfiles were introduced;
- owner accepted visual hierarchy/readability/responsiveness for C2;
- Lovable reports build/lint/type success with only existing Fast Refresh warnings.

### FOUND-001C2 closure
- `/ui` was temporarily exposed for supervised visual review.
- Supervisor verified the owner-requested production guard is restored in `src/routes/__dev/ui.tsx` using TanStack `beforeLoad` + `import.meta.env.PROD` redirect to `/`.
- Production `/ui` is therefore re-secured before C3.
- Local/non-production development access remains the intended Component Gallery workflow.

C2 APIs are canonical and frozen for downstream use.

## FOUND-001C3 — Interaction & Overlay Core UI Pack
**Status: CONDITIONAL — FINAL CONTRACT CLEANUP REQUIRED BEFORE C4**

### Verified C3 implementation now present after normalization fix
Supervisor verified on application `main`:
- Core C3 public boundary exists under `src/components/core/overlays/`, `src/components/core/disclosure/` and `src/components/core/utils/`;
- `@/components/core` exports Dialog, AlertDialog, Sheet, Drawer, Popover, HoverCard, DropdownMenu, ContextMenu, Accordion, Collapsible, Tabs and ScrollArea families;
- shared Re:Solve backdrop token now exists as `--rs-backdrop`, mapped to `bg-rs-backdrop`, with restrained light/dark scrim opacity;
- Dialog and AlertDialog now use `bg-rs-surface-raised`, `shadow-rs-overlay`, constrained mobile width/max-height and 200ms transition timing;
- AlertDialog action/cancel styling now consumes canonical Core Button `buttonVariants` instead of stock low-level shadcn button variants;
- Sheet now uses Re:Solve surface/backdrop/elevation, 200ms close / 300ms open timing, flex-column composition and exported `SheetBody` for independent scrolling;
- Sheet gallery no longer uses an absolutely positioned footer and instead composes Header → SheetBody → Footer;
- Drawer now uses the shared backdrop, Re:Solve raised/border/elevation treatment and bottom safe-area padding on its footer;
- Popover and HoverCard use Re:Solve raised surface/border/elevation treatment;
- DropdownMenu and ContextMenu now expose a `variant="destructive"` item API and gallery examples use it;
- Accordion trigger and Tabs use the accepted explicit focus-ring contract;
- ScrollArea thumb uses Re:Solve border semantics;
- `/ui` remains protected by the accepted production `beforeLoad` redirect guard;
- no Vue runtime/package exists;
- no new dependency was added by the normalization fix; `vaul ^1.1.2` remains a pre-existing dependency first consumed by Drawer in C3.

### Remaining verified C3 findings
1. **Destructive menu variants use the wrong semantic text token.** `DropdownMenuItem` and `ContextMenuItem` currently use `text-rs-status-danger` and `focus:text-rs-status-danger`; `rs-status-danger` is the soft status surface. Destructive text must use the high-contrast `rs-status-danger-foreground`, with the soft danger surface reserved for background/focus treatment.
2. **Tabs still hides its overflow affordance.** `TabsList` itself still contains `overflow-x-auto no-scrollbar`, so the canonical component hides the scrollbar even though the FIX explicitly required discoverable horizontal overflow.
3. **Horizontal ScrollArea evidence is still absent.** The Component Gallery demonstrates only vertical `ScrollArea`; it does not import/use `ScrollBar` or demonstrate a visible horizontal scrollbar.
4. **Drawer max-height/scroll-body contract is incomplete.** `DrawerContent` remains `h-auto` without a sensible viewport max-height or canonical independently scrollable body. The C3 contract requires long drawer content to remain usable on small screens while footer/actions and safe areas remain coherent.
5. **Sheet safe-area treatment is incomplete.** The new structural composition is correct, but `SheetFooter`/right-side content do not yet explicitly respect bottom/right safe-area variables as required by the C3 contract.
6. **Provenance still omits the pre-existing/first-consumed distinction for Vaul.** `docs/ui-sources.md` lists Vaul 1.1.2 as a Drawer dependency, but must state that the dependency existed before C3 and was first consumed by Re:Solve Drawer in C3. The shadcn C3 component list should also record the Drawer wrapper pattern explicitly.
7. **One accepted C2 gallery detail regressed.** The disabled `Terms accepted` label again uses `disabled:opacity-50` on a `<label>`, which cannot reflect sibling disabled state. Restore explicit `text-rs-text-disabled` and do not reopen the C2 API.

### Review classification
The C3 normalization is substantially correct and does not require another broad normalization pass. Execute one final narrow C3 cleanup covering only the seven findings above. If clean, C3 can be accepted/frozen and C4 can begin.

## shadcn ecosystem direction now canonical
- `shadcn-vue` is approved as a visual/composition/block-pattern source only; Re:Solve remains React/TanStack and must use React shadcn equivalents where available rather than Vue runtime code.
- approved future intake includes core interaction primitives, advanced controls, conversation/Àríyá primitives, questionnaire/review-style composition and QR presentation patterns subject to exact source verification.
- two-column form + cover-image auth blocks are the preferred composition reference for desktop login/signup/recovery/OTP/step-up surfaces with a deliberate single-column mobile transformation.
- shadcn dashboard blocks are approved composition references but do not override Re:Solve dashboard, Attention Engine, TanStack DataTable, Tremor/Recharts or navigation architecture.

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
- shadcn/ui: incorporated/source-owned starter foundation; C3 visual normalization is now materially present, with a final overflow/destructive-token cleanup pending.
- shadcn-vue: approved pattern/block reference only; never a runtime dependency.
- Radix: incorporated beneath current shadcn and Core components.
- Vaul: pre-existing dependency first consumed by Drawer in C3; MIT; raised/backdrop/safe-area normalization now present, max-height/scroll-body completion pending.
- Lucide: incorporated as primary icon family.
- Untitled UI React: material Avatar incorporation accepted in C1; C2 form composition is design reference only.
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

Accepted/frozen C2:
- Input
- Textarea
- Checkbox
- RadioGroup / RadioGroupItem
- Switch
- Select family
- FormField
- FieldGroup

C3 exists but is not canonical/frozen yet:
- Dialog
- AlertDialog
- Sheet / SheetBody
- Drawer
- Popover
- HoverCard
- DropdownMenu
- ContextMenu
- Accordion
- Collapsible
- Tabs
- ScrollArea

## Current database/domain inventory
None.

## Open Product Bible deltas
None requiring an owner product decision.

## Known implementation limitations
- C3 requires one final narrow contract cleanup before acceptance;
- questionnaire/review and QR patterns are approved future source candidates but exact React/source implementations have not yet been selected;
- auth, application states and broader composites remain future FOUND-001 substeps by design;
- shell, PWA, CI and test foundation remain future FOUND-001 substeps by design.

## Next action
Execute supervisor-provided `FOUND-001C3-FIX2` only: correct destructive menu foreground semantics, make Tabs overflow discoverable, add horizontal ScrollArea evidence, complete Drawer max-height/scroll-body and Sheet safe-area contracts, correct Vaul/shadcn provenance wording, and restore the disabled C2 gallery label styling. Re-review repository afterward. Do not begin FOUND-001C4.