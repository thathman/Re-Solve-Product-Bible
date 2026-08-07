# Client Portal Shell

## 1. Purpose

The Client Portal shell is the client-facing operating surface of Re:Solve. It must help client users understand the state of their relationship, properties, projects, approvals, billing, support, files, vault access, and organisation membership without exposing internal staff complexity.

The portal is not a reduced Admin OS. It is a distinct experience over the same business truth.

## 2. Primary users

- client organisation owner;
- client administrator;
- billing contact;
- project approver;
- project participant;
- technical/property contact;
- vault-authorized contact;
- read-only stakeholder.

A client user may have multiple roles and property-specific grants.

## 3. Core portal responsibilities

The shell owns:

- client navigation;
- organisation context;
- property context when relevant;
- notifications;
- global support entry;
- client-safe search;
- account/user controls;
- responsive/PWA shell;
- offline/update state;
- permission-aware route exposure.

## 4. Navigation philosophy

Portal navigation should be based on client goals.

Primary destinations:

- Home
- Properties
- Projects
- Support
- Billing
- Approvals
- Files
- Vault
- Knowledge
- Organisation

Secondary destinations:

- Notifications
- Account

Not every user sees every destination.

## 5. Desktop shell

Recommended structure:

- compact sidebar or strong top/side hybrid navigation;
- clear organisation identity;
- top utility area for notifications, support, account, and search;
- main content area with comfortable width;
- contextual property/project switching inside feature pages rather than global clutter.

The design should feel premium and trustworthy rather than like back-office software.

## 6. Mobile shell

Mobile portal usage is a primary scenario.

The mobile shell should consider a persistent bottom navigation for the highest-frequency destinations, with remaining destinations in a More/menu surface.

Candidate primary mobile destinations:

- Home
- Properties or Projects depending validated frequency
- Support
- Billing/Approvals depending user role
- More

The final selection should be validated by flow prototypes rather than assumed.

Requirements:

- one-hand reachable primary actions where practical;
- safe-area handling;
- installed PWA mode;
- no horizontal desktop navigation compressed onto a phone;
- notification and support access always easy to find;
- file upload and approval flows fully usable on mobile;
- invoices and receipts readable without pinch/zoom dependency.

## 7. Home responsibility

The portal home is an action-and-status summary, not a miniature version of every module.

It should answer:

- What requires my attention?
- What is happening with my projects/properties?
- Is anything wrong?
- Do I owe anything?
- Has anything important changed?
- How do I contact support?

Detailed dashboard specification will follow separately.

## 8. Global support entry

Chatwoot owns managed client support conversations. The portal shell should provide a persistent support entry without recreating Chatwoot's conversation engine.

Possible entry points:

- Support navigation item;
- floating/help trigger on appropriate screens;
- contextual `Ask support about this` actions on property/project records;
- incident/support CTA when a property is degraded.

Support handoff should carry permitted context such as organisation/property/reference without leaking confidential data.

## 9. Search

Portal search should only search records visible to the client user.

Potential searchable objects:

- properties;
- projects;
- files;
- invoices;
- receipts;
- knowledge;
- approvals;
- vault metadata the user may see.

Internal notes, hidden files, other clients, internal financial data, and internal audit data must never appear.

## 10. Organisation context

The portal must make it obvious which organisation the user is acting for, especially if multi-organisation membership is supported later.

Organisation administration may include:

- profile;
- team;
- invitations;
- role assignments;
- property access;
- billing contacts;
- approvers;
- vault access administrators.

## 11. Property context

Property-aware surfaces should show:

- property name;
- type;
- current state/health where permitted;
- parent relationship;
- related projects;
- support entry;
- recent activity;
- relevant files;
- relevant credentials/vault items;
- renewal/maintenance information where client-visible.

## 12. Notifications

The shell exposes:

- unread count;
- notification preview;
- urgent/important items;
- full notification center;
- preference shortcut.

Client notifications must use plain client language. Internal operational terminology should be translated or omitted.

## 13. Account menu

Include:

- personal profile;
- notification preferences;
- security/MFA;
- active sessions/devices;
- appearance;
- installed app/help information where appropriate;
- sign out.

