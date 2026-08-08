# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D1-D3 ADMIN SHELL ACCEPTED/FROZEN — ADMIN SHELL CLOSURE REVIEW NEXT**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — public, specification/planning only.
- Current Lovable app: `thathman/re-solve-c560d62c` — private, `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Accepted foundation
FOUND-001A, FOUND-001B and the complete FOUND-001C Core UI framework through C5E are accepted/canonical/frozen. FOUND-001D1-D3 Admin Shell slices are also accepted/canonical/frozen. Do not reopen frozen slices without a concrete regression or a later requirement that exposes a genuinely missing contract.

## Currency display convention
**CANONICAL**
- Internal/data/API currency identity remains explicit via ISO codes.
- Normal user-facing UI uses locale-appropriate currency symbols where unambiguous.
- No universal default currency.

## Security memory
**ACCEPTED / CANONICAL**
The scanner-oriented Re:Solve Security Memory is canonical. Authentication/authorization remain server-authoritative; final auth/RLS/Vault/Action Registry are not yet implemented; no vulnerability exceptions are accepted.

## SECURITY-GATE-001 — Dependency remediation
**ACCEPTED / CLOSED**
Canonical package security state:
- `@tanstack/react-router`: `^1.170.18`
- `@tanstack/react-start`: `^1.168.32`
- `@tanstack/router-plugin`: `^1.168.23`
- `@tanstack/react-table`: `8.20.5`
- no direct `@tanstack/router-core`
- no direct `js-yaml`
- top-level Bun override: `"js-yaml": "4.3.1"`
- accepted scan cleared `GHSA-5p4m-2wfm-xmqj` with no remaining High/Critical findings.

## FOUND-001C — Core UI Framework
**ACCEPTED / CANONICAL / FROZEN**

Accepted Core families include:
- actions/primitives: Button, IconButton, Badge, StatusBadge, ResolveAvatar, Tooltip, Separator, Skeleton, Metric, MetricDelta;
- forms: Input, Textarea, Checkbox, RadioGroup, Switch, Select, NativeSelect, FormField, FieldGroup, InputGroup, Toggle/ToggleGroup;
- overlays/disclosure: Dialog, AlertDialog, Sheet, Drawer, Popover, HoverCard, DropdownMenu, ContextMenu, Accordion, Collapsible, Tabs, ScrollArea;
- feedback/composition: Alert, Empty, StatePanel, Spinner, Progress, Toast, Item, ButtonGroup, Kbd, Breadcrumb;
- advanced input/date: Command, Combobox, InputOTP, Slider, Calendar, DatePicker, DateRangePicker;
- display/layout: Card, Table, AspectRatio, Pagination, Resizable;
- DataTable: generic TanStack Table engine with sorting, pagination, global/text/select filtering, column visibility, opt-in current-page row selection, truthful empty/loading/error/filtered states, responsive containment and explicit stable-row-ID boundary;
- navigation foundations: Sidebar family and NavigationMenu family.

### DataTable closure
FOUND-001C5D1-D3 are frozen. Server/manual pagination/sorting/filtering, URL state, saved views, persistent ordering/visibility, column pinning, bulk actions, exports and domain adapters/actions remain deferred beyond Foundation Core.

### FOUND-001C5E — Navigation Foundations
**ACCEPTED / CANONICAL / FROZEN**
Canonical C5E includes:
- Re:Solve-owned SidebarProvider/useSidebar and full Sidebar primitive family;
- controlled/uncontrolled desktop state and separate mobile-open state;
- no Core persistence policy and no global sidebar keyboard shortcut;
- canonical `--spacing-rs-sidebar-width` / `--spacing-rs-sidebar-collapsed` reservations;
- frozen Core Button/Input/Separator/Sheet/Skeleton/Tooltip composition;
- semantic `ul`/`li`, `asChild` link/action composition, active surface + font + action-primary indicator, collapsed tooltips and mobile Sheet semantics;
- deterministic SidebarMenuSkeleton (`textWidth`, default 70%), no render-time randomness;
- Re:Solve NavigationMenu on pre-existing `@radix-ui/react-navigation-menu` with explicit Core exports, `asChild`, Radix keyboard/ARIA behavior, canonical focus variables, non-color active distinction and viewport-safe max-width;
- gallery evidence for expanded/collapsed/nested/mobile Sidebar plus horizontal/hierarchical/current NavigationMenu;
- NavigationMenu provenance: declared `^1.2.14`, resolved `1.2.22`, MIT, pre-existing dependency, first Re:Solve Core consumption FOUND-001C5E;
- no package/lock/security drift.

Core UI is closed for FOUND-001.

## FOUND-001D1 — Admin Shell Chrome & Visual Foundation
**ACCEPTED / CANONICAL / FROZEN**

Canonical D1 includes:
- `/admin` TanStack layout route with `Outlet` and `/admin/` Home validation surface;
- explicit engineering note that authentication/authorization is deferred to FOUND-001F; no fake auth guard;
- shell-owned `AdminShell`, `AdminSidebar`, `AdminTopBar`, and `AdminPageHeader` under `src/components/shell/admin/`;
- frozen `SidebarInset` as the single Admin `main` landmark, with shell content scrolling inside a neutral container;
- shallow provisional Sidebar groups, real active Home link, icon-collapse and mobile Sheet behavior;
- Home `aria-current="page"` semantics when active;
- TopBar Search using frozen Core Button/focus behavior;
- Notifications DropdownMenu semantics attached to the actual IconButton trigger;
- responsive Àríyá controls: labeled Core Button at large widths and compact IconButton at narrow widths;
- deterministic local avatar fallback with no remote image request;
- account trigger on the frozen focus-variable contract;
- shell-only placeholder interactions for Notifications, Àríyá and Sign out;
- Admin Home validation copy only, with no fake KPI/domain data;
- responsive canonical gutters, light/dark semantic tokens, and no page-level horizontal overflow;
- `/` remains untouched;
- package/security state remains canonical, no dependency added;
- generated route tree correctly includes `/admin` and `/admin/`.

A lint/type-only cleanup in `/ui` removed unnecessary DataTable casts during the D1 final closure. It did not alter frozen Core APIs or DataTable behavior and is accepted as non-blocking hygiene.

Do not reopen D1 during later Admin-shell slices unless a concrete shell regression appears.

## FOUND-001D2 — Admin Route Skeletons & Global Command/Search
**ACCEPTED / CANONICAL / FROZEN**

Canonical D2 includes:
- typed shell-local `admin-nav.ts` shared by Sidebar, TopBar route context, and Command/Search;
- real placeholder routes for `/admin/clients`, `/admin/crm`, `/admin/properties`, `/admin/projects`, `/admin/sales`, `/admin/billing`, `/admin/support`, and `/admin/platform` under the existing `/admin` layout;
- placeholder pages remain `AdminPageHeader` + `StatePanel` validation surfaces with no domain schemas, mock records, forms, APIs, tables or business logic;
- Sidebar root destinations are real TanStack `Link` elements with route-aware active state and `aria-current="page"`;
- mobile navigation closes the Sidebar Sheet using `setOpenMobile(false)` while desktop behavior remains unchanged;
- shell-owned `AdminCommandMenu` composes frozen Core Command primitives and is opened by both desktop/mobile Search triggers;
- Cmd/Ctrl+K is the sole D2 global shortcut, with `preventDefault` and listener cleanup;
- Command navigation uses TanStack `navigate`, closes after selection, and does not reload the page;
- Notifications and `Open Àríyá` remain placeholder-only Quick Access command items with no fake global shortcuts;
- TopBar current section title derives from the shared navigation model;
- the obsolete D1 `FutureDestination` helper and Tooltip plumbing were removed once all D2 root routes became real links;
- no route, Core, package, lockfile or security drift was introduced.

Do not reopen D2 during later Admin-shell slices unless a concrete routing/Command regression appears.

## FOUND-001D3 — Admin Shell Composition Closure
**ACCEPTED / CANONICAL / FROZEN**

Canonical D3 includes:
- shell-owned `AdminBreadcrumbs` implementing `Home / Current Section` for non-Home Admin root routes using frozen Core Breadcrumb primitives;
- breadcrumb Home is a real TanStack `Link` to `/admin`; current section is `BreadcrumbPage` and is not clickable;
- `AdminPageHeader` remains shell-owned and composes the canonical breadcrumb behavior through a small `showBreadcrumbs` flag;
- Home remains breadcrumb-free while section placeholder pages show the canonical two-level breadcrumb;
- shell-owned `AdminAriyaPanel` establishes Àríyá's canonical FOUND-001 Admin placement as a right-side Core Sheet with semantic title/description and a truthful `StatePanel` placeholder;
- `AdminShell` owns exactly two local shell states: `commandOpen` and `ariyaOpen`; no global state library/context was introduced;
- both responsive TopBar Àríyá triggers and the Command `Open Àríyá` item open the same Sheet state; no Àríyá toast remains on those trigger paths;
- Notifications remain anchored as the TopBar DropdownMenu with deterministic unread count `3`; the Command Notifications item remains a truthful placeholder action rather than programmatically controlling the dropdown;
- account menu retains deterministic shell identity `Amara Okafor / Administrator` and gives explicit placeholder feedback for Profile, Preferences and Sign out without adding auth/account routes or persistent account state;
- D2 route-aware TopBar context, Cmd/Ctrl+K command behavior, real Sidebar links and mobile-close behavior remain intact;
- no domain data, auth, permissions, database, real notifications or AI backend was added;
- no Core/package/security/root-route drift was introduced.

Non-blocking hygiene: unused React imports remain in `AdminBreadcrumbs.tsx` and `AdminSidebar.tsx`. They have no runtime effect and do not reopen D3; remove opportunistically only during a later shell-local edit.

Admin shell implementation is now closed for FOUND-001 pending one brief no-feature closure review.

## FOUND-001C5E gap-audit deferrals
Build in shell (FOUND-001D/E):
- PageHeader
- CommandBar / CommandPalette composition over frozen Command
- AppLayout containers
- DescriptionList / key-value detail composition

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
- `/ui` is development/Lovable gallery surface and redirects to `/` in production through route `beforeLoad`.
- `src/routes/index.tsx` remains the untouched Lovable placeholder at this checkpoint.

## UI/product direction
- Re:Solve Core is the public UI boundary.
- Keep Admin navigation simple and shallow, closer to Perfex/Brevo than Odoo/Twenty.
- Strong Sidebar, TopBar, avatar/account area, notifications trigger, global search trigger and Àríyá entry point are shell priorities.
- shadcn-vue remains visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.
- No timesheets, HR, or client service-consumption concepts.

## Next action
Run one brief FOUND-001D4 Admin Shell Closure Review with no planned feature implementation. Audit desktop/tablet/mobile shell behavior, route/nav/search/breadcrumb/Notifications/Àríyá/account composition, frozen Core boundaries, package/security/root-route stability, and prompt leakage. Only fix objectively verified regressions. If clean, close FOUND-001D and begin FOUND-001E Client Portal Shell.