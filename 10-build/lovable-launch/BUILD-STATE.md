# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5A ACCEPTED/FROZEN — SECURITY-MEM-001 ACCEPTED/CANONICAL — FOUND-001C5B CONDITIONAL (FINAL TWO-ISSUE CLOSURE REQUIRED)**

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

## SECURITY-MEM-001 — Lovable Security Memory
**ACCEPTED / CANONICAL**
Supervisor-approved 13-rule security memory remains canonical.

## Currency display convention
**CANONICAL**
- Internal/data/API currency identity remains explicit via ISO codes.
- Normal user-facing UI uses locale-appropriate currency symbols where unambiguous.
- No universal default currency.
- Current gallery examples use `$42,850.00` and `$12,400.00`.

## FOUND-001C5B — Calendar, Date Selection, Pagination & Resizable
**STATUS: CONDITIONAL — FINAL TWO-ISSUE CLOSURE REQUIRED**

### Verified current improvements
- Port Range prompt leakage is gone and label is exactly `Port Range`.
- Standalone DatePicker now has `aria-label="Target date"`.
- Calendar evidence is deterministic August 2026: fixed default month and explicit today/selected states.
- DatePicker uses `PropsSingle`; DateRangePicker uses `PropsRange`; no `any` remains in their picker boundary.
- Picker controlled/uncontrolled detection uses actual prop presence.
- Calendar dates use local calendar constructors, not ISO date-string parsing.
- DateRange maintenance/error/disabled-date evidence exists.
- Pagination disabled Previous/Next evidence and asChild evidence exist.
- Resizable public API uses v4 `orientation` and gallery sizes use percentage strings.
- Resizable Group wrapper no longer adds manual flex/flex-col; it keeps only safe size classes.
- Resizable nested line/grip now use parent `group-aria-*` state instead of same-element ARIA selectors.
- package.json/bun.lock use `react-resizable-panels ^4.6.5`; Vitest absent.
- `/ui` guard and home route remain unchanged.

### Remaining verified blockers
1. **Frozen Slider now contains two `as any` casts.** `src/components/core/inputs/Slider.tsx` constructs `rootProps` with `value: value as any` and `defaultValue: defaultValue as any` to satisfy `exactOptionalPropertyTypes`. This weakens the accepted C5A type boundary and is unnecessary. Solve exact-optional typing by conditionally spreading only defined `value` / `defaultValue` props (or another fully typed approach) instead of casting to `any`. C5A remains frozen except for this hygiene repair introduced during C5B closure.
2. **Resizable separator geometry is reversed relative to its actual ARIA orientation.** Current `aria-orientation="vertical"` classes produce an 8px-high/full-width row-resize target and horizontal line; current `aria-orientation="horizontal"` classes produce an 8px-wide/full-height col-resize target and vertical line. WAI-ARIA separator orientation describes the separator itself. A vertical separator must be a vertical divider (narrow width/full height, col-resize); a horizontal separator must be a horizontal divider (short height/full width, row-resize). Swap the root target geometry, child line geometry, and grip rotation accordingly while keeping parent `group-aria-*` propagation.

### Source verification notes
- `tsconfig.json` has `exactOptionalPropertyTypes: true`.
- Official react-resizable-panels v4 docs confirm Group owns `display`, `flex-direction`, `flex-wrap`, and `overflow`; v4 uses `orientation`; numeric Panel sizes are pixels and percentage examples should use strings.
- Lovable reports build/lint/`tsc --noEmit` passing. Source-level supervisor review does not independently execute Bun through GitHub.

### Review classification
C5B is otherwise ready. One narrow correction should touch only `Slider.tsx` and `Resizable.tsx`, then stop for final review. No gallery, package, picker, pagination, formatter, provenance, security-memory or home-route changes are required unless a compile error proves otherwise.

## Current architecture facts
- TanStack Start v1 + Vite 8.2 + React 19.2.
- Bun 1.3.3 canonical package manager.
- Tailwind 4.2.1.
- shadcn source setup `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- Calendar/date foundation: react-day-picker 9.14.0 + date-fns 4.1.0.
- Resizable foundation: react-resizable-panels 4.6.5.
- Testing stack not canonical/configured.

## Next action
Execute the supervisor-provided final Slider type-hygiene + Resizable orientation-geometry correction only. Re-review before acceptance. Do not begin another slice.