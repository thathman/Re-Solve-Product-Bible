# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5A ACCEPTED/FROZEN — SECURITY-MEM-001 ACCEPTED/CANONICAL — FOUND-001C5B CONDITIONAL (FINAL CLOSURE CORRECTION REQUIRED)**

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

The user replaced Lovable `@security-memory` with the supervisor-approved 13-rule security memory and read the result back in chat. No secret material was detected. It remains canonical unless a later surfaced text differs.

Canonical principles include server-controlled authorization, intentional RLS on Data-API-exposed tables, least-privilege grants, server-only service-role credentials, SECURITY INVOKER by default, narrowly constrained SECURITY DEFINER, server-boundary authn/authz, createServerFn for same-origin typed RPC, server routes for external/protocol HTTP surfaces, runtime validation of untrusted server input, preserved TanStack Start CSRF middleware, Vault secret minimization, signed/scoped/short-lived security-sensitive QR references, migration-controlled security configuration and log/error redaction.

Do not implement auth/database systems merely because the memory is canonical; the rules constrain later slices.

## FOUND-001C5B — Calendar, Date Selection, Pagination & Resizable
**STATUS: CONDITIONAL — FINAL CLOSURE CORRECTION REQUIRED**

### Current implementation present on app `main`
- `Calendar` using pre-existing react-day-picker 9.14.0;
- `DatePicker` and `DateRangePicker` composed from Core Button + Core Popover + Core Calendar;
- `Pagination` family with Slot/asChild capability;
- `ResizablePanelGroup`, `ResizablePanel`, `ResizableHandle` wrapping react-resizable-panels 4.6.5;
- explicit C5B exports added to the restored Core public boundary;
- `Advanced Inputs II` gallery section now exists;
- C5B provenance entries for react-day-picker/date-fns/react-resizable-panels are present.

### Verified FIX improvements
- leaked prompt/task text has been removed from current app source and C5A `Port Range` label is clean;
- `src/lib/formatters/index.ts` is restored exactly to its accepted pre-C5B behavior;
- unauthorized formatter test was removed;
- `package.json` no longer contains Vitest and is back to the accepted dependency set;
- broad C5B `export *` rewrite was undone and explicit C5B public exports were added;
- DatePicker/DateRangePicker now use nullish FormField merging and danger-foreground invalid borders;
- DateRangePicker no longer contains `as any` and starts with one month before matchMedia enhancement;
- PaginationLink now has Slot/asChild composition;
- disabled Pagination Previous/Next render non-anchor spans;
- Advanced Inputs II imports C5B families through `@/components/core`;
- C5B date source contains no `toISOString`, `toUTCString`, `Date.UTC` or UTC serialization logic;
- home route remains unchanged and `/ui` remains production guarded.

### Remaining verified blockers
1. **bun.lock is still stale.** `package.json` has no Vitest, but current `bun.lock` still lists `vitest ^4.1.10` as a workspace devDependency and retains its added lock entries. Restore `bun.lock` to the accepted C5A baseline (commit `9666f780aecbe8f598bd6a13785c799dd66a0283` is package-identical) or regenerate/prune deterministically with Bun so Vitest is absent.
2. **Frozen C1 Metrics gallery is still regressed.** Current Metrics section contains `Total Expenses` twice and altered delta semantics. Restore exactly the accepted five examples: MRR; Active Properties; Incident Count; Total Expenses (down/positive 8.4%); System Availability.
3. **DatePicker controlled/uncontrolled detection is logically incorrect.** `value !== undefined || (onValueChange && "value" in { value })` treats any picker with `onValueChange` as controlled even when the `value` prop was omitted. Use actual prop-presence detection (e.g. `hasOwnProperty` on the original props object) or another stable controllable-state implementation.
4. **DateRangePicker repeats the same controlled-state bug.** Fix with the same canonical prop-presence strategy.
5. **Calendar prop precedence is unsafe in both pickers.** Managed Core props are supplied before `{...calendarProps}`, so `calendarProps.disabled` can override picker behavior and DateRange `calendarProps.numberOfMonths` can defeat the mobile one-month contract. Separate control-disabled from date-disabled rules and ensure Core-managed `mode`, `selected`, `onSelect`, responsive month count and required behavior cannot be overwritten by spread order.
6. **Picker calendarProps typing should be mode-specific.** Prefer React DayPicker single/range prop types so supported disabled-date/locale/timeZone/navigation props remain available without allowing consumers to override Core-managed selection/mode state.
7. **DatePicker/DateRange display locale casts are weak.** DayPicker exposes a partial locale type while date-fns formatting expects a full locale. Keep locale-aware formatting but avoid unsafe assumptions; use a truthful formatter/helper contract. Do not add timezone serialization or another package.
8. **Pagination disabled mobile controls lack guaranteed accessible names.** Disabled Previous/Next spans hide visible labels below `sm` but do not carry the enabled controls' aria-label. Add `aria-label` to the disabled noninteractive states.
9. **Resizable is still using removed v3 selectors.** `Resizable.tsx` still contains `data-[panel-group-direction=...]`. react-resizable-panels v4 Group owns layout via `orientation`; Separator exposes WAI-ARIA separator semantics. Remove all stale direction selectors and style using the actual v4 contract (e.g. wrapper-owned orientation data and/or Separator `aria-orientation`).
10. **Resizable gallery still uses old v3 prop and wrong v4 size units.** It renders `<ResizablePanelGroup direction="horizontal">`; v4 uses `orientation="horizontal"`. Numeric `defaultSize={25}`/`minSize={20}` are pixels in v4, not percentages. Use explicit percentage strings such as `"25%"`, `"20%"`, `"75%"` for this example.
11. **Resizable gallery lacks the required vertical example.** Add one compact vertical group and keep the existing stacked mobile fallback.
12. **C5B Calendar gallery evidence is incomplete.** Single and range calendars exist, but there is no disabled/unavailable-date example; selected date currently equals today, so today-vs-selected distinction is not clearly demonstrated. Use deterministic sample dates and show unavailable dates separately.
13. **DatePicker gallery evidence is incomplete.** There is no standalone named/default-selected DatePicker and no required/error DatePicker example; current examples are only ordinary FormField, required DateRangePicker and disabled DatePicker.
14. **DateRangePicker gallery evidence is incomplete.** Add a selected complete range plus a description/error example and disabled-date rule. Preserve narrow one-month behavior.
15. **Pagination gallery evidence is incomplete.** Add a truly disabled Next state, a bounded narrow/mobile composition, and one simple `asChild` example proving router-compatible composition without implementing routing.
16. **Provenance needs final wording after the implementation is corrected.** Explicitly document DatePicker/DateRangePicker as Re:Solve-owned Core Button + Popover + Calendar compositions and react-resizable-panels v4 orientation semantics; do not overclaim gallery evidence until final.

### Review classification
C5B remains salvageable and should be corrected in place. Do not replace React DayPicker/date-fns/react-resizable-panels. The remaining pass is closure hardening: prune the stale lockfile, restore frozen Metric evidence, fix picker controlled-state/prop precedence, finish Pagination/Resizable v4 semantics, complete the already-started Advanced Inputs II gallery, then stop for supervisor review.

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
- Testing stack remains not canonical/configured; C5B must leave Vitest absent from both package.json and bun.lock.
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
Execute the supervisor-provided final `FOUND-001C5B` closure correction only. Re-review before acceptance. Do not begin another C5 slice.