# Re:Solve Core UI Component Framework

## Purpose
Re:Solve requires a first-class, shared UI component framework for Admin, Client Portal, core modules, plugins and connectors. UI chrome and reusable interaction quality are product infrastructure, not optional polish.

Navigation, top bar, avatar/account, notifications, tables, forms, dialogs, drawers, record headers, assistant surfaces and application states must receive the same design attention as business features.

## Mandatory source hierarchy
1. **Re:Solve Product Design Language** — final authority.
2. **shadcn/ui** — primary open-code/source-owned component foundation.
3. **Untitled UI React** — major source and influence for polished navigation, forms, tables, filters, overlays, calendars and application composition.
4. **Tremor** — major source and influence for metrics, reports, monitoring and data visualization.
5. **React Aria / Base UI / Radix** — use the strongest accessible primitive behavior for the interaction.
6. **TanStack Table / TanStack Query** — preferred headless table and async-data foundations where appropriate.
7. Approved specialist libraries such as dnd-kit, React Flow or a true enterprise grid only when a documented workflow needs them.

Re:Solve must use these sources heavily without looking like several component libraries stitched together.

### shadcn-vue pattern reference policy
`shadcn-vue` is an approved visual, composition and block-pattern reference because its current component/block catalogue includes useful modern application patterns that align with Re:Solve. It is **not** an implementation runtime for Re:Solve because the application is React/TanStack.

Rules:
- when a liked `shadcn-vue` component/block has a current React `shadcn/ui` equivalent, use/import the React source-owned implementation and adapt it into Re:Solve Core UI;
- never add Vue runtime/components to the React application merely to reproduce a design;
- when a useful `shadcn-vue` pattern has no suitable React equivalent, port only the interaction/composition pattern into React using the accepted Re:Solve primitive base;
- all imported/adapted patterns remain subject to Re:Solve tokens, accessibility, responsive behavior, provenance and Core ownership rules;
- the `dashboard-01`, `sidebar-07`, restrained `sidebar-03`, auth and calendar block families are approved layout references, not page templates to copy wholesale;
- Re:Solve navigation rules override block defaults: no app launcher, no giant module tree, no uncontrolled submenu nesting and no stock shadcn shell identity.

### Canonical shadcn component intake
The Core Framework should deliberately intake the useful shadcn catalogue rather than adding components ad hoc.

**Already canonical or currently being normalized**
- Button / IconButton
- Avatar
- Badge / StatusBadge
- Input
- Textarea
- Checkbox
- Radio Group
- Switch
- Select
- Separator
- Skeleton
- Tooltip
- FormField / FieldGroup (Re:Solve-owned semantics rather than duplicating stock Field blindly)

**Core interaction intake**
- Accordion
- Alert
- Alert Dialog
- Breadcrumb
- Button Group
- Collapsible
- Command
- Context Menu
- Dialog
- Drawer
- Dropdown Menu
- Empty
- Hover Card
- Input Group
- Item
- Kbd
- Popover
- Progress
- Scroll Area
- Sheet
- Spinner
- Tabs
- Toast/Sonner — choose one canonical notification-toast implementation after repository audit; do not keep both as competing APIs
- Toggle
- Toggle Group

**Advanced input / workflow intake**
- Attachment
- Calendar
- Combobox
- Date Picker
- Date Range Picker / range-calendar behavior
- Input OTP / PIN-entry behavior for MFA and step-up flows
- Native Select where a simpler native control is preferable
- Number Field when a real numeric workflow requires it
- Pagination
- Resizable
- Slider when a real settings/domain workflow requires it
- Stepper for guided workflows
- Tags Input for tagging workflows

**Conversation / assistant intake**
- Message
- Bubble
- Message Scroller
- Marker
- Attachment

These are especially relevant to Àríyá, support/conversation views and evidence-rich agent interactions. They must not turn Re:Solve into a generic chat application.

**Later domain/composite intake**
- Questionnaire for surveys, intake and structured forms when those slices begin
- Table as a low-level surface only; operational DataTable remains TanStack Table → Re:Solve DataTable
- Sidebar as a low-level/reference implementation only; AdminSidebar and PortalNavigation remain Re:Solve-owned composites
- Card as a source pattern where needed; avoid indiscriminate cardification
- Chart only where useful as source reference; analytics authority remains Tremor + Recharts

**Not default Core imports**
- Carousel
- Menubar
- Navigation Menu
- Aspect Ratio

These may be added only when a documented workflow actually needs them. Re:Solve should not import components simply because the registry contains them.

## Ownership rule
Before creating a UI pattern:
1. check for an existing Re:Solve Core component;
2. evaluate approved source libraries if none exists;
3. normalize the chosen pattern into Re:Solve tokens, variants and behavior;
4. add it to the Core Framework when reusable;
5. consume the Re:Solve component from product features.

## Framework layers

