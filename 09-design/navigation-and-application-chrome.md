# Navigation and Application Chrome

## Purpose
Re:Solve navigation must feel obvious on first contact. Users should understand where Clients, Properties, Projects, Sales, Billing, Support and Operations live without learning an internal product taxonomy.

The desired simplicity is closer to clear service-CRM navigation such as Perfex/Brevo than Odoo-style app launchers or object-centric/module-switcher navigation.

## Non-negotiable navigation principles
- one clear primary left navigation on desktop Admin;
- familiar human-readable section names;
- shallow hierarchy;
- no app launcher as the main mental model;
- no icon-only root navigation;
- no permanent exposure of every subpage;
- strong active section treatment;
- context and secondary navigation appear only after entering a major area;
- Settings and platform administration are visually separated from daily operational work;
- plugin entries use controlled slots and cannot overwhelm the root navigation.

## Admin primary navigation
Recommended default structure:

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

The exact grouping may be refined through prototypes, but the root must remain understandable and compact.

Do not show every child such as invoices/payments/receipts or websites/domains/hosting in the root sidebar. Enter the parent area and use tabs/subnavigation/views there.

## Sidebar
The AdminSidebar should support:
- clear wordmark/product identity area;
- strong active route and active section state;
- optional section labels/dividers;
- compact/collapsed mode without losing discoverability;
- meaningful badge/count only for actionable states;
- tooltips in collapsed mode;
- keyboard access;
- long-label handling;
- scroll behavior that keeps important utility destinations reachable;
- permission-aware entries;
- setup/degraded indicator only when genuinely useful;
- responsive transition to mobile navigation.

Collapsed mode is a power-user enhancement, not the default teaching mode for new users.

## Top bar
The TopBar is a strong global utility surface, not decorative whitespace.

It should provide, as applicable:
- current context/breadcrumb or compact page context;
- global search / command palette trigger;
- Quick Create;
- Àríyá trigger;
- Notification trigger;
- connection/system status only when attention is required;
- avatar/account menu;
- operating entity/context switch only when the deployment actually needs it.

Do not fill the top bar with random feature shortcuts.

## Global search / command
The search entry must be easy to discover even for users who do not know keyboard shortcuts.

It can combine:
- navigation
- record search
- recent records
- favorites
- registered actions
- Quick Create
- Àríyá entry

Results must clearly identify record type and parent context.

## Notification chrome
The global NotificationTrigger must communicate unread state without becoming visually noisy.

The tray should support:
- All/Unread or lightweight filters;
- priority cues;
- meaningful grouping;
- action-required distinction;
- context labels;
- primary action/deep link;
- mark read/unread;
- snooze/archive where applicable;
- link to full Notification Center.

## Avatar/account chrome
The avatar control should be unmistakably interactive and show identity confidently.

Account menu includes:
- name/avatar;
- role/context summary;
- profile;
- personal preferences;
- notification preferences;
- security/devices/sessions;
- appearance;
- keyboard shortcuts/help;
- Portal/Admin switch when authorized;
- workspace/settings shortcut when authorized;
- sign out.

## Àríyá chrome
Àríyá should have a stable global location in the top bar/command system and contextual entry points in records. Avoid a generic floating assistant bubble covering content.

## Area-level navigation
Inside a major area, use simple tabs/views.

Example Billing:
```text
Overview | Invoices | Payments | Receipts | Credit Notes | Recurring
```

Example Properties:
```text
Overview | All Properties | Health | Renewals | Maintenance
```

Type filters such as Website, Domain, Journal, Hosting should normally be views/filters, not permanent root routes.

## Record-level navigation
A first-class record uses a compact RecordHeader plus tabs/sections. Do not create a second permanent sidebar inside every record.

## Client Portal
Portal navigation is even simpler.

Recommended:
```text
Home
Properties
Projects
Support
Billing
Approvals
Files
Knowledge
Organisation
```

Vault appears only when the client has authorized secure items/access.
Requests may appear as a clear `Requests` destination or contextual action if the client's service model needs it.

Notifications and Account remain global chrome rather than bloating the main nav.

## Mobile
Do not shrink the desktop sidebar.

Phone behavior should use a deliberate mobile navigation model:
- compact top bar;
- high-frequency destinations immediately reachable;
- more destinations in an explicit menu/sheet;
- search, notifications and account always reachable;
- Àríyá reachable without obstructing primary tasks;
- current context clear after deep links.

Portal may use a small bottom navigation for the highest-frequency destinations if prototype testing confirms it improves clarity.

## Navigation governance
New domains/plugins must answer:
1. Can this be a view/tab inside an existing major area?
2. Is it important/frequent enough to justify root navigation?
3. Does the label make sense to a non-technical operator?
4. What happens on mobile?

Default answer for new extension features should not be `add another sidebar item`.

## Acceptance criteria
- a new staff user can predict where major work lives;
- root Admin navigation remains compact as the OS grows;
- no Odoo-like launcher/app-grid mental model is required;
- no Twenty-like object/module switching is required for ordinary navigation;
- sidebar, top bar, notifications, avatar/account and Àríyá are visually strong Core Framework components;
- mobile navigation is a designed model rather than hidden desktop navigation;
- plugin growth cannot destroy navigation simplicity.
