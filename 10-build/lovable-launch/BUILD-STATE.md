# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E1 CLIENT PORTAL SHELL CONDITIONAL / NARROW FIX NEXT**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — specification/planning source.
- Current app: `thathman/re-solve-c560d62c` — canonical Lovable development app on `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Security memory
**ACCEPTED / CANONICAL**
- Authentication and authorization remain server-authoritative.
- RLS / least privilege remain required when persistence is introduced.
- Service-role credentials remain server-only.
- SECURITY INVOKER is the default; SECURITY DEFINER must remain narrow and justified.
- Runtime validation and the existing CSRF middleware boundary must be preserved.
- Vault secrets must never appear in browser storage, logs, search, notifications or non-Vault surfaces.
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
**CONDITIONAL — NARROW CLOSURE REQUIRED**

Verified-good E1 architecture:
- `/` now renders the Client Portal Home surface; the old Lovable blank placeholder and `data-lovable-blank-page-placeholder` are removed;
- `PortalShell`, `PortalTopBar`, `PortalNavigation`, `PortalPageHeader`, and shell-local `portal-nav.ts` live under `src/components/shell/portal/`;
- Portal is independently composed and does not import Admin shell components;
- desktop Portal navigation uses the frozen horizontal NavigationMenu pattern with Home active and Properties/Projects/Support/Billing shown as genuinely noninteractive future destinations;
- mobile Portal navigation uses a purpose-built Core Sheet with vertical navigation rather than desktop Sidebar collapse;
- Portal TopBar contains brand, Search placeholder, Notifications placeholder with deterministic count `2`, Àríyá placeholder and deterministic client account/avatar evidence;
- Home is a quiet `PortalPageHeader` + `StatePanel` validation surface with no fake business data;
- root route explicitly defers authentication/authorization to FOUND-001F;
- no package dependency or security override drift was introduced.

E1 closure blockers:
1. Notifications `DropdownMenuTrigger asChild` currently wraps a `div` containing the IconButton, so Radix trigger semantics attach to the wrapper instead of the actual button. The actual IconButton must be the trigger; position the unread Badge separately without stealing trigger semantics.
2. Account trigger uses hardcoded `focus-visible:ring-2` / `ring-rs-action-primary` styling. Normalize to the frozen focus-variable contract.
3. The Re:Solve brand Link removes outline without supplying the frozen visible focus treatment. Give the real Link the canonical focus-variable contract.
4. `PortalNavigation` imports NavigationMenu directly from `@/components/core/navigation/NavigationMenu` instead of the public `@/components/core` boundary; normalize to the Core export boundary and remove unused imports.
5. `PortalTopBar` imports `toast` directly from `sonner`; shell code should consume the Core toast export. Normalize to `@/components/core`.
6. Sign-out styling references non-canonical `rs-action-danger`. Use accepted destructive action/status tokens; canonical destructive action authority is `rs-action-destructive` / `rs-action-destructive-*`.
7. Portal shell/topbar content uses hardcoded responsive horizontal gutters (`px-4/md:px-6/lg:px-8`) instead of canonical `--spacing-rs-gutter-mobile/tablet/desktop` tokens. Normalize shell horizontal gutters to the established token contract while preserving the comfortable Portal max width.

Preserve the accepted E1 visual direction, root replacement, desktop-vs-mobile navigation model and placeholder-only behavior while making only this closure pass.

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
Run one narrow FOUND-001E1-FIX pass to correct Portal trigger semantics, canonical focus treatment, Core public-boundary imports/toast use, destructive token usage, and canonical gutter tokens. Preserve the accepted Portal shell visual direction and root replacement. If clean, freeze E1 and proceed to E2 route-aware Portal navigation/shell composition rather than business-domain implementation.