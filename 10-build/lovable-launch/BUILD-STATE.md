# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL NEXT**

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

### D1 — Chrome & visual foundation
Canonical Admin shell at `/admin` includes:
- TanStack layout route with `Outlet` and explicit note that auth/authz is deferred to FOUND-001F;
- shell-owned `AdminShell`, `AdminSidebar`, `AdminTopBar`, `AdminPageHeader`;
- frozen Core Sidebar composition, icon collapse and mobile Sheet;
- strong TopBar with Search, Notifications, Àríyá and account/avatar area;
- one semantic `main` landmark via SidebarInset;
- deterministic local demo identity `Amara Okafor / Administrator`;
- responsive semantic gutters, light/dark tokens, no page-level horizontal overflow;
- root `/` left untouched.

### D2 — Route skeletons & Command/Search
Canonical Admin root routes:
- `/admin`
- `/admin/clients`
- `/admin/crm`
- `/admin/properties`
- `/admin/projects`
- `/admin/sales`
- `/admin/billing`
- `/admin/support`
- `/admin/platform`

Canonical behavior:
- typed shell-local `admin-nav.ts` shared by Sidebar, TopBar and Command/Search;
- all root destinations are real TanStack Links with route-aware active state and `aria-current="page"`;
- mobile navigation closes the Sidebar Sheet;
- placeholder pages remain `AdminPageHeader` + `StatePanel`, with no domain implementation;
- shell-owned Command dialog opens from desktop/mobile Search and Cmd/Ctrl+K;
- Cmd/Ctrl+K is the only global Admin shortcut introduced in Foundation;
- Command navigation uses TanStack navigation with no document reload;
- Notifications and `Open Àríyá` remain truthful quick-access placeholders.

### D3 — Composition closure
Canonical composition includes:
- `AdminBreadcrumbs` with `Home / Current Section` on non-Home root routes using a real TanStack Home Link and `BreadcrumbPage` current item;
- Home remains breadcrumb-free;
- `AdminAriyaPanel` as Àríyá's canonical FOUND-001 Admin placement: right-side Core Sheet with semantic title/description and truthful placeholder StatePanel;
- `AdminShell` owns only local `commandOpen` and `ariyaOpen` shell state;
- TopBar large/narrow Àríyá controls and Command `Open Àríyá` item open the same Sheet;
- Notifications remain the anchored TopBar DropdownMenu with deterministic unread count `3`;
- account Profile, Preferences and Sign out produce truthful placeholder feedback without auth/account routes.

### D4 — Final closure review
**PASS — NO BLOCKERS / NO MODIFICATIONS**
Verified as one system across desktop/tablet/mobile:
- all nine Admin routes render inside the same shell;
- route active/current semantics, TopBar context and breadcrumbs agree;
- Sidebar expanded/collapsed/mobile behavior is coherent;
- Cmd/Ctrl+K Command/Search works and remains the only global shortcut;
- Àríyá uses one shared Sheet state across all shell triggers;
- Notifications remain anchored and placeholder-only;
- account actions remain truthful placeholders;
- one primary main landmark; icon-only controls are named; focus/keyboard behavior remains coherent;
- light/dark semantic tokens remain intact;
- Core is unchanged;
- package/security state is unchanged;
- root `/` remains untouched;
- zero prompt/task leakage reported;
- reported frozen install, build, lint and TypeScript checks pass.

FOUND-001D is closed. Do not reopen it without a concrete regression or a later requirement exposing a missing shell contract.

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
- `src/routes/index.tsx` remains the untouched placeholder and is reserved for the Client Portal surface during FOUND-001E.

## UI/product direction
- Re:Solve Core is the public UI boundary.
- Admin navigation stays simple and shallow, closer to Perfex/Brevo than Odoo/Twenty.
- Àríyá is Re:Solve's built-in AI surface; Chatwoot keeps Captain separately.
- shadcn-vue is visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.
- No timesheets, HR, or client service-consumption concepts.

## Next action
Begin FOUND-001E as small supervised Client Portal Shell slices. The client-facing portal owns `/` and other non-admin routes, while staff/admin remains under `/admin`. First Portal slice should establish client-facing shell/chrome, responsive navigation and a quiet Home validation surface using frozen Core, without auth, business-domain implementation, database work, real notifications, or real Àríyá functionality.