Organisation settings belong in Organisation, not personal Account.

## 14. Branding

The portal may support controlled workspace/client branding, but Re:Solve must retain a coherent accessible design system.

Permitted branding could include:

- workspace/client logo;
- approved accent color;
- portal title;
- selected auth/login identity;
- email/document identity.

Branding must not permit inaccessible color combinations or arbitrary layout breakage.

## 15. Client-safe terminology

Portal labels should optimize clarity over internal precision.

Examples:

- `Action required` instead of internal queue names;
- `Waiting for you` instead of workflow engine state;
- `Payment received` instead of reconciliation event terminology;
- `Website issue` instead of technical monitor codes unless detail is requested.

## 16. Permission behavior

The portal should distinguish:

- feature unavailable to organisation;
- feature available but current user lacks permission;
- no data yet;
- no property grant;
- action requires organisation admin approval.

Do not expose hidden destinations merely to show a permission error unless there is a useful reason to explain how access can be requested.

## 17. Client actions

Common portal actions may include:

- approve/reject/request changes;
- pay invoice;
- download receipt;
- upload requested file;
- update organisation profile;
- invite teammate;
- request credential access;
- reveal permitted vault item;
- contact support;
- acknowledge maintenance/incident;
- complete project action.

Actions must deep-link from notifications.

## 18. PWA behavior

The portal should be designed as installable from the beginning.

Required states:

- install opportunity;
- offline shell;
- cached recent safe content where appropriate;
- offline-safe draft or queued action only when data integrity is clear;
- reconnecting;
- sync success/failure;
- push permission onboarding;
- app update available.

Sensitive vault values should not be cached for offline access by default.

## 19. Push notifications

Push is particularly valuable for:

- approval required;
- urgent property incident;
- payment confirmation;
- project action due;
- support update when configured;
- credential access request/approval;
- important renewal reminder.

Push behavior must respect notification policy and user preferences except mandatory security events.

## 20. Empty and first-use states

Portal empty states should be reassuring and explanatory.

Examples:

- no active projects → explain there are no current projects, show completed history if permitted;
- no invoices → state account is clear rather than suggesting setup work;
- no approvals → `Nothing waiting for your approval`;
- no properties → explain access may not yet be assigned;
- no vault access → avoid advertising hidden confidential content.

## 21. Error and degraded states

The portal must gracefully handle:

- connector unavailable;
- payment provider unavailable;
- support system unavailable;
- file preview unavailable;
- stale property health;
- offline state;
- permission revoked while screen is open.

Client copy must distinguish system issue from client action where possible.

## 22. Accessibility

Portal flows must target WCAG 2.2 AA and be fully usable with keyboard, screen readers, text zoom, and touch.

Particular care:

- invoice/payment forms;
- approval dialogs;
- file uploads;
- support launch;
- vault reveal;
- mobile navigation;
- push/install prompts.

## 23. Plugin extension points

Plugins may add portal functionality only through approved slots:

- navigation destination;
- property tab;
- project tab;
- dashboard/home widget;
- organisation capability;
- contextual action.

Plugin visibility must respect organisation entitlement and user permissions.

## 24. Acceptance criteria

The portal shell is acceptable when:

- client users understand where they are and what requires action;
- permissions produce safe, understandable navigation;
- mobile feels intentionally designed;
- PWA installed mode is usable;
- support is always easy to access without duplicating Chatwoot;
- notifications deep-link to actionable portal states;
- organisation/property context is clear;
- sensitive/internal data cannot leak through search, navigation, errors, or cached states;
- plugin destinations can be added without breaking navigation hierarchy.

## 25. Initial Lovable build slices

### Slice A — portal shell
- navigation;
- header/account;
- responsive layouts;
- placeholder destinations;
- realistic client identity.

### Slice B — mobile/PWA shell
- mobile navigation;
- safe-area behavior;
- install/offline/update states;
- touch review.

### Slice C — notification entry
- unread badge;
- preview;
- deep-link behavior into placeholder pages.

### Slice D — support entry
- persistent Chatwoot launch pattern;
- context-safe handoff demonstration;
- unavailable/degraded state.
