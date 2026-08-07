# Re:Solve Design System

## 1. Purpose

This specification defines the shared interaction and component system used by both the Admin OS and Client Portal. It is intended to make the product feel coherent while still allowing different density and navigation patterns for staff and clients.

## 2. Core implementation principle

Use high-quality accessible primitives first. Prefer shadcn/ui and its underlying Radix-compatible patterns, but allow equally strong alternatives when they materially improve a specific interaction, especially for:

- advanced data grids;
- command palettes;
- rich text editing;
- charts;
- file viewers;
- date/time scheduling;
- drag-and-drop workspaces;
- kanban;
- complex filtering;
- virtualized lists.

Do not create bespoke controls simply to look different.

## 3. Component hierarchy

Components should be layered:

### Primitive layer
Buttons, inputs, selects, dialog, sheet, popover, tooltip, tabs, accordion, dropdown, checkbox, radio, switch, calendar, toast, separator, avatar, badge, table primitives, command menu.

### Re:Solve composite layer
Examples:

- `RecordHeader`
- `RecordStatus`
- `AttentionItem`
- `ActivityTimeline`
- `NotificationItem`
- `PropertyHealth`
- `ConnectorHealth`
- `Money`
- `DateTime`
- `UserChip`
- `OrganisationChip`
- `PropertyChip`
- `PermissionGate`
- `QuickCreate`
- `BulkActionBar`
- `FilterBar`
- `SavedViewPicker`
- `DataViewSwitcher`
- `EmptyState`
- `FailureState`
- `OfflineState`
- `SensitiveValue`
- `VaultFile`
- `AuditEntry`
- `ProgressState`
- `ClientActionCard`

### Feature layer
Feature screens compose primitives and shared composites. They should not silently redefine established behavior.

## 4. Layout tokens

Define consistent tokens for:

- page gutters;
- content max widths;
- sidebar widths;
- topbar heights;
- panel padding;
- table row density;
- control heights;
- modal widths;
- drawer widths;
- responsive breakpoints;
- mobile safe-area spacing.

Compact and comfortable density modes may be supported later, but the default Admin density should already be efficient.

## 5. Surface hierarchy

Avoid excessive nested cards. Use these levels intentionally:

1. page canvas;
2. section/panel surface;
3. elevated overlay;
4. selected/active state.

Borders and whitespace should do most of the structural work. Shadows should be restrained.

## 6. Typography scale

Define tokens for:

- app/page title;
- record title;
- section title;
- card/panel title;
- body;
- table body;
- metadata;
- label;
- helper text;
- code/identifier;
- numeric emphasis.

Financial figures must use tabular numerals where possible.

## 7. Icon system

Use one coherent icon family by default, such as Lucide-compatible icons.

Rules:

- pair unfamiliar icons with text;
- do not use multiple icon families casually;
- destructive actions must not rely on red iconography alone;
- status icons require accessible labels;
- plugin-provided icons must fit the visual system.

## 8. Status vocabulary

Status treatments must be semantic and reusable.

Minimum reusable states:

- neutral;
- draft;
- pending;
- active;
- completed;
- paused;
- warning;
- overdue;
- failed;
- cancelled;
- archived;
- disconnected;
- degraded.

Features may define domain-specific status names, but visual mappings should reuse shared semantic tokens.

## 9. Buttons and actions

Action priority:

- primary;
- secondary;
- tertiary/ghost;
- destructive;
- inline contextual action.

A page should usually have one visually dominant primary action.

High-risk actions require explicit language, not ambiguous labels such as `Confirm`.

## 10. Forms

Standard forms must support:

- labels;
- descriptions;
- required indicators;
- validation messages;
- server errors;
- disabled/read-only fields;
- loading/saving states;
- dirty-state protection when material;
- keyboard submission where safe;
- accessible help text;
- conditional fields;
- sensitive-field reveal behavior;
- autosave only where loss/recovery semantics are clear.

Use Zod-style schema validation or Lovable's strongest compatible equivalent for consistent client/server rules.

## 11. Data tables

Operational tables are first-class interfaces, not static displays.

Where appropriate they must support:

- search;
- filter chips;
- advanced filters;
- sorting;
- pagination or virtualization;
- selectable rows;
- bulk actions;
- configurable columns;
- saved views;
- export with permission checks;
- row quick actions;
- row open behavior;
- empty results state;
- loading skeleton;
- stale/retrying state;
- responsive transformation.

Mobile must not rely on shrinking a 10-column desktop table. Use priority columns, stacked record rows, drawers, or cards where necessary.

## 12. Filtering system

Filters should be consistent across modules.

Standard concepts:

