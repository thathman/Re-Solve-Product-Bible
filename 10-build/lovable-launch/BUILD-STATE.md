# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5A ACCEPTED/FROZEN — SECURITY-MEM-001 ACCEPTED/CANONICAL — FOUND-001C5B CONDITIONAL (FINAL CONTRACT/HYGIENE FIX REQUIRED)**

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
**STATUS: CONDITIONAL — FINAL CONTRACT/HYGIENE FIX REQUIRED**

### Current implementation present on app `main`
- Calendar using pre-existing `react-day-picker` 9.14.0;
- DatePicker and DateRangePicker composed from Core Button + Core Popover + Core Calendar;
- Pagination family with Slot/asChild capability;
- ResizablePanelGroup / ResizablePanel / ResizableHandle wrapping `react-resizable-panels` 4.6.5;
- explicit C5B exports through the Core public boundary;
- Advanced Inputs II gallery section exists;
- C5B provenance entries exist.

### Verified improvements in the latest closure
- Metrics gallery now has the intended five examples and uses `$42,850.00` / `$12,400.00` symbol display;
- DatePicker and DateRangePicker now use real prop-presence detection (`hasOwnProperty`) for controlled vs uncontrolled state;
- DateRangePicker initializes narrow-safe at one month and enhances via `matchMedia`;
- Pagination disabled Previous/Next render non-link spans and have accessible labels;
- Pagination asChild composition exists;
- Calendar gallery now uses deterministic August 2026 sample dates and includes an unavailable-date example;
- standalone/default-selected DatePicker evidence exists;
- complete DateRangePicker evidence exists at least for a selected range;
- horizontal and vertical Resizable examples plus a stacked mobile fallback are present;
- current `package.json` contains no Vitest;
- current `bun.lock` workspace devDependencies contain no Vitest;
- home route remains unchanged and `/ui` remains production guarded.

### Remaining verified blockers
1. **Prompt/task leakage returned again.** The C5A Slider `Port Range` label in `src/routes/__dev/ui.tsx` contains copied user/supervisor instruction text (`Do not make any visual modifications... you ruined the Port Range slider again.`). Restore exactly `Port Range` and search the runtime source for any copied instruction text before acceptance.
2. **DatePicker still contains `any`.** `DatePickerProps.calendarProps` declares `locale?: any`, and rendering uses `calendarProps as any`. Remove both. Use truthful single-mode DayPicker props without allowing Core-owned mode/selected/onSelect to be overridden.
3. **DateRangePicker still contains `any`.** Same `locale?: any` and `calendarProps as any` problem. Use truthful range-mode DayPicker props. No `any` in the C5B picker boundary.
4. **Picker locale typing is still unsafe.** Do not force-cast DayPicker locale through `unknown as Locale`. Provide a truthful shared locale/display-format contract that works for both DayPicker and date-fns without `any`/double casting.
5. **Calendar gallery uses ISO-string Date constructors (`new Date("2026-08-12")`, etc.).** These parse as UTC timestamps and can shift the displayed calendar day by timezone. For date-only evidence, construct local calendar dates without ISO timestamp parsing (e.g. `new Date(2026, 7, 12)`) or another explicit date-only-safe approach. Do not introduce UTC serialization.
6. **Resizable wrapper is still not actually v4-aligned.** `src/components/core/layout/Resizable.tsx` still styles `data-[panel-group-direction=...]`, a removed v3 contract. Official v4 renamed `direction` to `orientation`; Group owns layout, and Separator emits WAI-ARIA separator semantics. Remove the stale selectors.
7. **Resizable compatibility alias is implemented as the primary API.** `ResizablePanelGroup` adds `direction?:` and maps it to `orientation`, while also manually adding flex/flex-col. The canonical public API should be v4 `orientation`. A temporary deprecated `direction` alias is acceptable only if it does not conflict with `orientation`, does not drive stale CSS/layout, and is clearly secondary/deprecated.
8. **Resizable visual orientation styling is still stale.** Separator/visual line/grip all depend on `data-panel-group-direction`. Style from the actual v4 separator `aria-orientation` (or another current v4-emitted state), not the old attribute.
9. **Resizable gallery still demonstrates legacy usage.** It uses `direction="horizontal"` / `direction="vertical"` instead of canonical `orientation`.
10. **Resizable gallery still uses numeric v4 sizes as though they were percentages.** `defaultSize={25}`, `minSize={20}`, etc. are pixels in v4. Use explicit percentages like `"25%"`, `"20%"`, `"75%"`.
11. **DateRangePicker gallery evidence is still incomplete.** Add a compact FormField error/description range example and demonstrate a disabled-date matcher; do not create a workflow.
12. **Pagination gallery evidence is still incomplete.** A disabled Next state is still missing. Keep the existing standard/asChild/mobile evidence and add one compact disabled-Next state.
13. **Package range drift remains.** `react-resizable-panels` changed from accepted `^4.6.5` to exact `4.6.5`. C5B was not authorized to change package ranges. Restore the accepted package/lock declaration unless a documented build blocker requires otherwise.
14. **Provenance overstates the current Resizable implementation.** It says legacy direction mapping and responsive flex-col layout are incorporated. After correction, document canonical v4 orientation/Group/Panel/Separator behavior and any deprecated alias truthfully.

### Review classification
C5B is close but not accepted. The next pass must be narrow: remove prompt leakage, eliminate all picker `any`/unsafe locale casts, make gallery dates truly date-only-safe, complete the missing DateRange/Pagination evidence, restore package range, and make Resizable genuinely v4-first. Then stop for supervisor review.

## Current architecture facts
- TanStack Start v1 + Vite 8.2 + React 19.2.
- Bun 1.3.3 is the canonical package manager.
- Tailwind 4.2.1.
- shadcn source setup: `new-york`; do not rerun init.
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
Execute the supervisor-provided final C5B hygiene/type/v4 correction only. Re-review before acceptance. Do not begin another C5 slice.