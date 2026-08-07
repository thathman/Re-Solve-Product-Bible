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
- shell chrome is first-class;
- reusable patterns live in the Core Framework;
- a Component Gallery exists before broad module work;
- tables/forms/notifications/avatar/navigation have canonical behavior;
- plugin surfaces remain coherent;
- phone, tablet, desktop, keyboard and focus states are deliberately designed.
