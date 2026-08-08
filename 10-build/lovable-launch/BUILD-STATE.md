# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C4 ACCEPTED/FROZEN — FOUND-001C5A ACCEPTED/FROZEN — SECURITY-MEM-001 READY — FOUND-001C5B PENDING**

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

C4 non-blocking known limitation:
- `Item` public forwarded ref remains div-biased when `asChild` renders another semantic element. Runtime/semantic behavior is accepted; do not reopen casually.

### FOUND-001C5A — Advanced Input Primitives I
**ACCEPTED / CANONICAL / FROZEN**

Accepted inventory:
- Command / CommandDialog
- Combobox
- NativeSelect / NativeSelectOption / NativeSelectOptGroup
- InputOTP / InputOTPGroup / InputOTPSlot / InputOTPSeparator
- Slider

Accepted contracts:
- Command uses pre-existing `cmdk` 1.1.1, canonical selected/disabled semantics and a programmatically named CommandInput;
- CommandDialog composes the frozen Core Dialog, guarantees an accessible title (default `Command palette`), supports optional description and does not override the raised Dialog surface;
- Combobox composes Core Popover + Core Command, supports controlled/uncontrolled `value` / `defaultValue` / `onValueChange`, inherits FormField ID/required/disabled/invalid/described-by state, and uses a separate Core IconButton for explicit clearing;
- selecting an already-selected Combobox option does not implicitly clear it;
- NativeSelect remains a real native `select`, inherits FormField semantics and preserves 16px narrow/mobile typography;
- InputOTP uses pre-existing `input-otp` 1.4.2, inherits FormField semantics, keeps visual slots/separator presentational, supports one-time-code/numeric examples without globally forbidding alphanumeric use, and uses reduced-motion-safe caret behavior;
- Slider uses pre-existing `@radix-ui/react-slider` 1.3.6, requires thumb labels at the Core API, links FormField descriptions/errors to actual thumbs, uses 24px actual thumb targets, distinct range-thumb names, action-primary selected range, subtle inactive track and Radix disabled-state styling;
- Slider development diagnostics use `import.meta.env.DEV`, not ordinary client-side `process.env`;
- all C5A APIs export through `src/components/core/index.ts`;
- no new dependency was added;
- `input-otp` provenance points to `https://github.com/guilhermerodz/input-otp` (MIT);
- `/ui` production guard remains secured;
- home route and package state remain unchanged.

Visual review:
- user-supplied dark desktop, light desktop and narrow/mobile Component Gallery captures passed visual review;
- Advanced Inputs I remains restrained and coherent with the existing Core system;
- narrow layout shows no page-level horizontal overflow and OTP/NativeSelect/Slider remain usable.

Non-blocking C5A note:
- Slider's development warning wording may be polished later; runtime fallback still guarantees a thumb name if labels and rendered thumbs diverge.

## Security-memory review
The user surfaced the current Lovable `@security-memory` in chat. No secrets or credentials were present.

Current memory is **not canonical as written** and should be replaced before backend/auth work because several rules are over-broad or premature:
- do not force all roles/permissions into a single `user_roles` model; Re:Solve authorization must accommodate principals, memberships, roles and permissions without trusting client-editable profile metadata;
- do not mandate `SECURITY DEFINER` for every role check; default to invoker semantics and use narrowly scoped definer functions only when required;
- do not blanket-GRANT every public table to `authenticated` and `service_role`; exposed tables require RLS and least-privilege grants, while sensitive tables may be server-only/unexposed;
- `service_role` is server-only and must never reach browser code or `VITE_*` variables;
- app-internal private data operations should use authenticated/authorized server functions or server routes as appropriate, but not every piece of application logic must be a `createServerFn`;
- external/cross-origin APIs use server routes; a `/api/public/*` path does not imply anonymous access;
- the named `requireSupabaseAuth` middleware does not exist yet and must not be treated as an existing implementation;
- `src/start.ts` already explicitly installs TanStack Start CSRF middleware for server functions and should retain that protection;
- Vault secrets must not enter browser storage, URLs, logs, analytics/error telemetry, search indexes, notification bodies or other non-Vault persistence;
- Action Registry enforcement is a target architecture rule once that registry exists; until then, no consequential domain mutation should ship without explicit authz, validation, confirmation where appropriate and an audit-event design.

Next security-memory step: replace the Lovable memory with the supervisor-approved text from `SECURITY-MEM-001`; do not create database/auth implementation during that step.

## Current architecture facts
- TanStack Start v1 + Vite 8.2 + React 19.2.
- Bun 1.3.3 only package manager.
- Tailwind 4.2.1.
- shadcn source setup: `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- `src/start.ts` explicitly includes TanStack Start CSRF middleware for server functions.
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
Execute `SECURITY-MEM-001` only: replace Lovable `@security-memory` with the supervisor-approved security rules. Return the resulting memory text for confirmation, then STOP. Do not begin C5B until that memory update is reviewed.