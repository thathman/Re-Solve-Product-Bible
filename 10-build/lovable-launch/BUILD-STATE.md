# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C4 ACCEPTED/FROZEN — FOUND-001C5A CONDITIONAL (ADVANCED INPUT CONTRACT FIX REQUIRED)**

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
- `Item` no longer contains `as any`, but the public forwarded ref remains div-biased when `asChild` renders another semantic element. Runtime/semantic behavior is accepted; do not reopen it during C5A.

## FOUND-001C5A — Advanced Input Primitives I
**STATUS: CONDITIONAL — ONE BOUNDED CONTRACT CORRECTION REQUIRED BEFORE C5B**

### Current implementation present on app `main`
- Command / CommandDialog family using `cmdk`;
- searchable single-select Combobox composed from Core Popover + Core Command;
- NativeSelect / option / optgroup using a real HTML `select`;
- InputOTP family using pre-existing `input-otp`;
- Slider using pre-existing `@radix-ui/react-slider`;
- all five families export through `src/components/core/index.ts`;
- gallery contains an `Advanced Inputs I` section;
- `package.json` shows no new dependency: cmdk 1.1.1, input-otp 1.4.2 and Radix Slider 1.3.6 were already present;
- `/ui` production guard remains secured;
- home route remains the accepted temporary placeholder.

### Verified blockers / corrections required
1. **Non-canonical focus token reintroduced.** NativeSelect, InputOTP slots and Slider use `ring-rs-focus`, which is not part of accepted token authority. Replace with the frozen explicit `--rs-focus-ring-*` / offset-variable contract. Do not create a new `rs-focus` alias.
2. **Command normalization incomplete.** CommandDialog adds stock `shadow-lg` instead of canonical overlay elevation. Command selected state should use the accepted selected surface. CommandInput needs an explicit accessible-name contract rather than relying on placeholder text.
3. **Combobox FormField contract incomplete.** It propagates ID, disabled, invalid and described-by but omits FormField required semantics. Standalone Combobox has no accessible-name prop/contract. Use nullish state merging rather than `||` where explicit overrides are supported.
4. **Combobox gallery is functionally inert.** Current Combobox is controlled-only (`value` + `onValueChange`) but the standard gallery example supplies neither, so selecting an option does not update the visible selected value. Add a coherent controlled/uncontrolled contract (`defaultValue` is acceptable) or make gallery state explicit.
5. **Combobox clear action is inaccessible.** `clearable` renders a clickable `X` SVG inside the trigger Button. It is mouse-only and creates a second pseudo-action inside a button. Replace with a real separately focusable Core action outside the trigger, or another accessible non-nested clear contract.
6. **NativeSelect FormField contract incomplete.** Required state is not inherited. Disabled/required/id/described-by/invalid values should be intentionally resolved without later prop spreading silently undoing context. Use canonical disabled surface/text/border and focus-variable treatment.
7. **InputOTP FormField contract incomplete.** Required state is not inherited and disabled merging uses `||`. Active slot focus uses non-canonical `rs-focus`. OTP visual slots/separator should remain presentational so the underlying coherent input is not duplicated to assistive tech. Verification-code gallery should explicitly demonstrate `autocomplete="one-time-code"` and numeric input semantics. Fake-caret motion must remain reduced-motion safe.
8. **Slider accessibility is not yet canonical.** `aria-describedby`/FormField ID are placed on the Radix Root rather than the actual slider Thumb controls. Accessible thumb names are optional although the slice required naming. The disabled gallery slider is unnamed. Range thumbs must have distinct names. Move relevant ARIA/ID/error linkage to thumbs and make naming mandatory or otherwise guaranteed.
9. **Slider visual/touch contract mismatch.** Code uses 20×20 thumbs despite the completion report claiming 24×24. Use at least the accepted 24×24 actual target, canonical focus variables, `rs-action-primary` for selected range and a subtle inactive track. Active scaling must be motion-safe. Use programmatic disabled semantics/styling from Radix state.
10. **Gallery evidence needs correction rather than expansion.** Preserve Command grouped/empty/disabled/shortcut evidence, but make Combobox actually selectable/clearable and named; prove required FormField semantics; give OTP verification semantics; give disabled Slider an accessible name/value context.
11. **Provenance has an incorrect input-otp source URL.** Correct upstream to `guilhermerodz/input-otp` (MIT). Keep package version 1.4.2 and pre-existing-dependency history. Only claim FormField/Slider accessibility normalization that actually exists after the fix.
12. **No new dependencies are required.** Do not modify package.json/bun.lock. Do not add Base UI, React Aria, Vue or another combobox/OTP/slider library.

### Review classification
C5A architecture is usable and should be corrected in place. Do not tear it down. One bounded fix should normalize focus tokens, complete FormField/accessibility contracts, make Combobox interaction real, harden OTP/Slider semantics and correct provenance. Re-review before C5B.

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
Execute supervisor-provided `FOUND-001C5A-FIX` only. Re-review afterward. Do not begin C5B.