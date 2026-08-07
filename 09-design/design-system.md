# Re:Solve Design System

## Purpose
This specification defines the shared interaction and component system used by Admin OS and Client Portal. The canonical implementation layer is the Re:Solve Core UI Component Framework in `09-design/core-ui-framework.md`.

## Mandatory component sources
Re:Solve must heavily use and be influenced by:
- shadcn/ui
- Untitled UI React
- Tremor
- React Aria / Base UI / Radix according to primitive quality
- TanStack Table / TanStack Query where appropriate
- approved specialist libraries when genuinely required

The design system owns the final Re:Solve visual/interaction language. Feature pages should consume Re:Solve components rather than independently styling raw library components.

## Component hierarchy

### Primitive layer
Buttons, links, avatar, inputs, selects/comboboxes, overlays, tabs, form controls, calendars, badges/status, tables, command menu, alerts, skeletons and other canonical controls.

### Application/composite layer
Examples include:
- AppShell / AdminSidebar / PortalNavigation / TopBar
- ResolveAvatar / AccountMenu
- GlobalSearch / CommandPalette / QuickCreate
- NotificationTrigger / NotificationTray / NotificationItem
- AriyaTrigger / AriyaPanel
- PageHeader / RecordHeader / RecordTabs
- AttentionItem
- ActivityTimeline / AuditTimeline
- PropertyPosture / ConnectorHealth
- FilterBar / SavedViewPicker / ViewSwitcher / BulkActionBar
- DataTable
- PermissionGate / StepUpDialog
- SensitiveValue / SensitiveFileCard
- Metric / StatStrip / InsightPanel
- Empty/Error/Permission/Offline/NotBuilt/Connection states

### Feature layer
Feature screens compose shared primitives and composites. They do not silently redefine established behavior.

## Layout tokens
Define consistent tokens for page gutters, content widths, sidebar/topbar dimensions, panel padding, table density, control heights, overlays, responsive breakpoints and mobile safe areas.

Avoid excessive nested cards. Borders and whitespace should do most structural work; shadows remain restrained.

## Typography
Define tokens for page title, record title, section title, panel title, body, table body, metadata, label, helper, code/identifier and numeric emphasis. Financial/metric figures should use tabular numerals where possible.

## Iconography
Use one coherent icon family by default. Pair unfamiliar icons with text. Status icons need accessible labels. Plugin icons must fit the system.

Àríyá should have a recognizable Re:Solve-native mark/treatment rather than relying solely on a generic sparkle icon.

## Semantic status
Reusable semantic states include neutral, draft, pending, active, completed, paused, warning, overdue, failed, cancelled, archived, disconnected, degraded and unknown. Domain names map onto shared visual semantics.

## Buttons/actions
Action priority:
- primary
- secondary
- tertiary/ghost
- destructive
- inline/contextual

A page normally has one visually dominant primary action. High-risk actions use explicit language and Action Registry policy.

## Forms
Forms support labels, help, validation, server errors, disabled/read-only, loading/saving, unsaved-change protection, keyboard/focus behavior, conditional fields, sensitive treatment and responsive composition.

Use React Hook Form + Zod or Lovable's strongest compatible equivalent when appropriate.

## Data tables
Operational tables are first-class interfaces.

Default engine direction: TanStack Table or equivalent headless table behavior normalized into Re:Solve DataTable.

Relevant capabilities:
- search
- quick/advanced filters
- sorting
- pagination/virtualization
- selection
- bulk actions
- configurable/pinned columns
- saved views
- exports with permission checks
- row actions
- keyboard behavior
- stale/retrying/error/empty/loading states
- responsive transformation

Mobile must not simply shrink a 10-column table. Use priority data, stacked rows, drawers or cards.

A specialist enterprise grid is permitted only for workflows that genuinely require spreadsheet/grid behavior.

## Filtering and saved views
Filtering is consistent across modules. Support quick filters, advanced filters, active chips, clear all, date presets, ownership/status/organisation/property filters and personal/team/shared Saved Views where allowed.

## Command palette and search
Global command/search supports navigation, record search, Quick Create, recent records, favorites, registered actions and Àríyá entry. Results show type, parent context, status and match reason where useful.

## Record headers
Canonical RecordHeader supports type/eyebrow, title, status, human reference, ownership, parent, key metadata, primary action, overflow actions, favorite and plugin actions while remaining compact.

## Tabs/subnavigation
Use tabs for parallel views of one record/major area. Preserve deep links and counts when meaningful. Mobile uses scrollable/alternative selection rather than broken compression.

## Overlays
Use popover for lightweight choice, dialog for bounded decisions, drawer/sheet for side-context work and full pages for deep workflows. Avoid modal chains.

## Notifications
Toasts are transient feedback only. Persistent user awareness lives in Notifications. Global Notification chrome must be a polished Core Framework experience with strong unread/group/action behavior.

## Avatar/account
ResolveAvatar and AccountMenu are canonical shell components. AccountMenu must include meaningful identity/context, profile/preferences/security/appearance/help and sign-out behavior rather than a minimal logout dropdown.

## Àríyá
AriyaTrigger/AriyaPanel are canonical components. Avoid floating-bubble clichés and visually disconnected assistant styling.

## Sensitive information
Sensitive values/files are masked by default and use explicit reveal/copy/download actions, permission checks, optional step-up and audit.

## Files
File components support upload progress, drag/drop, mobile picker/camera, preview, metadata, version, replace, download, permission state, confidential routing, processing/failure states.

## Charts/visualization
Tremor should heavily influence chart/metric composition. Every visualization needs a real operational question, clear period/filter context, accessible representation and empty/error state. Prefer a number, tracker or small table when clearer than a chart.

Do not casually mix chart libraries.

## Drag/drop/canvas
Use dnd-kit as preferred drag/reorder direction. Use React Flow for automation/process topology when a canvas materially improves the workflow.

## Responsive behavior
Admin uses adaptive/collapsible navigation, persistent search/notification access, responsive table transformations and sheets for secondary controls.

Portal prioritizes phone-first tasks, accessible primary actions, support, approvals, invoices, files and notifications. Installed PWA must feel native to the product.

## PWA states
Shared components expose offline, reconnecting, update available, install available, push permission, queued safe action, sync failed and sync restored where relevant.

## Accessibility
Every shared component supports keyboard operation, semantic screen-reader behavior, focus order/return, reduced motion, text zoom, contrast, touch targets and announced errors. Target WCAG 2.2 AA.

## Themes/branding
Tokens permit light/dark and controlled Operating Entity/Brand identity. Branding can affect logo, approved accents and selected portal/email/document surfaces without overriding core semantic accessibility.

## Plugin extension contract
Plugins may contribute navigation entries, record tabs, settings panels, dashboard widgets, actions, fields, columns and command actions only through approved slots and Core UI components.

## Component Gallery
A development-only Component Gallery/Storybook-equivalent is mandatory from FOUND-001. It should demonstrate canonical components, realistic content, state variants and responsive behavior.

## Design acceptance gate
Before a reusable component becomes canonical or a major UI slice is complete:
- verify desktop/tablet/phone;
- verify keyboard/focus;
- verify empty/error/loading/read-only/offline/stale states;
- verify accessibility;
- verify realistic content lengths;
- verify it does not duplicate an existing component;
- verify shadcn/Untitled/Tremor/Core UI sourcing is appropriate;
- verify it fits the navigation/application-chrome rules;
- verify it appears correctly in Component Gallery when reusable.
