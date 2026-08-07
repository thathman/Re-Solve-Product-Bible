# Admin OS Shell

## Purpose
The Admin OS shell is the staff-facing operational frame for Re:Solve. It must make a large operating system feel simple.

The shell is a first-class product feature. Sidebar, top bar, avatar/account, notifications, search/command, Quick Create and Àríyá must be production-quality Core UI components before broad business modules are built.

## Navigation philosophy
Navigation is organized by obvious business intent, not implementation modules.

The preferred mental model is a clear persistent service-CRM navigation similar in legibility to Perfex/Brevo: users can see the major business areas and predict where work belongs.

Do not use:
- Odoo-style app-launcher/module-grid navigation;
- Twenty-style object/app switching as the ordinary navigation model;
- deeply nested expanding trees;
- icon-only root navigation;
- every possible sub-route permanently visible.

## Recommended desktop primary navigation

```text
Home
  Dashboard
  My Work

Clients
CRM
Properties
Projects
Sales
Billing
Support

Operations
  Monitoring
  Renewals
  Requests
  Knowledge
  Files
  Vault
  Automations
  Reports

Platform
  Connectors
  Plugins
  Audit
  Settings
```

This is a clarity contract, not a requirement that every label be hard-coded forever. New features should usually become views/tabs inside these areas instead of new root destinations.

Examples:
- Billing contains Invoices, Payments, Receipts, Credit Notes, recurring billing and account statements.
- Properties contains All Properties, Health/Posture, Renewals and Maintenance, with property type filters/views.
- Sales contains Opportunities, Pipeline, Services, Proposals, Estimates/Quotes, Contracts and Document Studio entry points.

## Desktop anatomy
- strong left sidebar;
- strong top utility bar;
- compact page/record header inside content;
- primary work canvas;
- optional contextual drawer/panel for bounded secondary work.

## Sidebar contract
AdminSidebar must support:
- Re:Solve/product identity;
- clear section grouping;
- obvious active route and active area;
- text labels by default;
- compact/collapsed power-user mode;
- tooltips and retained discoverability when collapsed;
- meaningful counts only when actionable;
- permission-aware visibility;
- plugin entries only in approved slots;
- long-label handling;
- keyboard navigation;
- stable scroll behavior;
- responsive conversion to mobile navigation.

Collapsed mode is an enhancement for experienced users, not a substitute for understandable labels.

## Top bar contract
TopBar should provide, where applicable:
- compact current context/breadcrumb;
- global search/CommandPalette trigger;
- Quick Create;
- Àríyá trigger;
- NotificationTrigger;
- degraded/offline/update indicator only when relevant;
- ResolveAvatar/AccountMenu;
- Operating Entity/context switch only when the deployment actually needs one.

Avoid feature-specific shortcut clutter.

## Global search / Command Palette
Accessible globally through visible UI and keyboard shortcut.

Capabilities:
- navigate to major area;
- search records;
- open recent/favorite record;
- Quick Create;
- run permitted Action Registry commands;
- open Àríyá;
- plugin-provided approved commands.

Results identify record type, parent Organisation/Property context, status and secondary reference where useful.

## Quick Create
Quick Create is permission/context aware and contains only useful common creates rather than every record type.

Potential actions:
- Organisation/Client
- Contact
- Lead/Opportunity
- Property
- Project/Task
- Request
- Proposal/Estimate
- Invoice
- reminder/note
- Vault Item where authorized

Recent/frequent actions may rank higher.

## Notification chrome
NotificationTrigger must communicate unread/urgent state without badge noise.

NotificationTray supports:
- compact All/Unread/action distinction;
- grouped items;
- priority cues;
- context;
- primary deep-link/action;
- mark read/unread;
- snooze/archive when relevant;
- link to full Notification Center;
- preferences shortcut.

## Avatar and AccountMenu
ResolveAvatar should be visually strong and clearly interactive.

AccountMenu includes:
- avatar/name;
- current role/context summary;
- profile;
- preferences;
- notification preferences;
- security/devices/sessions;
- appearance;
- keyboard shortcuts/help;
- Portal/Admin switch where authorized;
- workspace/settings shortcut where authorized;
- sign out.

Do not ship a minimal avatar dropdown with only profile/logout.

## Àríyá integration
Àríyá has a stable global TopBar/Command entry and contextual entry in records.

It must not dominate the shell or use a generic floating bubble. AriyaPanel follows `04-ai/ariya-experience.md` and the Core UI Framework.

## Page header contract
Major pages provide:
- page/record title;
- optional eyebrow/breadcrumb;
- optional status/reference;
- concise key metadata;
- primary action;
- secondary/overflow actions;
- view/filter controls when relevant.

Keep headers operationally compact.

## Area subnavigation
After entering a major area, use tabs/views rather than root-nav expansion.

Example Billing:
`Overview | Invoices | Payments | Receipts | Credit Notes | Recurring`

Example Properties:
`Overview | All Properties | Health | Renewals | Maintenance`

## Context drawers
Use right-side drawers for bounded secondary work such as quick preview, small edit, task detail, notification detail, connector event and audit detail. Deep record work opens the full workspace.

## Persistent application state
The shell may show targeted persistent state for:
- offline/reconnecting;
- system degradation;
- connector problem materially affecting the current flow;
- maintenance mode;
- update ready;
- security action required.

Shell remains usable when an individual feature fails.

## Mobile Admin
Do not shrink the desktop sidebar.

Requirements:
- deliberate mobile destination menu/sheet;
- compact top bar;
- persistent search, notifications and Account access;
- Àríyá reachable without obstructing content;
- Quick Create reachable;
- condensed informative record headers;
- filters/secondary controls in sheets;
- no hover dependency;
- safe-area support in installed PWA.

## Tablet
Tablet is a first-class operational target and should support a compact/collapsed nav with near-desktop record workflows where space permits.

## Keyboard
Document/support shortcuts for command/search, Quick Create, notifications, overlay close and selected safe navigation/actions. Keyboard shortcuts must not conflict unnecessarily with browser conventions.

## Permissions
Shell visibility mirrors authorization but is never the security boundary. Deep links and Action Registry executions perform server-side authorization.

## Plugins
Approved shell extension points:
- designated navigation area entry;
- command action;
- Quick Create item;
- globally relevant status indicator only under strict policy.

Plugins cannot inject arbitrary TopBar controls or create their own root navigation system.

## Component Gallery
All foundational shell components appear in the development Component Gallery with normal/focus/active/collapsed/mobile/long-label/unread/degraded variants.

## Acceptance criteria
- a new staff user can predict where major work lives;
- root navigation stays compact as the OS expands;
- Sidebar, TopBar, avatar/account, notifications, search and Àríyá are visually strong;
- staff can reach permitted major areas without an app launcher;
- mobile/tablet are deliberately designed;
- shell survives page-level failures;
- plugin growth cannot destroy navigation simplicity;
- deep links remain permission enforced.

## Initial Lovable build slices
### Slice A — production-quality shell foundation
Sidebar, TopBar, avatar/account, search/command entry, Quick Create, Notification entry, Àríyá entry, responsive behavior and placeholder routes. No business module implementation.

### Slice B — command/search behavior
Navigation commands and realistic read-only demo records.

### Slice C — notification tray behavior
Unread/group/deep-link/personal preference entry using demo notifications.

### Slice D — mobile/PWA polish
Phone/tablet navigation, safe areas, offline/update state and touch review.