### Tokens
Canonical tokens cover color, semantic status, typography, spacing, dimensions, radii, borders, elevation, focus, motion, density, breakpoints, safe areas and visualization behavior.

### Primitives
Canonical Re:Solve variants should exist for common controls including Button, IconButton, Link, Avatar, Badge, StatusBadge, Input, Textarea, Select, Combobox, Checkbox, Radio, Switch, DatePicker, DateRangePicker, FileInput, FormField, Tooltip, Popover, DropdownMenu, ContextMenu, Dialog, AlertDialog, Drawer/Sheet, Tabs, Accordion, Command, Toast, Alert, Progress, Skeleton, Separator and ScrollArea.

### Application primitives
The framework must provide or reserve consistent contracts for:
- AppShell
- AdminSidebar
- PortalNavigation
- TopBar
- NavSection / NavItem / NavBadge
- MobileNav
- ContextSwitcher
- GlobalSearch
- CommandPalette
- QuickCreate
- ResolveAvatar
- AccountMenu
- NotificationTrigger / NotificationTray / NotificationItem
- AriyaTrigger / AriyaPanel
- BreadcrumbTrail
- PageHeader / RecordHeader / RecordTabs
- ContextBar / ActionBar
- FilterBar / SavedViewPicker / ViewSwitcher / BulkActionBar
- AttentionItem
- ActivityTimeline / AuditTimeline
- HealthIndicator / FreshnessIndicator
- ConnectorStatus / PluginStatus
- OwnerChip / AssigneePicker
- PermissionGate / StepUpDialog
- SensitiveValue / SensitiveFileCard
- Metric / MetricDelta / StatStrip / InsightPanel / OperationalBrief
- EmptyState / ErrorState / PermissionState / OfflineState / NotBuiltState / ConnectionState

### Domain composites
Domain components such as PropertyPosture, RenewalItem, ProjectProgress, InvoiceStatus, ProposalStatus, IncidentSummary and VaultAccessRequest still consume Core UI primitives.

## Shell quality mandate
The shell is not complete merely because links work. Side navigation, top bar, avatar/account, notification tray, search/command, Àríyá entry, quick create, breadcrumbs, connection state and mobile navigation must be production-quality foundation components.

Each needs intentional normal, hover, focus, pressed, active, disabled, count/unread, long-label, narrow-width and accessibility behavior where applicable.

## Avatar and account
Avatar patterns support image, initials fallback, compact/standard sizes, accessible names and groups.

The Account Menu should expose identity, current role/context, profile, preferences, security/sessions, appearance, keyboard help, permitted Admin/Portal switching and sign out. It must not be a trivial logout menu.

## Notifications
Provide both a strong global trigger/tray and a full Notification Center. Tray items support unread state, restrained priority, grouping, context, primary action and relevant read/archive/snooze controls.

## Àríyá
Àríyá has a distinctive but restrained presence. Avoid the generic floating sparkle-button treatment. Global entry, contextual actions and assistant workspace must expose sources, permission boundaries and confirmations clearly.

## Tables
Use TanStack Table or an equivalent headless engine as the default for operational tables. Re:Solve DataTable should support relevant search, filtering, sorting, selection, bulk actions, saved views, column controls, row actions, pagination/virtualization, keyboard use, responsive alternatives and complete loading/empty/error/stale states.

Use a specialist enterprise grid only when a documented workflow truly needs spreadsheet/grid behavior.

## Async data behavior
Prefer a coherent query/mutation layer such as TanStack Query so loading, retry, stale, optimistic and background-refresh behavior is consistent instead of reinvented page by page.

## Analytics
Tremor should heavily influence analytics and monitoring presentation. Charts must answer an operational question. Prefer compact metrics, trackers, trends or tables when a large chart adds no decision value.

## Specialist interactions
- dnd-kit is the preferred direction for accessible reordering and drag/drop.
- React Flow is the preferred direction for automation/process canvases when a canvas is warranted.

## Admin versus Portal
Admin uses denser, keyboard-forward composition. Portal uses calmer, guided, touch-friendly composition. Both share tokens and canonical components.

## Component Gallery
FOUND-001 must establish a development-only Component Gallery or Storybook-equivalent surface showing canonical components, variants, states, realistic content lengths and responsive behavior. This becomes the visual QA and regression surface.

## Extension contract
Plugins consume approved Re:Solve components/tokens and named extension slots. They must not introduce an unrelated design system.

## Accessibility
WCAG 2.2 AA is required. Primitive choice should favor mature accessible behavior over custom imitation.

## Acceptance criteria
- shadcn, Untitled UI and Tremor materially influence implementation quality;
- shadcn-vue may materially influence composition/block choices without introducing Vue runtime code;
- shell chrome is first-class;
- reusable patterns live in the Core Framework;
- a Component Gallery exists before broad module work;
- tables/forms/notifications/avatar/navigation have canonical behavior;
- plugin surfaces remain coherent;
- phone, tablet, desktop, keyboard and focus states are deliberately designed.
