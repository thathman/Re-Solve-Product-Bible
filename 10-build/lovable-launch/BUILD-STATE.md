# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D1 ADMIN SHELL CONDITIONAL / NARROW FIX NEXT**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — public, specification/planning only.
- Current Lovable app: `thathman/re-solve-c560d62c` — private, `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Accepted foundation
FOUND-001A, FOUND-001B and the complete FOUND-001C Core UI framework through C5E are accepted/canonical/frozen. Do not reopen frozen UI slices without a concrete regression or a later shell/domain requirement that exposes a genuinely missing contract.

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
**CONDITIONAL — NARROW CLOSURE REQUIRED**

Verified-good D1 architecture:
- `/admin` is a TanStack layout route with `Outlet`; `/admin/` provides the Home validation surface.
- The route explicitly documents that authentication/authorization is deferred to FOUND-001F; no fake auth guard was added.
- `AdminShell`, `AdminSidebar`, `AdminTopBar`, and `AdminPageHeader` live under `src/components/shell/admin/`, keeping shell composition outside frozen Core.
- Sidebar composition uses the frozen Core Sidebar family, provisional shallow groups, active Home, disabled future destinations, icon-collapse and mobile Sheet behavior.
- TopBar includes Search, Notifications, Àríyá and account/avatar evidence; all interactions are placeholder-only.
- Admin Home contains only shell-validation copy and no fake KPI/domain data.
- `/` remains untouched; package/security state remains canonical and no dependency was added.
- generated `routeTree.gen.ts` correctly includes `/admin` and `/admin/`.

D1 closure blockers:
1. `SidebarInset` already renders the document's `main` landmark, but `AdminShell` nests another `<main>` inside it. Replace the inner landmark with a non-main content container.
2. Desktop Search is a raw button without the frozen focus-variable contract. Prefer frozen Core Button composition or apply the exact canonical focus variables.
3. Account trigger uses hardcoded `focus-visible:ring-2 focus-visible:ring-rs-action-primary`; normalize it to the frozen focus-variable contract.
4. Notifications `DropdownMenuTrigger asChild` currently wraps a non-focusable `div`, so Radix trigger semantics/ARIA attach to the wrapper instead of the actual IconButton. The actual interactive button must be the trigger; position the unread Badge without stealing trigger semantics.
5. Àríyá uses `IconButton size="icon-compact"` while embedding visible text at large screens. Core IconButton has a fixed icon width, so use a real Button for the labeled desktop/tablet control and an IconButton for narrow screens.
6. Demo avatar loads from an external DiceBear URL, violating D1's static/local/no-network shell evidence rule. Use ResolveAvatar initials/fallback with no remote `src`.
7. Future disabled Sidebar destinations use the frozen disabled button contract, whose pointer-events are disabled; their internal Sidebar tooltip cannot be relied on for collapsed pointer discovery. Use a shell-level noninteractive composition that remains visibly/semantically unavailable and still exposes a collapsed label without reopening Core.
8. Clean minor shell hygiene while touching these files (unused imports, explicit Home current-page semantics where appropriate) without changing the accepted IA evidence.

Do not redesign the shell during the fix; preserve the accepted visual direction and route architecture.

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
Run one narrow FOUND-001D1-FIX pass to correct shell landmarks, focus semantics, DropdownMenu trigger semantics, responsive Àríyá composition, static avatar evidence, and disabled-future-nav collapsed labeling. Preserve the accepted shell architecture and visual direction. If clean, freeze D1 and proceed to the next small Admin-shell slice rather than business-domain implementation.