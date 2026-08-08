# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D1 ADMIN SHELL ACCEPTED/FROZEN — FOUND-001D2 NEXT**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — public, specification/planning only.
- Current Lovable app: `thathman/re-solve-c560d62c` — private, `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Accepted foundation
FOUND-001A, FOUND-001B and the complete FOUND-001C Core UI framework through C5E are accepted/canonical/frozen. FOUND-001D1 Admin Shell Chrome & Visual Foundation is also accepted/canonical/frozen. Do not reopen frozen slices without a concrete regression or a later requirement that exposes a genuinely missing contract.

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
- future destinations rendered as shell-local, visibly disabled, noninteractive `aria-disabled="true"` composition with collapsed tooltip discovery and no fake links/buttons;
- TopBar Search using frozen Core Button/focus behavior;
- Notifications DropdownMenu semantics attached to the actual IconButton trigger;
- responsive Àríyá controls: labeled Core Button at large widths and compact IconButton at narrow widths;
- deterministic local avatar fallback with no remote image request;
- account trigger on the frozen focus-variable contract;
- shell-only placeholder interactions for Search, Notifications, Àríyá and Sign out;
- Admin Home validation copy only, with no fake KPI/domain data;
- responsive canonical gutters, light/dark semantic tokens, and no page-level horizontal overflow;
- `/` remains untouched;
- package/security state remains canonical, no dependency added;
- generated route tree correctly includes `/admin` and `/admin/`.

A lint/type-only cleanup in `/ui` removed unnecessary DataTable casts during the D1 final closure. It did not alter frozen Core APIs or DataTable behavior and is accepted as non-blocking hygiene.

Do not reopen D1 during later Admin-shell slices unless a concrete shell regression appears.

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
Begin FOUND-001D2 as a small Admin-shell slice focused on route-aware shell navigation and shell-level global Command/Search composition. Keep business-domain implementations as placeholders only; do not implement auth, database, real notifications, real Àríyá, or business data. Preserve frozen D1 chrome and all Core APIs.