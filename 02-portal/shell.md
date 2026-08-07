# Client Portal Shell

## Purpose
The Client Portal shell is the client-facing Re:Solve operating surface. It must feel simpler and calmer than Admin while retaining the same Core UI quality.

The Portal is not a reduced Admin OS. It is a client-goal-oriented experience over the same authorized business truth.

## Navigation philosophy — non-negotiable
Portal navigation must be obvious without product training.

Default destinations:
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

Conditional:
- Requests, when enabled as a meaningful client workflow;
- Vault, only when the client User has authorized secure items/access.

Notifications and Account are **global chrome**, not root-navigation clutter.

Avoid:
- Odoo-style app/module launchers;
- Twenty-style object/app switching;
- nested module trees;
- every record subtype in root navigation;
- exposing hidden features just to show permission errors;
- icon-only root navigation as the primary teaching model.

## Primary users
- Organisation Owner/Admin;
- Billing Contact;
- Approver;
- Project Collaborator;
- Property Manager/Technical Contact;
- Vault User;
- read-only member.

A User may combine responsibilities and have Property-specific grants.

## Shell responsibilities
- simple client navigation;
- Organisation context;
- global client-safe Search/Command where enabled;
- NotificationTrigger/Tray;
- Account/ResolveAvatar;
- persistent Support entry;
- optional Àríyá entry;
- responsive/PWA navigation;
- offline/update/connection state;
- permission-aware route exposure.

## Core UI quality mandate
Portal shell uses the same mandatory Re:Solve Core UI Framework and sourcing hierarchy:
- shadcn/ui;
- Untitled UI React;
- Tremor where data presentation is relevant;
- React Aria/Base UI/Radix behavior;
- Re:Solve-owned final tokens/components.

Header/navigation/avatar/notifications/support/Àríyá must be production-quality foundation components, not starter-template leftovers.

## Desktop / laptop
Recommended:
- compact simple left navigation or validated top/side hybrid using canonical PortalNavigation;
- Operating Entity/Brand/Re:Solve identity without excessive branding chrome;
- strong TopBar/utility area;
- comfortable content width;
- contextual tabs/views inside destination pages rather than additional permanent sidebars.

If Portal uses a left nav, it should be lighter/less dense than Admin and avoid exposing technical Operations/Platform structure.

## Top bar
Portal TopBar should provide as applicable:
- current Organisation context;
- client-safe Search/Command;
- Support shortcut;
- optional Àríyá trigger;
- NotificationTrigger;
- ResolveAvatar/AccountMenu;
- connection/offline state only when relevant.

Do not fill it with random feature shortcuts.

## ResolveAvatar / AccountMenu
The avatar/account experience is a first-class Core UI component.

AccountMenu includes:
- identity/avatar/name;
- current Organisation/role context;
- Profile;
- Notification Preferences;
- Communication Preferences;
- Security/MFA;
- Sessions/Devices;
- Appearance/Accessibility;
- Help/keyboard info where useful;
- Admin switch only for Users who are genuinely authorized for Admin;
- sign out.

Organisation administration remains under Organisation, not personal Account.

## Notifications chrome
NotificationTrigger/Tray must be strong and immediately understandable.

Tray supports:
- unread/action-required cues;
- grouped client-safe items;
- context;
- one obvious action/deep link;
- read/archive/snooze where relevant;
- full Notification Center link;
- preference shortcut.

Do not use unread count as the Portal Home Attention model.

## Support entry
Chatwoot owns Support conversations.

Support must be easy to reach from:
- root `Support` destination;
- TopBar shortcut where useful;
- contextual `Get support for this Property/Project` Actions;
- Incident/Property state CTA.

Context handoff includes safe Organisation/Property/reference only. No secrets/private internal notes.

Avoid a second Re:Solve support-messaging console.

## Search / Command
Portal Search only searches client-authorized records/content.

Potential results:
- Properties;
- Projects;
- Requests;
- Approvals;
- Invoices/Receipts/Statements where permitted;
- Files;
- Knowledge;
- safe Vault metadata when explicitly authorized.

Internal Notes, hidden Properties, other Organisations, internal finance/Audit/provider details never appear.

Portal command actions are curated/simple, e.g.:
- New Request;
- Upload requested File;
- open outstanding Approval;
- pay Invoice;
- start Support;
- ask Àríyá where enabled.

## Àríyá
Optional Portal Àríyá uses a stable TopBar/Command/contextual pattern and `04-ai/ariya-experience.md`.

Avoid a generic floating bubble that covers content. Portal Àríyá is narrower/client-safe and must never expose internal evidence or Vault secrets.

