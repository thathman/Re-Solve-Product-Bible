# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5A ACCEPTED/FROZEN — SECURITY-MEM-001 ACCEPTED/CANONICAL — FOUND-001C5B CONDITIONAL (FINAL VISUAL/A11Y CLOSURE REQUIRED)**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — public, specification/planning only.
- Current Lovable app: `thathman/re-solve-c560d62c` — private, `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Lovable project
- Project Knowledge installed: YES.
- Canonical workspace Skills installed: YES — 30 Re:Solve skills + `self-host-check`.
- Platform default skill active: `design-taste-frontend`.
- Duplicate `.agents/skills/` drafts removed; obsolete `airix-*` skills absent.

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
TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3 + Tailwind 4.2.1. Radix-based shadcn source setup preserved. Environment/config, locale/currency, portability and provenance guardrails accepted.

### FOUND-001B — UI Stack & Design Tokens
**ACCEPTED + CLOSED**
Re:Solve semantic OKLCH tokens, light/dark/system theming, self-hosted Inter + JetBrains Mono, density/layout/elevation/focus/safe-area/motion contracts and shadcn compatibility mappings accepted.

Component Gallery contract:
- source: `src/routes/__dev/ui.tsx`;
- browser route: `/ui`;
- production guard: `beforeLoad` + `import.meta.env.PROD` redirect to `/`;
- local/non-production access intended.

### FOUND-001C1 — Core UI Primitive Foundation
**ACCEPTED / CANONICAL / FROZEN**
Button, IconButton, Badge, StatusBadge, ResolveAvatar, Tooltip, Separator, Skeleton, Metric, MetricDelta.

### FOUND-001C2 — Forms & Controls
**ACCEPTED / CANONICAL / FROZEN**
Input, Textarea, Checkbox, RadioGroup, Switch, Select, FormField, FieldGroup. Typed FormField context and ID/required/disabled/invalid/described-by semantics are canonical.

### FOUND-001C3 — Interaction & Overlay Pack
**ACCEPTED / CANONICAL / FROZEN**
Dialog, AlertDialog, Sheet/SheetBody, Drawer/DrawerBody, Popover, HoverCard, DropdownMenu, ContextMenu, Accordion, Collapsible, Tabs, ScrollArea/ScrollBar. Radix/shadcn base + Vaul Drawer accepted; overlay/safe-area/destructive/focus contracts frozen.

### FOUND-001C4 — Utility, Feedback & Composition Pack
**ACCEPTED / CANONICAL / FROZEN**
Alert, Empty, StatePanel, Spinner, Progress, typed Sonner Toast boundary, Item family, ButtonGroup family, InputGroup family, Kbd, Toggle/ToggleGroup and Breadcrumb accepted.

Known non-blocking limitation:
- Item's public forwarded ref remains div-biased when `asChild` renders another semantic element. Runtime/semantic behavior is accepted; do not reopen casually.

### FOUND-001C5A — Advanced Input Primitives I
**ACCEPTED / CANONICAL / FROZEN**
Command/CommandDialog, Combobox, NativeSelect family, InputOTP family and Slider are canonical. C5A uses pre-existing cmdk 1.1.1, input-otp 1.4.2 and @radix-ui/react-slider 1.3.6; no package was added. FormField integration, explicit Combobox clearing, OTP semantics, required Slider thumb naming, 24px thumbs, focus variables and production `/ui` guard are frozen.

Visual review:
- user-supplied dark desktop, light desktop and narrow/mobile Component Gallery captures passed C5A visual review.

## SECURITY-MEM-001 — Lovable Security Memory
**ACCEPTED / CANONICAL**
The supervisor-approved 13-rule security memory remains canonical. Do not modify it during C5B.

## Currency display convention
**CANONICAL**
- Internal/data/API currency identity remains explicit via ISO codes such as USD, GBP, EUR and NGN.
- Normal user-facing UI uses locale-appropriate currency symbols where unambiguous: `$`, `£`, `€`, `₦`, etc.
- No universal default currency is allowed; formatter callers must still provide an explicit currency code.
- Current gallery examples use `$42,850.00` and `$12,400.00`, not `USD ...`.

## FOUND-001C5B — Calendar, Date Selection, Pagination & Resizable
**STATUS: CONDITIONAL — FINAL VISUAL/A11Y CLOSURE REQUIRED**

### Current implementation
- Calendar using pre-existing `react-day-picker` 9.14.0;
- DatePicker and DateRangePicker composed from Core Button + Core Popover + Core Calendar;
- Pagination family with Slot/asChild capability;
- ResizablePanelGroup / ResizablePanel / ResizableHandle wrapping `react-resizable-panels` 4.6.5;
- explicit C5B exports through Core;
- Advanced Inputs II gallery exists;
- package/lock restored to pre-existing dependency set;
- C5B provenance exists.

### Verified FIX3 improvements
- runtime prompt/task leakage removed; `Port Range` restored exactly;
- DatePicker uses `PropsSingle`, DateRangePicker uses `PropsRange`; no `any` remains in their public/calendar boundary;
- locale is typed directly with date-fns `Locale`; no `unknown as Locale` cast remains;
- controlled/uncontrolled detection uses actual `value` prop presence;
- picker calendarProps are spread before Core-owned mode/selected/onSelect state;
- DateRange responsive month count remains Core-owned and starts narrow-safe at one month;
- calendar/picker gallery dates now use local calendar constructors such as `new Date(2026, 7, 12)` rather than ISO-string timestamps;
- DateRange maintenance/error/disabled-date evidence exists;
- disabled Next pagination evidence exists;
- Resizable public API uses v4 `orientation`, not legacy `direction`;
- gallery panel percentages use explicit strings such as `"25%"`;
- package.json and bun.lock declare `react-resizable-panels` as `^4.6.5`;
- Vitest is absent from package.json and current repository search;
- Metrics preserve symbol UI: `$42,850.00` and `$12,400.00`;
- `/ui` production guard remains intact;
- `src/routes/index.tsx` remains unchanged.

### Final verified blockers
1. **Standalone DatePicker gallery evidence is not programmatically named.** The example is preceded by visible text (`Accessible DatePicker`) but the DatePicker trigger has no `aria-label`, `aria-labelledby`, or FormField association. Add a real accessible name to this standalone example.
2. **Resizable nested orientation styling does not inherit the Separator's ARIA attribute.** `ResizableHandle` correctly applies `aria-[orientation=...]` variants on the Separator itself, but the nested visual line and grip also use same-element `aria-[orientation=...]` variants even though those children do not carry `aria-orientation`. Use a parent-state mechanism (`group` + `group-aria-*`, an equivalent parent selector, or another truthful v4 approach) so the nested line/grip actually respond to the Separator orientation.
3. **ResizablePanelGroup still adds `flex` class despite v4 owning layout.** Official v4 documentation states Group owns `display`, `flex-direction`, `flex-wrap`, and `overflow`. Remove the redundant manual `flex` class; keep only safe size/visual classes such as `h-full w-full` if desired.
4. **Calendar evidence is not fully deterministic across time.** The examples use fixed August 2026 selected dates but do not set a fixed `defaultMonth`/`month`, so DayPicker can open on the current month in a future review. Set August 2026 as the initial displayed month, and set a deterministic `today` (e.g. Aug 8, 2026) where today-vs-selected evidence is required.

### Review classification
C5B is otherwise acceptable. One final tiny closure pass should touch only `Resizable.tsx` and the C5B gallery (plus provenance only if wording becomes inaccurate), then stop for review. No package, picker architecture, formatter, security-memory, or frozen C1-C5A changes are needed.

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
- Testing stack remains not canonical/configured.
- PWA/auth/domain implementation remains later work.

## UI source direction
- Re:Solve Core is the public UI boundary.
- Keep the established Radix foundation; no wholesale Base UI/React Aria migration.
- shadcn-vue remains visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.

## Planned later work
- Later advanced input/composition slices may address Number Field, Tags Input, Stepper, Questionnaire and QR where justified.
- Questionnaire/review remains a higher-order composition above FormField/FieldGroup, not a second forms framework.
- Security-sensitive QR uses signed/scoped/short-lived references only.
- Conversation/Àríyá, auth, dashboard, shell, PWA, CI and testing remain later FOUND-001 work.

## Next action
Execute the supervisor-provided final C5B visual/accessibility closure only. Re-review before acceptance. Do not begin another C5 slice.