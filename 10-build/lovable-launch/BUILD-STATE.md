# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E1 CLIENT PORTAL SHELL CONDITIONAL / FINAL MICRO-FIX NEXT**

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
**CONDITIONAL — FINAL MICRO-CLOSURE REQUIRED**

Verified-good E1 architecture:
- `/` now renders the Client Portal Home surface; the old Lovable blank placeholder and `data-lovable-blank-page-placeholder` are removed;
- `PortalShell`, `PortalTopBar`, `PortalNavigation`, `PortalPageHeader`, and shell-local `portal-nav.ts` live under `src/components/shell/portal/`;
- Portal is independently composed and does not import Admin shell components;
- desktop Portal navigation uses frozen horizontal NavigationMenu with Home active and Properties/Projects/Support/Billing shown as genuinely noninteractive future destinations;
- mobile Portal navigation uses a purpose-built Core Sheet with vertical navigation rather than desktop Sidebar collapse;
- Portal TopBar contains brand, Search placeholder, Notifications placeholder with deterministic count `2`, Àríyá placeholder and deterministic client account/avatar evidence;
- Home is a quiet `PortalPageHeader` + `StatePanel` validation surface with no fake business data;
- root route explicitly defers authentication/authorization to FOUND-001F;
- requested E1-FIX corrections are verified on `main`: Notifications trigger semantics now land on the actual Core button, Badge is pointer-safe, account and brand use frozen focus variables, Portal Navigation imports through `@/components/core`, Portal TopBar consumes Core `toast`, Sign out uses canonical destructive/status tokens, and Portal shell/topbar horizontal gutters use canonical responsive gutter tokens;
- no package dependency or security override drift was introduced;
- `src/start.ts` still explicitly preserves TanStack `createCsrfMiddleware` for server functions.

Remaining E1 blockers:
1. `PortalTopBar.tsx` Search trigger still references `bg-rs-surface-secondary`, but no canonical `rs-surface-secondary` token exists. Use an accepted surface token such as `bg-rs-surface-primary` or `bg-rs-surface-subtle`, preserving current restrained visual intent.
2. `PortalShell.tsx` contains the instruction-like source comment `Do not pretend the portal is secured yet.` Keep the concise engineering fact `Authentication/authorization is intentionally deferred to FOUND-001F.` but remove the supervisor-style imperative line to satisfy prompt/source hygiene.

Non-blocking hygiene: `PortalNavigation.tsx` still imports React without using it. It may be removed during this final shell-local micro-fix.

Preserve all accepted E1 behavior while fixing only these remaining details.

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
- `/` is now the Client Portal Home surface; `/admin` remains the frozen staff/admin application shell.

## UI/product direction
- Re:Solve Core is the public UI boundary.
- Admin navigation stays simple and shallow, closer to Perfex/Brevo than Odoo/Twenty.
- Client Portal is calmer and less dense than Admin while remaining clearly Re:Solve.
- Àríyá is Re:Solve's built-in AI surface; Chatwoot keeps Captain separately.
- shadcn-vue is visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.
- No timesheets, HR, or client service-consumption concepts.

## Next action
Run one final FOUND-001E1-FIX2 micro-pass to replace the non-existent `rs-surface-secondary` Search surface token, remove the instruction-like PortalShell comment, and optionally remove the unused React import in PortalNavigation. Preserve all accepted Portal shell behavior, Admin/Core frozen boundaries, package/security state and explicit CSRF middleware. If clean, freeze E1 and proceed to E2 route-aware Portal navigation/shell composition.