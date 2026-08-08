# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5A ACCEPTED/FROZEN — SECURITY-MEM-001 ACCEPTED/CANONICAL — FOUND-001C5B READY**

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

Accepted inventory:
- Command / CommandDialog
- Combobox
- NativeSelect / NativeSelectOption / NativeSelectOptGroup
- InputOTP / InputOTPGroup / InputOTPSlot / InputOTPSeparator
- Slider

Accepted contracts:
- Command uses pre-existing `cmdk` 1.1.1, canonical selected/disabled semantics and a programmatically named CommandInput;
- CommandDialog composes frozen Core Dialog, guarantees an accessible title, supports optional description and preserves raised Dialog surface/elevation;
- Combobox composes Core Popover + Core Command, supports controlled/uncontrolled value state, inherits FormField ID/required/disabled/invalid/described-by state, and uses a separate Core IconButton for explicit clearing;
- selecting an already-selected Combobox option does not implicitly clear it;
- NativeSelect remains a real native select with FormField semantics and 16px narrow/mobile typography;
- InputOTP uses pre-existing `input-otp` 1.4.2, inherits FormField semantics, keeps visual slots/separator presentational, supports one-time-code/numeric examples without globally forbidding alphanumeric use, and uses reduced-motion-safe caret behavior;
- Slider uses pre-existing `@radix-ui/react-slider` 1.3.6, requires thumb labels at the Core API, links FormField description/error to thumbs, uses 24px actual thumb targets, distinct range-thumb names, action-primary selected range, subtle inactive track and Radix disabled-state styling;
- Slider diagnostics use `import.meta.env.DEV`, not client-side `process.env`;
- all C5A APIs export through Core;
- no new dependency was added;
- `input-otp` provenance points to `https://github.com/guilhermerodz/input-otp` (MIT);
- `/ui` production guard remains secured;
- home route and package state remain unchanged.

Visual review:
- user-supplied dark desktop, light desktop and narrow/mobile Component Gallery captures passed visual review;
- Advanced Inputs I remains restrained/coherent and narrow layout shows no page-level horizontal overflow.

## SECURITY-MEM-001 — Lovable Security Memory
**ACCEPTED / CANONICAL**

The user replaced Lovable `@security-memory` with the supervisor-approved rules and read the result back in chat. No secret material was detected.

Canonical security-memory principles now include:
- never trust client-editable profile/user metadata as the sole authorization authority;
- model authorization in server-controlled principals/memberships/roles/permissions/grants;
- every table exposed through the Supabase Data API requires intentional RLS plus least-privilege database grants;
- keep tables server-only/unexposed where direct Data API access is unnecessary;
- Supabase secret/service-role credentials are server-only and must never enter browser bundles, `VITE_*`, browser storage, URLs, logs or telemetry;
- PostgreSQL functions default to `SECURITY INVOKER`; narrowly justified `SECURITY DEFINER` functions require controlled/empty `search_path`, fully qualified objects and restricted EXECUTE privileges;
- private/tenant/account/sensitive data must enforce authn/authz at the server function or server route boundary; UI/route guards are UX, not authorization;
- TanStack `createServerFn` is for typed same-origin app RPC; server routes are for external/cross-origin/protocol HTTP surfaces;
- untrusted server input requires runtime validation;
- preserve `createCsrfMiddleware` in `src/start.ts` for server functions;
- do not treat an auth middleware/helper as canonical until it actually exists and is reviewed;
- Vault secrets must not enter browser storage, URLs, ordinary logs, analytics/error telemetry, search, notification bodies or non-Vault persistence;
- security-sensitive QR flows encode only signed/scoped/short-lived references, never raw secrets;
- Action Registry enforcement begins once that registry exists; before then consequential mutations still require server-side authz, validation, confirmation where appropriate, idempotency/retry consideration and audit-event design;
- schema/RLS/grants/functions/triggers/security configuration must be reproducible through version-controlled migrations/configuration;
- logs/errors follow data minimization and redact secret material.

Supervisor verification against current official guidance:
- Supabase requires RLS on exposed-schema tables and recommends least-privilege grants;
- secret/service-role keys bypass RLS and are server-only;
- Supabase recommends `SECURITY INVOKER` by default and controlled `search_path`/restricted execution for `SECURITY DEFINER` functions;
- TanStack Start documents server functions as same-origin app RPC, server routes for outside callers, endpoint-level auth for private data and explicit `createCsrfMiddleware` when `src/start.ts` exists.

Do not implement database/auth systems merely because these memory rules are now canonical; they constrain later slices when those systems are actually built.

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
- Calendar/date foundation already installed: `react-day-picker` 9.14.0 + `date-fns` 4.1.0.
- Resizable foundation already installed: `react-resizable-panels` 4.6.5.
- Icons: Lucide 0.575.0.
- Typography: Inter Variable + JetBrains Mono Variable via Fontsource 5.3.0.
- Query/server state: TanStack Query.
- Forms/validation available: React Hook Form + Zod.
- Chart foundation: Recharts.
- testing/PWA/auth/domain implementation: not yet configured/built.

## UI source direction
- Re:Solve Core is the public UI boundary.
- Current React shadcn Radix-compatible patterns are preferred where compatible with the existing project.
- Current shadcn may default new projects to Base UI, but existing Re:Solve remains on its established Radix foundation; do not migrate wholesale.
- shadcn-vue remains visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.

## Planned later work
- C5B: Calendar, DatePicker, DateRangePicker, Pagination and Resizable.
- Later advanced input/composition slices may address Number Field, Tags Input, Stepper and Questionnaire where justified.
- Questionnaire/review remains a higher-order composition above FormField/FieldGroup, not a second forms framework.
- QR remains a later utility/presentation pattern; security-sensitive QR encodes signed/short-lived references only.
- Conversation/Àríyá, auth, dashboard, shell, PWA, CI and testing remain later FOUND-001 work.

## Next action
Begin bounded `FOUND-001C5B — Calendar, Date Selection, Pagination & Resizable`. Preserve frozen C1-C5A APIs and canonical security memory. Expand the Component Gallery, verify date-only/timezone semantics, accessibility, responsiveness and provenance, then STOP for supervisor review.