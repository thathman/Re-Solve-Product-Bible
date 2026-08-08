# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C4 ACCEPTED/FROZEN — FOUND-001C5A CONDITIONAL (FINAL ADVANCED INPUT CLEANUP REQUIRED)**

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

C4 non-blocking known limitation:
- `Item` no longer contains `as any`, but its public forwarded ref remains div-biased when `asChild` renders another semantic element. Runtime/semantic behavior is accepted; do not reopen it during C5A.

## FOUND-001C5A — Advanced Input Primitives I
**STATUS: CONDITIONAL — FINAL NARROW CLEANUP REQUIRED BEFORE C5B**

### Current implementation on app `main`
Reviewed application state through commit `9666f780aecbe8f598bd6a13785c799dd66a0283`.

Present through Core:
- Command / CommandDialog using `cmdk`;
- searchable single-select Combobox composed from Core Popover + Core Command;
- NativeSelect / option / optgroup using native HTML `select`;
- InputOTP family using pre-existing `input-otp`;
- Slider using pre-existing `@radix-ui/react-slider`;
- all public APIs export through `src/components/core/index.ts`;
- no new package dependency was added;
- `/ui` remains production guarded;
- home route remains the accepted temporary placeholder.

### Verified FIX improvements
- `ring-rs-focus` was removed from Command/NativeSelect/InputOTP/Slider in favor of the accepted focus-variable contract;
- CommandInput now has a default accessible name and Command selected/disabled states use Re:Solve semantics;
- Combobox now supports controlled/uncontrolled state via `value`/`defaultValue`/`onValueChange`;
- Combobox integrates FormField ID, required, disabled, invalid and described-by state;
- Combobox clear action is now a real Core IconButton outside the trigger Button;
- NativeSelect now inherits required/disabled/invalid/described-by state and uses canonical disabled/focus styling;
- InputOTP now inherits required/disabled/invalid/described-by state, marks visual slots/separator presentational and uses reduced-motion-safe fake-caret behavior;
- gallery OTP verification example now demonstrates `autocomplete="one-time-code"`, numeric input mode and numeric pattern;
- Slider now uses canonical action/subtle track semantics, 24px thumbs, FormField description/error linkage on thumbs and required `thumbLabels` typing;
- gallery Slider examples include distinct range labels and a named disabled slider;
- `input-otp` provenance now points to `https://github.com/guilhermerodz/input-otp` with MIT/version 1.4.2;
- supplied dark/light desktop and narrow/mobile gallery screenshots are visually coherent; Advanced Inputs I fits without page-level horizontal overflow, OTP remains usable on narrow layout, and Slider/NativeSelect/Combobox density is consistent with the existing Core direction.

### Remaining verified C5A blockers
1. **Slider reintroduces ordinary client-side `process.env`.** `src/components/core/inputs/Slider.tsx` uses `process.env['NODE_ENV'] === "development"` for the thumb-label warning. Foundation env boundaries already rejected ordinary universal/client `process.env`. Replace with `import.meta.env.DEV`.
2. **CommandDialog does not yet guarantee accessible Dialog naming.** It composes Core Dialog but renders `DialogContent` without a canonical DialogTitle/Description contract. Add a screen-reader title (default such as `Command palette`) and optional description/customization, or remove CommandDialog if that contract is not supported. Do not ship a public Dialog wrapper that depends on consumers accidentally supplying a title inside Command children.
3. **CommandDialog overrides the accepted raised overlay surface with `bg-rs-surface-primary`.** Preserve the frozen Core Dialog raised/elevation contract; remove that override or use `rs-surface-raised` intentionally.
4. **Combobox selection semantics conflict with the new explicit clear action.** `handleSelect` currently clears the value when the user selects the already-selected option (`newValue === value ? "" : newValue`) even when `clearable` is false. Selecting an option should select it; clearing should happen through the explicit clear control when `clearable` is enabled.
5. **Clearable Combobox is not actually demonstrated.** The gallery marks the disabled, empty Combobox as `clearable`, so no clear button can appear. Add one selected, enabled `clearable` example (prefer `defaultValue`) so the real focusable clear action is reviewable. Keep the standard standalone example nameable and functional.
6. **Slider disabled visual semantics should use Radix disabled state rather than `disabled:` pseudo-classes on Thumb.** Radix Slider Thumb is not a native disabled form element. Normalize thumb/root styling with the Radix `data-disabled` state so the locked slider is visibly and semantically distinct. Current screenshot shows the locked slider but its thumb/range treatment remains close to active state.
7. **Slider label-count warning should use the final dev-safe environment contract.** While changing to `import.meta.env.DEV`, warn on a meaningful mismatch between thumb count and `thumbLabels` count; keep the runtime fallback so an accidental mismatch cannot produce an unnamed thumb.
8. **No C5B work yet.** Calendar/date/range/pagination/resizable remain blocked until this cleanup is reviewed.

### Review classification
C5A is close. Preserve the current architecture and visual direction. Execute one final narrow cleanup covering only CommandDialog accessibility/surface, Combobox select-vs-clear behavior/evidence, Slider dev-env/disabled-state hardening, then re-review. If clean, freeze C5A and proceed to C5B.

## Security-memory visibility
- Supervisor searched both the app repository and Product Bible for `security-memory` / Lovable memory source and found no source-controlled artifact.
- The user reports `@security-memory` was updated in Lovable project memory, but that memory is not currently inspectable through GitHub.
- Do not claim it has been audited or changed by the supervisor until its text is surfaced in chat or source control.

## Current architecture facts
- TanStack Start v1 + Vite 8.2 + React 19.2.
- Bun 1.3.3 only package manager.
- Tailwind 4.2.1.
- shadcn source setup: `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- Drawer: Vaul 1.1.2.
- Toast: Sonner 2.0.7.
- Command: cmdk 1.1.1.
- OTP: input-otp 1.4.2.
- Slider: @radix-ui/react-slider 1.3.6.
- Icons: Lucide 0.575.0.
- Typography: Inter Variable + JetBrains Mono Variable via Fontsource 5.3.0.
- Query/server state: TanStack Query.
- Forms/validation available: React Hook Form + Zod.
- Chart foundation: Recharts.
- testing/PWA/auth/domain implementation: not yet configured/built.

## UI source direction
- Re:Solve Core is the public UI boundary.
- Current React shadcn patterns are preferred where compatible.
- shadcn-vue remains visual/composition reference only; never runtime Vue code.
- Keep current Radix base; no wholesale Base UI or React Aria migration.
- Untitled UI and Tremor remain selective source/reference systems.

## Planned later work
- C5B: Calendar, Date Picker/Date Range, Pagination, Resizable and other bounded scheduling/navigation primitives.
- Questionnaire/review remains a higher-order composition above FormField/FieldGroup, not a second forms framework.
- QR remains a later utility/presentation pattern; security-sensitive QR encodes signed/short-lived references only.
- Conversation/Àríyá, auth, dashboard, shell, PWA, CI and testing remain later FOUND-001 work.

## Next action
Execute supervisor-provided final `FOUND-001C5A` cleanup only. Re-review afterward. Do not begin C5B.