## Organisation context
If a User belongs to multiple Organisations, switching is explicit and prominent enough to prevent mistaken action. Current context persists through navigation/deep links safely.

## Property / Project context
Context belongs inside record pages/RecordHeader/tabs, not as permanent shell switchers unless a prototype proves a clear need.

## Mobile — primary scenario
Do not shrink the desktop nav.

Use deliberate mobile navigation:
- compact TopBar;
- persistent Home/high-frequency destinations via bottom nav if validated;
- explicit `More`/sheet for remaining destinations;
- Search, Notifications, Account and Support always easy to reach;
- Àríyá reachable without obstructing primary work;
- safe-area handling;
- installed PWA quality;
- no horizontal root navigation.

Candidate bottom-nav destinations can be Home, Projects/Properties, Support and role-relevant Action/More. Final composition should be prototyped rather than hard-coded from assumption.

## Client-safe language
Prefer:
- `Action required`;
- `Waiting for you`;
- `Payment received`;
- `Website needs attention`;
- `Renewal due`;
- `Status temporarily unavailable`.

Avoid raw workflow/event/monitor/provider jargon unless user opens technical detail and has permission.

## Permission states
Distinguish:
- feature not offered to Organisation;
- feature exists but User lacks access;
- no data yet;
- no Property grant;
- client-admin approval/access request available;
- permission revoked while page open.

Do not advertise hidden Vault/finance/internal capability without a useful access-request reason.

## Common client actions
May include:
- approve/reject/request changes;
- pay Invoice/deposit;
- view/download Receipt/Statement;
- upload requested File;
- create/respond to Request;
- update permitted Organisation profile;
- invite/manage teammate;
- request Vault access;
- reveal/download explicitly granted Vault Item;
- open Support;
- acknowledge/view Incident/Maintenance;
- make Renewal decision;
- complete Client Action.

Actions use Action Registry and deep-link from Attention/Notifications.

## PWA/offline
Required shell states:
- install opportunity;
- offline;
- reconnecting;
- safe cached summaries;
- update available;
- sync failed/restored;
- push permission onboarding.

High-risk/payment/Approval/Vault actions normally require live connectivity. Vault contents never broadly offline cache.

## Empty states
Examples:
- no Projects -> clear account is quiet/show history if permitted;
- no Invoices -> `No outstanding billing`;
- no Approvals -> `Nothing waiting for your approval`;
- no Properties -> explain access may not yet be assigned;
- no Vault access -> do not advertise hidden secrets;
- onboarding -> show exact next actions.

## Degraded states
Handle Support unavailable, payment provider unavailable, stale Property Posture, File preview failure, offline and permission revocation without falsely showing empty/healthy state.

## Branding
Operating Entity/Brand may control approved logo/accent/title/auth/email/document identity within Core UI accessibility constraints. Do not allow arbitrary client-specific layout themes that fragment the product.

## Plugins
Plugin Portal contributions use approved navigation/tab/widget/action slots and Core UI components.

Default answer is not `add a new root nav item`. Plugin visibility respects Organisation entitlement/User scope and mobile rules.

## Accessibility
WCAG 2.2 AA with special care for mobile navigation, invoices/payment, Approvals, File upload, Support launch, Vault step-up and install/push prompts.

## Component Gallery
PortalNavigation, Portal TopBar, ResolveAvatar/AccountMenu, NotificationTrigger/Tray, Support state, mobile nav, offline/update and optional AriyaTrigger variants should appear in the development Component Gallery.

## Acceptance criteria
- first-time client User can predict where work lives;
- root navigation remains simple as capabilities grow;
- no Odoo/Twenty-style navigation mental model;
- TopBar/avatar/notifications/support are strong Core UI;
- mobile feels intentionally designed;
- support is easy without duplicating Chatwoot;
- hidden data cannot leak through Search/navigation/errors/cache;
- conditional Vault/Requests do not clutter users who do not need them;
- plugin growth cannot destroy Portal simplicity;
- no HR/Timesheet/Client Service Consumption concept appears.

## Initial Lovable build slices
### Slice A — strong Portal shell
Navigation, TopBar, ResolveAvatar/AccountMenu, Notification entry demo, Support entry, placeholder destinations and fictional client identity.

### Slice B — mobile/PWA shell
Mobile nav, safe areas, install/offline/update, touch review.

### Slice C — Search/Notification polish
Client-safe Search/Command entry, tray/deep links into placeholder pages.

### Slice D — Support context handoff
Chatwoot launch pattern and degraded state.

Àríyá functional capability remains a later slice; only canonical shell presence may be established in FOUND-001.