- quick filters;
- advanced filter builder;
- active filter chips;
- clear all;
- saved view;
- personal/shared views;
- URL-shareable state where safe;
- date presets;
- ownership filters;
- status filters;
- organisation/property filters.

## 13. Command palette and global search

Provide a global keyboard-accessible command/search surface capable of:

- navigation;
- record search;
- quick create;
- recent records;
- saved/favorite destinations;
- common actions;
- AI entry point where appropriate.

Search results should identify record type, parent organisation/property, status, and why the result matched.

## 14. Record header

A standard record header should support:

- record type eyebrow;
- title/name;
- status;
- optional ID/reference;
- ownership;
- parent relationship;
- key metadata;
- primary action;
- action menu;
- favorite/save;
- breadcrumbs or back context;
- plugin actions.

## 15. Tabs and subnavigation

Use tabs when sections are parallel views of one record. Use nested navigation when sections represent major standalone areas.

Tabs should:

- preserve deep links;
- expose counts when meaningful;
- work on mobile using scrollable or dropdown fallback;
- allow plugin extension slots without destroying hierarchy.

## 16. Drawers, dialogs, and full pages

Use:

- popover for lightweight contextual choices;
- dialog for bounded decisions/forms;
- sheet/drawer for side-context work without leaving a page;
- full page for deep workflows, records, and long forms.

Avoid modal chains.

## 17. Notifications and toasts

Toasts are transient confirmation only. They do not replace persistent notification records.

Toast categories:

- success;
- neutral info;
- warning;
- error with retry when applicable.

Critical failures should remain visible in page state or notification center.

## 18. Empty states

Empty states should explain:

- what the area is;
- why it may be empty;
- the next meaningful action;
- whether permissions or configuration are involved.

Avoid generic `No data found` unless the context is self-evident.

## 19. Sensitive information patterns

Sensitive values and files need a dedicated pattern:

- masked by default;
- reveal requires appropriate permission;
- step-up may be required;
- reveal/copy/download actions are explicit;
- audit consequences are visible when useful;
- avoid leaking secrets into client-side logs or copied error messages.

## 20. File patterns

Shared file components should support:

- upload progress;
- drag/drop;
- mobile file picker/camera when appropriate;
- preview;
- filename/type/size;
- owner/context;
- version;
- download;
- replace/new version;
- permission state;
- confidential classification;
- scan/processing state;
- failure/retry.

## 21. Charts and visualization

Charts must answer a real operational question. Every chart requires:

- clear title;
- period/filter context;
- accessible data representation;
- hover/focus details;
- empty state;
- no misleading axes or decorative complexity.

Do not use a chart where a number, trend, or small table is clearer.

## 22. Responsive behavior

### Admin

- collapsible navigation;
- mobile command/search access;
- priority content first;
- advanced controls move into sheets or overflow menus;
- table transformations;
- sticky action bars only when useful;
- no hover-only behavior.

### Portal

- phone-first navigation considerations;
- bottom navigation may be used for highest-frequency areas;
- primary actions remain reachable with one hand where practical;
- attachments, approvals, invoices, notifications, and support must be fully usable on mobile;
- installed PWA mode must feel native to the product, not like a desktop page inside a small browser.

## 23. PWA component requirements

Shared system components must expose states for:

- offline;
- reconnecting;
- update available;
- install available;
- push permission;
- background action queued;
- sync failed;
- sync restored.

## 24. Accessibility requirements

Every shared component must be designed for:

- keyboard operation;
- screen-reader semantics;
- logical focus order;
- focus return after overlays;
- reduced motion;
- text zoom;
- high contrast viability;
- touch target sizing;
- error announcement.

## 25. Theme support

Design tokens should permit future light/dark themes and controlled branding without allowing arbitrary client branding to make the interface inaccessible.

Brand customization may affect:

- logo;
- approved accent token;
- login/portal identity;
- selected email/document surfaces.

Core semantic colors and interaction behavior remain system-controlled.

## 26. Plugin extension contract

The design system must anticipate plugin-provided:

- sidebar/nav entries;
- record tabs;
- settings panels;
- dashboard widgets;
- actions;
- form fields;
- data-table columns;
- status badges;
- command palette actions.

Plugin UI should consume Re:Solve components and tokens rather than shipping unrelated design systems into the product.

## 27. Design acceptance gate

Before a component becomes canonical:

- verify desktop and mobile;
- verify keyboard behavior;
- verify empty/error/loading/read-only states;
- verify dark-theme readiness if theme support is active;
- verify accessibility;
- verify real content lengths;
- verify it does not duplicate an existing component;
- document unusual behavior.
