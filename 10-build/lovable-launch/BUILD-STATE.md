# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E1 CLIENT PORTAL SHELL ACCEPTED/FROZEN — FOUND-001E2 NEXT**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — specification/planning source.
- Current app: `thathman/re-solve-c560d62c` — canonical Lovable development app on `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Security memory
**ACCEPTED / CANONICAL**
- Roles, permissions and capability decisions are server-controlled; browser/client metadata is never authoritative for authorization.
- Authentication and authorization must be enforced at server-function / server-route boundaries, not only in UI or client navigation.
- Do not invent helper names or security middleware that do not exist (for example, never assume `requireSupabaseAuth` exists); inspect and extend real server boundaries deliberately.
- RLS and least privilege are mandatory when persistence is introduced. Database grants/policies/security configuration must be version-controlled and reviewable.
- Service-role credentials and other privileged backend secrets are server-only and must never ship in client bundles.
- `SECURITY INVOKER` is the default for database functions/views; `SECURITY DEFINER` must remain narrow, justified, least-privileged and explicitly reviewed.
- Runtime input validation is required at consequential server boundaries.
- Preserve `createCsrfMiddleware` in `src/start.ts`; defining `src/start.ts` opts out of TanStack Start's implicit CSRF setup, so this explicit middleware is a security contract.
- Vault secrets must never appear in browser storage, logs, search results, notifications, analytics, non-Vault surfaces or ordinary client caches.
- QR codes may expose only signed, scoped, short-lived references/tokens; never encode raw secrets or durable privileged credentials.
- Consequential mutations should eventually route through an Action Registry / equivalent audited mutation boundary as the product domain is implemented; do not scatter privileged mutations across ad-hoc client-triggered handlers.
- Sensitive values, auth tokens, secret payloads and privileged identifiers must not be written to application logs or error telemetry.
- No security vulnerability exceptions are accepted.

## SECURITY-GATE-001 — Dependency remediation
**ACCEPTED / CLOSED**
Canonical package state:
- `@tanstack/react-router`: `^1.170.18`
- `@tanstack/react-start`: `^1.168.32`
- `@tanstack/router-plugin`: `^1.168.23`
- `@tanstack/react-table`: `8.20.5`
- no direct `@tanstack/router-core`
- no direct `js-yaml`
- top-level Bun override: `"js-yaml": "4.3.1"`
- no accepted High/Critical security finding.

## Currency display convention
**CANONICAL**
- Currency identity remains explicit via ISO codes in data/API contracts.
- Normal user-facing UI uses locale-appropriate symbols where unambiguous.
- There is no universal default currency.

## FOUND-001A/B — Foundation and design system
**ACCEPTED / CLOSED**
Canonical foundation includes TanStack Start + React 19, Bun, Tailwind v4, semantic OKLCH tokens, light/dark/system themes, Inter + JetBrains Mono, responsive spacing/shell reservations, frozen focus variables, environment/server-only boundaries, UI provenance, `/ui` development gallery with production redirect, and self-hostability/no required Lovable runtime dependency.

## FOUND-001C — Core UI Framework
**ACCEPTED / CANONICAL / FROZEN / CLOSED**
Canonical Core includes actions, forms, overlays/disclosure, feedback/composition, advanced inputs/date, display/layout, generic TanStack DataTable, Sidebar family, and NavigationMenu family.

Frozen DataTable includes sorting, pagination, global/text/select filtering, visibility, opt-in current-page selection, truthful loading/error/source-empty/filtered-empty states, responsive containment, and stable-row-ID boundary. Server/manual modes, URL state, saved views, pinning, bulk actions and exports remain deferred until concrete product requirements.

Frozen navigation includes responsive SidebarProvider/useSidebar and full Sidebar primitive family, mobile Sheet composition, no Core persistence/global shortcut policy, semantic list/asChild composition, deterministic skeletons, and Radix NavigationMenu with canonical focus/tokens and viewport-safe behavior.

Do not reopen Core absent a concrete regression or later shell/domain requirement proving a genuinely missing contract.

## FOUND-001D — Admin Shell
**ACCEPTED / CANONICAL / FROZEN / CLOSED**
Canonical Admin shell at `/admin` includes:
- shell-owned Sidebar/TopBar/PageHeader/Breadcrumbs/Command/Àríyá compositions;
- nine Admin root routes under one TanStack layout;
- route-aware navigation/current semantics and mobile-close behavior;
- shell-owned Cmd/Ctrl+K Command/Search;
- anchored Notifications placeholder;
- shared right-side Àríyá Sheet placeholder;
- deterministic account/avatar placeholder actions;
- one main landmark, responsive desktop/tablet/mobile behavior, light/dark semantic tokens;
- no auth, permissions, database, domain data, real notifications or AI backend;
- no Core/package/security drift.

FOUND-001D passed its final no-feature closure review with no blockers and no modifications. Do not reopen it without a concrete regression or later requirement exposing a missing shell contract.

## FOUND-001E1 — Client Portal Shell Chrome & Visual Foundation
**ACCEPTED / CANONICAL / FROZEN**
Canonical E1 includes:
- `/` is now the Client Portal Home surface; the old Lovable blank placeholder and placeholder SVG/marker are removed;
- shell-owned `PortalShell`, `PortalTopBar`, `PortalNavigation`, `PortalPageHeader`, and `portal-nav.ts` under `src/components/shell/portal/` with no Admin-shell imports;
- desktop Portal navigation uses frozen horizontal Core NavigationMenu with Home as the only implemented route in E1;
- Properties, Projects, Support and Billing are shown in E1 as genuinely noninteractive `aria-disabled` future destinations with no fake href/click/tabIndex behavior;
- mobile Portal navigation uses a purpose-built Core Sheet with semantic title/description and vertical navigation rather than Admin Sidebar collapse;
- Portal TopBar contains Re:Solve brand, Search placeholder, Notifications placeholder with deterministic unread count `2`, responsive Àríyá placeholder, and deterministic fictional client identity `Chinedu Okeke / Acme Properties Ltd.` using local avatar fallback;
- root Home is a quiet `PortalPageHeader` + `StatePanel` validation surface with no fake domain data;
- `PortalShell` keeps exactly one primary `main` landmark and explicitly notes that authentication/authorization is deferred to FOUND-001F;
- Notifications Radix trigger semantics land on the actual Core button and the unread Badge is pointer-safe;
- account and brand links use the frozen focus-variable contract;
- Portal Navigation and toast consumption use the public `@/components/core` boundary;
- Sign out uses canonical destructive/status tokens rather than invented danger tokens;
- Portal shell and TopBar use canonical responsive gutter tokens;
- Search uses canonical `bg-rs-surface-primary`; the invalid `rs-surface-secondary` usage is removed;
- instruction-like security/source commentary was removed while retaining the factual FOUND-001F auth-deferral note;
- no auth, database, RLS implementation, domain models/data, real Search, real Notifications or real Àríyá backend was added;
- no Core/Admin/package/security drift was introduced; reported frozen install/build/lint/TypeScript checks pass.

Do not reopen E1 unless a concrete Portal-shell regression appears.

## FOUND-001C5E audit deferrals
Build in shell/domain only when justified:
- DescriptionList / key-value detail composition.

Defer to first real domain requirement:
- NumberField / Currency / Percent editing
- Timeline / activity
- FileUpload
- RichTextEditor
- Charts
- Kanban
- TreeSelect

Unnecessary as dedicated Core families unless a later requirement proves otherwise:
- SearchField
- Menubar
- SectionHeader
- generic Toolbar
- Carousel

## Current architecture facts
- TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3.
- Tailwind 4.2.1 declaration baseline.
- shadcn source setup `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- TanStack React Table `8.20.5` is the canonical DataTable engine.
- Auth, database/RLS, PWA and domain implementation remain later work.
- `/ui` is development/Lovable gallery and redirects to `/` in production.
- `/` is the Client Portal Home surface; `/admin` remains the frozen staff/admin application shell.

## UI/product direction
- Re:Solve Core is the public UI boundary.
- Admin navigation stays simple and shallow, closer to Perfex/Brevo than Odoo/Twenty.
- Client Portal is calmer and less dense than Admin while remaining clearly Re:Solve.
- Àríyá is Re:Solve's built-in AI surface; Chatwoot keeps Captain separately.
- shadcn-vue is visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.
- No timesheets, HR, or client service-consumption concepts.

## Next action
Begin FOUND-001E2 as a small Client Portal shell slice: convert Properties, Projects, Support and Billing into real placeholder route skeletons, make Portal navigation route-aware across desktop/mobile, add a shell-owned Portal Command/Search surface over frozen Core Command, and establish route-aware page-header/breadcrumb context without implementing business-domain data, auth, database, real Notifications or real Àríyá functionality.