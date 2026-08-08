# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5B ACCEPTED/FROZEN — SECURITY-MEM-001 ACCEPTED/CANONICAL**

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
Command/CommandDialog, Combobox, NativeSelect family, InputOTP family and Slider are canonical. C5A uses pre-existing cmdk 1.1.1, input-otp 1.4.2 and @radix-ui/react-slider 1.3.6.

### FOUND-001C5B — Calendar, Date Selection, Pagination & Resizable
**ACCEPTED / CANONICAL / FROZEN**
Calendar, DatePicker, DateRangePicker, Pagination family and ResizablePanelGroup/ResizablePanel/ResizableHandle are canonical.

Accepted C5B contracts:
- React DayPicker 9.14.0 + date-fns 4.1.0 remain the date foundation;
- picker values stay calendar-date oriented; no implicit UTC/ISO serialization;
- DatePicker uses typed single-mode DayPicker composition; DateRangePicker uses typed range-mode composition;
- controlled/uncontrolled detection is based on actual `value` prop presence;
- DateRangePicker is narrow-first at one month and enhances at desktop/tablet;
- Pagination is semantic, router-agnostic through `asChild`, and disabled Previous/Next are true non-links;
- react-resizable-panels v4.6.5 is used through Group/Panel/Separator with canonical `orientation`, explicit percentage string sizing where intended, library-owned Group layout, parent `group-aria-*` separator styling and stacked mobile fallback;
- Resizable vertical separator geometry is narrow/full-height with col-resize; horizontal separator geometry is short/full-width with row-resize;
- Slider exact-optional typing uses conditional prop spreading with no `any`/unknown casts;
- deterministic August 2026 gallery evidence is accepted;
- standalone DatePicker has an explicit accessible name;
- package/lock remain on the pre-existing dependency set; no C5B dependency was added;
- `/ui` production guard and home route remain unchanged.

Lovable reported `bun install --frozen-lockfile`, build, lint and `tsc --noEmit` passing. GitHub source review verified the resulting contracts; GitHub review does not independently execute Bun.

## SECURITY-MEM-001 — Lovable Security Memory
**ACCEPTED / CANONICAL**
Supervisor-approved 13-rule security memory remains canonical unless Lovable surfaces changed text. Do not reopen merely because a completion message says the memory was updated.

## Currency display convention
**CANONICAL**
- Internal/data/API currency identity remains explicit via ISO codes.
- Normal user-facing UI uses locale-appropriate currency symbols where unambiguous.
- No universal default currency.
- Gallery examples use `$42,850.00` and `$12,400.00`.

## Current architecture facts
- TanStack Start v1 + Vite 8.2 + React 19.2.
- Bun 1.3.3 canonical package manager.
- Tailwind 4.2.1.
- shadcn source setup `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- Drawer: Vaul 1.1.2.
- Toast: Sonner 2.0.7.
- Command: cmdk 1.1.1.
- OTP: input-otp 1.4.2.
- Slider: @radix-ui/react-slider 1.3.6.
- Calendar/date foundation: react-day-picker 9.14.0 + date-fns 4.1.0.
- Resizable foundation: react-resizable-panels 4.6.5.
- Testing stack not canonical/configured.
- PWA/auth/domain implementation remains later work.

## UI source direction
- Re:Solve Core is the public UI boundary.
- Keep the established Radix foundation; no wholesale Base UI/React Aria migration.
- shadcn-vue remains visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.

## Planned later work
- Additional Core composition/display primitives remain before shell work.
- Number Field and Tags Input are not current official React shadcn primitives; any future React port requires explicit source/type review rather than copying Vue code.
- Questionnaire/review remains a higher-order composition above FormField/FieldGroup, not a second forms framework.
- Security-sensitive QR uses signed/scoped/short-lived references only.
- Conversation/Àríyá, auth, dashboard, shell, PWA, CI and testing remain later FOUND-001 work.

## Next action
Proceed only with the next supervisor-issued FOUND-001C slice. Do not rename repositories or begin shell/auth/domain work yet.