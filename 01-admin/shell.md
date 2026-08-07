# Admin OS Shell

## 1. Purpose

The Admin OS shell is the staff-facing operational frame for Re:Solve. It must support high-frequency work across clients, properties, projects, finance, support, automations, AI, plugins, connectors, and system administration without becoming a permanently expanded navigation tree.

## 2. Primary users

- workspace owner;
- administrator;
- operations staff;
- client success/account staff;
- project/delivery staff;
- finance staff;
- technical staff;
- support staff where Re:Solve context is needed around Chatwoot;
- restricted specialist roles.

## 3. Core shell responsibilities

The shell owns:

- global navigation;
- global search/command palette;
- quick create;
- notifications;
- user/workspace context;
- breadcrumbs/context path;
- responsive navigation;
- persistent system banners;
- offline/reconnecting state;
- update available state;
- permission-aware route exposure;
- plugin navigation slots.

## 4. Desktop structure

Recommended anatomy:

- left navigation rail/sidebar;
- top utility bar;
- contextual page header inside content area;
- main work canvas;
- optional right-side contextual drawer for transient detail.

The shell should support a compact/collapsed navigation state for power users.

## 5. Navigation philosophy

Navigation should be organized by user intent, not implementation module names.

Primary groups:

### Home
- Dashboard
- My Work

### Relationships
- Clients
- Contacts
- CRM / Sales pipeline

### Delivery
- Properties
- Projects
- Services
- Support

### Commercial
- Sales
- Billing

### Operations
- Knowledge
- Vault
- Monitoring
- Files
- Automations
- Reports

### Platform
- Plugins
- Connectors
- Audit
- Settings

Exact group labels may evolve after flow prototyping, but the information architecture should avoid surfacing every child route in the root sidebar.

## 6. Navigation behavior

- current section clearly highlighted;
- children appear only when relevant or expanded;
- counts only when actionable or meaningful;
- permission-hidden destinations should not appear;
- disabled/configuration-required areas may appear with clear setup state when the user has permission to configure them;
- plugins may add entries only into approved extension slots;
- recent/favorite destinations may appear in command palette rather than permanently bloating navigation.

## 7. Top utility bar

Must provide:

- global search / command palette entry;
- quick create;
- notifications;
- system state indicator when degraded/offline;
- user menu;
- optional workspace switcher if multi-workspace operation is later enabled.

Avoid filling the top bar with feature-specific shortcuts.

## 8. Global search and command palette

Keyboard shortcut should open a unified surface supporting:

- navigate to section;
- search records;
- quick create;
- open recent record;
- run permitted common action;
- access AI assistant;
- open notification;
- plugin-provided commands.

Search result display should show:

- record name/title;
- record type;
- organisation/property context;
- status where helpful;
- secondary identifier;
- match explanation when useful.

## 9. Quick Create

Quick Create should be permission aware and context aware.

Potential objects:

- organisation/client;
- contact;
- lead/opportunity;
- property;
- project;
- task;
- service;
- proposal/estimate;
- invoice;
- note/activity;
- vault item;
- automation.

The menu should rank recently/frequently used actions instead of showing all objects equally.

## 10. Page header contract

Every major page should supply the shell with:

- page/record title;
- optional eyebrow/breadcrumb;
- optional status;
- optional summary metadata;
- primary action;
- secondary actions;
- optional view controls;
- optional saved view/filter state.

Page headers should remain compact enough for operational use.

## 11. Context drawers

Use a right-side drawer for bounded secondary work such as:

- quick record preview;
- edit small metadata set;
- task detail;
- activity detail;
- notification detail;
- connector event detail;
- audit entry detail.

Deep record work should open the full record workspace.

## 12. Persistent banners

The shell may show persistent banners for:

- offline/reconnecting;
- system degraded;
- connector outage affecting active workflow;
- maintenance mode;
- update available;
- trial/license state if such a product mode exists later;
- security action required.

Banners must be targeted and dismissible only when appropriate.

## 13. User menu

Include:

- profile;
- personal notification preferences;
- appearance/preferences;
- devices/sessions shortcut;
- keyboard shortcuts;
- help/documentation;
- sign out.

Administrative settings should not be mixed into the personal menu except as a clear `Workspace settings` shortcut for authorized users.

## 14. Mobile Admin shell

The mobile shell must support meaningful staff work, but should not imitate desktop density.

Requirements:

- mobile navigation drawer or compact destination switcher;
- persistent search access;
- notification access;
- quick create access;
- no hover dependencies;
- action menus reachable by touch;
- table/list transformations;
- record headers condensed but informative;
- sheets used for filters and secondary controls;
- safe-area support in PWA mode.

## 15. Tablet Admin shell

Tablet should support a collapsed sidebar and near-desktop record workspaces. It is a first-class operational target, especially for client meetings and field/technical work.

## 16. Keyboard behavior

The shell should eventually document and support shortcuts for:

- command palette;
- quick create;
- notifications;
- next/previous list item where safe;
- close drawer/modal;
- save form when appropriate;
- go-to navigation shortcuts if they do not conflict with browser conventions.

A keyboard shortcut reference should be available in-product.

## 17. Permissions

The shell itself must not be the security boundary. Route/menu visibility mirrors server-side permissions.

Navigation rules:

- hide destinations user cannot access;
- distinguish `cannot access` from `not configured`;
- direct deep-link access must still enforce permission;
- plugin routes inherit the same permission contract.

## 18. Notifications integration

The shell must expose:

- unread count;
- urgent/critical distinction without excessive badge noise;
- notification drawer/preview;
- link to full notification center;
- mark read/unread;
- notification preferences shortcut.

## 19. AI integration

Re:Solve AI may have a global entry point, but must not dominate the shell.

Possible entry patterns:

- command palette action;
- dedicated assistant button;
- contextual AI actions inside records.

AI access is permission and feature-policy controlled.

## 20. PWA states

The shell must expose:

- offline indicator;
- queued action count when offline-safe actions exist;
- reconnecting;
- sync restored;
- app update ready;
- install prompt only when appropriate;
- push permission education without nagging.

## 21. Plugin extension points

Approved shell extension points:

- navigation section entry;
- command palette action;
- quick create item;
- page-level status indicator if globally relevant.

Plugins must not arbitrarily inject controls into the top bar.

## 22. Loading and failure

The shell should render independently of most page data so navigation remains usable during feature failures.

If a page/module fails:

- shell remains stable;
- page shows bounded failure;
- retry is available;
- global degradation appears only if impact is broader than one page.

## 23. Acceptance criteria

The Admin shell is acceptable when:

- staff can reach any permitted major area without navigation overload;
- global search/command works from every admin screen;
- quick create is context/permission aware;
- notifications are reachable from every admin screen;
- mobile and tablet navigation are usable without desktop assumptions;
- deep links enforce permissions;
- offline/degraded states are visible;
- plugin navigation can be added through a controlled extension point;
- the shell feels operational rather than template-driven.

## 24. Initial Lovable build slices

### Slice A — visual shell only
- navigation frame;
- topbar;
- responsive collapse;
- placeholder routes;
- no real feature data.

### Slice B — command/search shell
- open/close interaction;
- navigation commands;
- realistic demo records;
- no write actions yet.

### Slice C — notifications entry
- unread indicator;
- drawer preview;
- link to full notification page.

### Slice D — mobile/PWA shell pass
- phone/tablet layouts;
- safe areas;
- offline/update banners;
- touch interaction review.
