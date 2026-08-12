# Admin and Client Portal Experience Reset

## Status
**Canonical design-direction reset.** Existing Admin/Portal functional shells and earlier visual specifications are not final experience authority. They preserve useful functional/security boundaries, but the product must receive a deliberate information-architecture and visual-composition redesign before product completion.

## Why this reset exists
Re:Solve has grown from a smaller CRM/operations concept into a broad agency OS. Preserving every existing card, route and navigation choice would produce a capable but cluttered product.

The redesign must keep breadth while reducing visible complexity.

## Shared principles
- clean and calm rather than dense-by-default;
- obvious business language;
- shallow navigation;
- one strong visual hierarchy per screen;
- fewer decorative cards/borders/shadows;
- whitespace and typography carry hierarchy;
- responsive behavior designed, not merely stacked;
- saved views and contextual actions instead of permanent navigation proliferation;
- module visibility/toggles can reduce irrelevant product breadth without changing security;
- Ariya is baked into relevant contexts rather than a competing app/module;
- state/Attention/actionability are clearer than dashboard decoration;
- Core UI remains source-owned and consistent.

## Admin experience
Admin should answer:
- what needs attention;
- what am I responsible for;
- what client/record am I operating;
- what can I do next;
- what changed;
- what does Ariya know/recommend and why.

### Recommended shell direction
Primary navigation should remain compact around:
`Home | Tasks | Clients | CRM | Sales | Delivery | Support | Billing | Forms | Calendar | Information | Reports | Automations | Settings`.

Properties/Monitoring, Renewals, Files, Knowledge, Vault, Connectors, Plugins, Audit and System Operations remain first-class capabilities but do not all need permanent root rows.

Global Search/Command, Quick Create, Notifications, Account and Ariya stay consistently reachable.

### Canonical record workspace
Where practical, record pages share a composition:
1. identity/header;
2. concise state/health/relationship context;
3. primary actions;
4. contextual tabs/sections;
5. related Attention/Activity/Audit where useful;
6. contextual Ariya.

Examples:
- Organisation: Overview, Contacts, Opportunities, Proposals, Contracts, Projects, Properties, Billing, Support, Forms, Files, Communications, Notes, Activity/Audit.
- Opportunity: Overview, Discovery/Forms, Proposal, Activities, Communications, Files, Notes.
- Project: Overview, Milestones, Tasks, Approvals, Properties, Forms, Files, Financials, Support, Communications, Notes.

Do not render every possible tab if disabled/empty/unauthorised; use sensible progressive disclosure.

## Tasks experience
The former `My Work` area is redesigned/canonicalised as **Tasks**. Focus/Today/Overdue/Waiting/Saved Views provide personal execution without a second work product.

## Admin dashboards
Dashboards may support governed configurable widgets/layouts and role/default views, but must not become a wall of small metric cards. Default Home prioritizes Needs Attention, Tasks, client/project/property/commercial health and Ariya briefing.

## Client Portal experience
Portal is a client product, not a reduced Admin clone.

It should answer:
1. What needs my attention?
2. What are you working on?
3. What do I owe?
4. What do you need from me?
5. Where are my files?
6. How do I get help?

### Recommended primary navigation
`Home | Projects | Billing | Support | Files | More`

`More` can expose permitted Properties, Approvals, Forms/Requests, Knowledge, Organisation/Account and Vault. Exact navigation adapts to enabled capabilities and client permissions.

### Portal Home
The visual priority is **Needs Your Attention**:
- document/signature required;
- Form/questionnaire due;
- File Request;
- Project approval/client action;
- deposit/Invoice/payment milestone;
- renewal decision;
- important Incident/maintenance;
- recent meaningful update.

Below that: concise active Project, Billing, Property Health/incident and recent-file/support context. Avoid copying Admin KPI density.

### Onboarding pack / client journey
A client-facing onboarding/journey view may group the real underlying actions after Proposal acceptance:
- Contract to sign;
- deposit to pay;
- questionnaire to complete;
- Files to upload;
- kickoff appointment to book.

The journey is orchestration; underlying records remain Contract/Invoice/Form/File Request/Booking.

### Portal Ariya/live chat
Ariya is integrated naturally into client help/context. Human support handoff uses Chatwoot. The UI should present one coherent client conversation rather than exposing backend product boundaries.

### Preview as Client
Admin needs a safe read-only preview of a chosen client context before releases/visibility changes.

## Mobile
### Admin
Prioritize Tasks, triage, record summary, primary actions, approvals, Billing review and urgent Property/Support states. Dense authoring may use larger-screen optimization without becoming impossible on phone.

### Portal
Should feel app-like, touch-friendly and extremely simple. Bottom/tab navigation is acceptable where it improves mobile clarity, but final pattern must be validated against the redesigned IA rather than inherited blindly.

## Lists / views
Use table, list, board/Kanban, calendar or grid only where the underlying work benefits. Universal Saved Views preserve filters/sorts/columns/grouping and may be private/team/workspace/system.

## Module visibility
Deployments/roles may disable or hide unused modules/capabilities to keep the OS clean. Visibility does not grant/revoke authority and cannot bypass dependencies/security.

## Quick Create
A governed global create menu can offer relevant actions such as Organisation, Lead, Opportunity, Proposal, Project, Task, Support case, Invoice, Payment, Expense, Form Request and File Request based on capability/module state.

## Design QA gate
Before Admin/Portal UI is declared product-complete, run deliberate browser acceptance on desktop/tablet/phone including:
- real task completion paths;
- navigation depth;
- information density;
- empty/loading/error/permission states;
- keyboard/focus/accessibility;
- responsive composition;
- dark/light/client themes;
- Ariya placement/context;
- client-safe visibility;
- Preview as Client.

## Non-goals
This reset does not change server authorization/RLS, business-record authority, Audit/Attention semantics or product exclusions merely for visual convenience.

## Acceptance criteria
- Admin and Portal no longer inherit earlier shell visuals as final authority;
- Admin remains powerful without exposing every capability as a root menu item;
- Portal is significantly simpler than Admin;
- record workspaces use consistent hierarchy;
- Tasks replaces My Work;
- Ariya is contextual/baked-in and never obstructive;
- module visibility/Saved Views reduce clutter;
- client actions dominate Portal Home;
- mobile is intentionally designed;
- final browser design acceptance occurs before product completion.
