# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5A ACCEPTED/FROZEN — SECURITY-MEM-001 ACCEPTED/CANONICAL — FOUND-001C5B CONDITIONAL (CORRECTION REQUIRED)**

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

The user replaced Lovable `@security-memory` with the supervisor-approved rules and read the result back in chat. No secret material was detected.

Canonical principles include server-controlled authorization, intentional RLS on Data-API-exposed tables, least-privilege grants, server-only service-role credentials, SECURITY INVOKER by default, narrowly constrained SECURITY DEFINER, server-boundary authn/authz, createServerFn for same-origin typed RPC, server routes for external/protocol HTTP surfaces, runtime validation of untrusted server input, preserved TanStack Start CSRF middleware, Vault secret minimization, signed/scoped/short-lived security-sensitive QR references, migration-controlled security configuration and log/error redaction.

Do not implement auth/database systems merely because the memory is canonical; the rules constrain later slices.

## FOUND-001C5B — Calendar, Date Selection, Pagination & Resizable
**STATUS: CONDITIONAL — CORRECTION REQUIRED BEFORE ACCEPTANCE**

### Current implementation present on app `main`
- `src/components/core/calendar/Calendar.tsx` using pre-existing react-day-picker 9.14.0;
- `DatePicker.tsx` composed from Core Popover + Core Button + Core Calendar;
- `DateRangePicker.tsx` using React DayPicker `DateRange`;
- `Pagination.tsx`;
- `Resizable.tsx` using pre-existing react-resizable-panels 4.6.5;
- C5B families currently export through `src/components/core/index.ts`;
- provenance entries for react-day-picker, date-fns and react-resizable-panels are present.

### Positive findings
- Calendar is Re:Solve-tokenized and uses React DayPicker rather than a parallel calendar library;
- no `toISOString()`/UTC serialization logic was found in C5B;
- selected range uses Re:Solve action/selected surfaces and disabled/outside states are distinct;
- DatePicker/DateRangePicker use Core Popover + Core Button + Core Calendar;
- Pagination exposes `nav aria-label="Pagination"` and active-page `aria-current`;
- Resizable uses the correct v4 primitive names `Group`, `Panel`, `Separator` under the Re:Solve wrapper;
- provenance correctly records pre-existing react-day-picker 9.14.0, date-fns 4.1.0 and react-resizable-panels 4.6.5 with MIT licenses.

