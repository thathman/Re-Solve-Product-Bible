# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5B ACCEPTED/FROZEN — FOUND-001C5C CONDITIONAL — SECURITY-MEM-001 ACCEPTED/CANONICAL**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — public, specification/planning only.
- Current Lovable app: `thathman/re-solve-c560d62c` — private, `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Lovable project
- Project Knowledge installed: YES.
- Canonical workspace Skills installed: YES — 30 Re:Solve skills + `self-host-check`.
- Platform default skill active: `design-taste-frontend`.

## Backend state
- Lovable Cloud enabled for development.
- Custom database tables: none.
- RLS policies: none.
- Migrations: not initialized.
- Demo seed/reset: not initialized.
- Auth/domain implementation: not yet built.

Never store credentials/secrets in this file.

## Accepted foundation

### FOUND-001A — Stack & Repository Foundation
**ACCEPTED**
TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3 + Tailwind 4.2.1. Radix-based shadcn source setup preserved.

### FOUND-001B — UI Stack & Design Tokens
**ACCEPTED + CLOSED**
Re:Solve semantic OKLCH tokens, light/dark/system theming, typography, density/layout/elevation/focus/safe-area/motion contracts and shadcn compatibility mappings accepted.

Component Gallery:
- source: `src/routes/__dev/ui.tsx`;
- browser route: `/ui`;
- production guard: `beforeLoad` + `import.meta.env.PROD` redirect to `/`.

### FOUND-001C1 — Core UI Primitive Foundation
**ACCEPTED / CANONICAL / FROZEN**
Button, IconButton, Badge, StatusBadge, ResolveAvatar, Tooltip, Separator, Skeleton, Metric, MetricDelta.

### FOUND-001C2 — Forms & Controls
**ACCEPTED / CANONICAL / FROZEN**
Input, Textarea, Checkbox, RadioGroup, Switch, Select, FormField, FieldGroup.

### FOUND-001C3 — Interaction & Overlay Pack
**ACCEPTED / CANONICAL / FROZEN**
Dialog, AlertDialog, Sheet/SheetBody, Drawer/DrawerBody, Popover, HoverCard, DropdownMenu, ContextMenu, Accordion, Collapsible, Tabs, ScrollArea/ScrollBar.

### FOUND-001C4 — Utility, Feedback & Composition Pack
**ACCEPTED / CANONICAL / FROZEN**
Alert, Empty, StatePanel, Spinner, Progress, typed Sonner Toast boundary, Item family, ButtonGroup family, InputGroup family, Kbd, Toggle/ToggleGroup and Breadcrumb.

Known non-blocking limitation:
- Item public forwarded ref remains div-biased when `asChild` renders another semantic element.

### FOUND-001C5A — Advanced Input Primitives I
**ACCEPTED / CANONICAL / FROZEN**
Command/CommandDialog, Combobox, NativeSelect family, InputOTP family and Slider are canonical.

### FOUND-001C5B — Calendar, Date Selection, Pagination & Resizable
**ACCEPTED / CANONICAL / FROZEN**
Calendar, DatePicker, DateRangePicker, Pagination family and ResizablePanelGroup/ResizablePanel/ResizableHandle are canonical. Date-only semantics, typed picker modes, responsive range month count, router-agnostic Pagination, v4 Resizable orientation/geometry, conditional Slider prop spreading, deterministic August 2026 gallery evidence and no-new-dependency package state are frozen.

## FOUND-001C5C — Core Display Primitives
**STATUS: CONDITIONAL — NARROW NORMALIZATION REQUIRED**

### Current implementation present on app `main`
- `Card`, `CardHeader`, `CardTitle`, `CardDescription`, `CardContent`, `CardFooter`, `CardAction`;
- Card variants: default, raised, subtle, interactive, with `asChild` semantic composition;
- native semantic `Table` family with bounded horizontal-scroll wrapper;
- thin `AspectRatio` wrapper around pre-existing `@radix-ui/react-aspect-ratio`;
- explicit C5C exports added to Core boundary;
- `Display Primitives` gallery exists with Card, Table and AspectRatio evidence;
- currency evidence follows canonical symbol display;
- no C5C dependency was reported or observed.

### Verified strengths
- default Card is quiet/bordered; raised uses accepted level-1 elevation;
- interactive Card gallery uses an actual anchor through `asChild`, not click-only div semantics;
- Table retains native table/thead/tbody/tfoot/tr/th/td/caption semantics;
- table horizontal overflow is contained by the Table wrapper;
- gallery includes header/body/footer/caption, numeric right alignment, `$` currency values and narrow constrained table evidence;
- AspectRatio is a thin Radix wrapper and gallery images carry meaningful alt text;
- C5C exports are explicit for the newly added families;
- existing C1-C5B gallery evidence remains present.

### Remaining verified blockers
1. **Interactive Card uses a noncanonical focus ring.** `Card.tsx` uses `focus-visible:ring-2`, `focus-visible:ring-rs-action-primary`, and fixed offset utilities. Replace these with the frozen Re:Solve focus-variable contract: `--rs-focus-ring-width`, `--rs-focus-ring-color`, `--rs-focus-offset-width`, `--rs-focus-offset-color`.
2. **Static Table rows receive hover styling by default.** `TableRow` applies `hover:bg-rs-surface-subtle/30` to every row, including static display-only rows. Static rows must not imply clickability. Remove default hover treatment or gate it behind an explicit opt-in state/variant without introducing DataTable behavior.
3. **AspectRatio provenance is underspecified.** `docs/ui-sources.md` lists Aspect Ratio under shadcn and Radix generically, but C5C should explicitly record the pre-existing runtime `@radix-ui/react-aspect-ratio` (currently 1.1.8), MIT license, and first Re:Solve Core consumption in C5C. Keep shadcn pattern provenance separate from runtime package provenance.

### Review classification
C5C architecture is accepted in direction but not frozen yet. Apply one narrow normalization pass touching Card, Table and provenance only. Do not redesign the gallery or introduce DataTable.

## SECURITY-MEM-001 — Lovable Security Memory
**ACCEPTED / CANONICAL**
Supervisor-approved 13-rule security memory remains canonical unless Lovable surfaces changed text. Do not reopen merely because a completion message says the memory was updated.

## Currency display convention
**CANONICAL**
- Internal/data/API currency identity remains explicit via ISO codes.
- Normal user-facing UI uses locale-appropriate currency symbols where unambiguous.
- No universal default currency.
- Gallery examples use symbols such as `$42,850.00`.

## Current architecture facts
- TanStack Start v1 + Vite 8.2 + React 19.2.
- Bun 1.3.3 canonical package manager.
- Tailwind 4.2.1.
- shadcn source setup `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- Calendar/date foundation: react-day-picker 9.14.0 + date-fns 4.1.0.
- Resizable foundation: react-resizable-panels 4.6.5.
- AspectRatio foundation: @radix-ui/react-aspect-ratio 1.1.8, pre-existing dependency.
- Testing stack not canonical/configured.

## UI source direction
- Re:Solve Core is the public UI boundary.
- Keep the established Radix foundation; no wholesale Base UI/React Aria migration.
- shadcn-vue remains visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.

## Planned later work
- DataTable remains a separate later supervised system; do not fold it into simple Table.
- Additional higher-order composition primitives remain before shell work.
- Questionnaire/review remains above FormField/FieldGroup, not a second forms framework.
- Security-sensitive QR uses signed/scoped/short-lived references only.
- Conversation/Àríyá, auth, dashboard, shell, PWA, CI and testing remain later FOUND-001 work.

## Next action
Execute only the supervisor-issued C5C normalization correction. Re-review before acceptance. Do not begin DataTable or another C5 slice.