### Verified blockers / corrections required
1. **C5B gallery is missing.** `src/routes/__dev/ui.tsx` imports none of Calendar, DatePicker, DateRangePicker, Pagination or Resizable and has no `Advanced Inputs II` section. The implementation report's gallery-complete claim is false.
2. **Prompt/task leakage has reappeared in runtime source.** The C5A Port Range label contains user/Lovable instruction text (`Do not make any visual modifications...`). Remove it and restore the accepted `Port Range` label. Search current source for instruction/task leakage before closure.
3. **Unexpected package/test drift violates the C5B dependency contract.** `vitest` was added to `package.json` and `bun.lock`, and `src/lib/formatters/formatters.test.ts` was added even though C5B required no dependencies/testing-stack changes. Remove this drift and restore package/bun state to the accepted C5A baseline.
4. **Frozen formatter/Metric evidence drifted out of scope.** `formatCurrency` behavior was changed and the accepted Metric gallery strings were replaced with runtime symbol formatting. Restore `src/lib/formatters/index.ts` and the C1 Metric gallery evidence to the accepted C5A baseline; C5B did not authorize formatter or Metric changes.
5. **Core index was broadly rewritten.** C5B replaced many explicit frozen exports with `export *`, unintentionally widening the public Core boundary. Restore the accepted C5A index/export style and add only the new C5B public exports.
6. **DatePicker/FormField merging uses `||` instead of nullish precedence.** `id`, disabled, invalid and required must use caller-provided values first and FormField fallback via `??` where false/empty overrides are meaningful.
7. **DatePicker invalid border uses the soft danger surface token as a border.** Use `rs-status-danger-foreground` for invalid border/focus semantics.
8. **DatePicker controlled-empty behavior is fragile.** `value !== undefined` cannot represent a controlled picker whose value is intentionally `undefined` after clearing. Establish a coherent controlled/uncontrolled contract that does not switch modes when a controlled value becomes empty.
9. **DatePicker has an unused `DayPicker` type import.** Remove dead imports and ensure lint/type clean.
10. **DateRangePicker repeats the same `||`/invalid-token/controlled-empty issues.** Normalize consistently with DatePicker.
11. **DateRangePicker contains `calendarProps as any`.** Remove the `any` cast and model range-calendar props truthfully using React DayPicker range types or a typed branch for required/optional range mode.
12. **DateRangePicker is not truly mobile-first.** It initializes with the requested desktop month count (default 2) and only switches to one month after a client effect. Initialize narrow-safe (one month) and enhance to multiple months after a safe media-query check so first narrow render cannot briefly squeeze/overflow two months.
13. **Picker display formatting does not honor Calendar locale.** Calendar accepts locale/timeZone passthrough, but trigger text uses date-fns default locale. At minimum, apply `calendarProps.locale` to display formatting. Do not add UTC serialization/timezone conversion logic.
14. **Pagination is not router-compatible as required.** `PaginationLink` is hard-coded to `<a>` and has no `asChild`/Slot composition contract for TanStack Router links. Add router-compatible composition without coupling to routing.
15. **Disabled Pagination Previous/Next remain anchors.** `pointer-events-none` + `tabIndex=-1` is visual/interaction suppression, not a truly noninteractive disabled control. Render a non-link disabled state or otherwise make activation impossible while preserving `aria-disabled`.
16. **Resizable uses a stale v3 direction selector.** `data-[panel-group-direction=vertical]` no longer matches react-resizable-panels v4. Current v4 uses Group orientation behavior and WAI-ARIA `aria-orientation` on Separator. Normalize wrapper styling to the v4 contract.
17. **Resizable handle target is too thin/under-specified.** Current separator is effectively a 1px line and the pseudo-element hit-area classes do not establish a real pseudo-element. Give the separator a discoverable pointer target while keeping a restrained visual line/optional grip, visible focus and correct orientation styling.
18. **Resizable uses generic `shadow-sm` on the grip.** Use no shadow or accepted Re:Solve elevation.
19. **Responsive Resizable fallback is unproven because the gallery is absent.** C5B gallery must show resizable panels at tablet/desktop and an intentional stacked narrow fallback rather than draggable phone panes.
20. **Security memory was previously accepted and is not source-controlled.** The latest user says it was updated again but did not provide the resulting text. Do not modify it during the C5B fix; return the current memory text for supervisor comparison, with secrets redacted if any exist.

### Review classification
C5B architecture is usable and should be corrected in place. Do not tear down React DayPicker or react-resizable-panels. One bounded fix should restore scope hygiene, complete gallery evidence, normalize picker state/FormField contracts, add router-compatible Pagination, update Resizable to its actual v4 semantics and then stop for review.

## Current architecture facts
- TanStack Start v1 + Vite 8.2 + React 19.2.
- Bun 1.3.3 is the canonical package manager.
- Tailwind 4.2.1.
- shadcn source setup: `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- `src/start.ts` explicitly includes TanStack Start CSRF middleware for server functions.
- Drawer: Vaul 1.1.2.
- Toast: Sonner 2.0.7.
- Command: cmdk 1.1.1.
- OTP: input-otp 1.4.2.
- Slider: @radix-ui/react-slider 1.3.6.
- Calendar/date foundation: react-day-picker 9.14.0 + date-fns 4.1.0.
- Resizable foundation: react-resizable-panels 4.6.5.
- Icons: Lucide 0.575.0.
- Typography: Inter Variable + JetBrains Mono Variable via Fontsource 5.3.0.
- Query/server state: TanStack Query.
- Forms/validation available: React Hook Form + Zod.
- Chart foundation: Recharts.
- Testing stack remains **not canonical/configured**; the current C5B-added Vitest drift must be removed before C5B close.
- PWA/auth/domain implementation: not yet configured/built.

## UI source direction
- Re:Solve Core is the public UI boundary.
- Current React shadcn Radix-compatible patterns are preferred where compatible with the existing project.
- Keep the established Radix foundation; no wholesale Base UI/React Aria migration.
- shadcn-vue remains visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.

## Planned later work
- Later advanced input/composition slices may address Number Field, Tags Input, Stepper, Questionnaire and QR where justified.
- Questionnaire/review remains a higher-order composition above FormField/FieldGroup, not a second forms framework.
- Security-sensitive QR uses signed/scoped/short-lived references only.
- Conversation/Àríyá, auth, dashboard, shell, PWA, CI and testing remain later FOUND-001 work.

## Next action
Execute the supervisor-provided `FOUND-001C5B-FIX` only. Restore frozen scope, correct C5B contracts, add the missing Advanced Inputs II gallery evidence, return the current security-memory text without changing it, and STOP for supervisor review.