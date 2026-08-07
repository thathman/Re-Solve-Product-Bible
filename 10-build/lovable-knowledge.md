# Re:Solve Lovable Knowledge

## Purpose
This document defines persistent product/engineering rules loaded into Lovable Knowledge so every build slice inherits the same decisions without receiving the entire Product Bible.

## Product identity
Re:Solve is a modular operating system for running client relationships, digital Properties, projects, commercial documents, billing, support context, monitoring, renewals, knowledge, confidential information, requests, automation and operations from one coherent application.

Re:Solve is not a generic CRM template and must not devolve into disconnected CRUD pages or interchangeable KPI dashboards.

## Build philosophy
- Build only the current bounded slice.
- Prefer complete flows over broad shallow coverage.
- Include relevant loading, empty, error, permission, stale, responsive, PWA and accessibility states.
- Preserve Product Bible terminology/ownership boundaries.
- Stop and report contradictions rather than silently inventing a new rule.

## Lovable-first implementation
- Favor Lovable's current preferred application patterns over the legacy NestJS/GraphQL/TypeORM architecture.
- Supabase is acceptable for development database/auth/storage/realtime workflows.
- Exported application must remain understandable, portable and self-hostable without Lovable runtime dependency.
- Centralize provider/data access through service/repository/connector boundaries rather than scattering SDK calls through UI.

## Application structure
One application, two role-shaped shells:
- Admin OS
- Client Portal

They share identity, permissions, data, Core UI tokens, notifications, audit, plugin/connector infrastructure and platform primitives but have different density/navigation composition.

## Workspace / Operating Entity / Organisation
- Every deployment has one Workspace.
- Operating Entity represents the business doing the work; Airix Media is the initial Operating Entity.
- Organisation represents clients/prospects/vendors/partners.
- Do not model the operating business as an ordinary client merely to reuse the Organisation UI.

## Identity and permissions
`Principal` is the generic authorization actor. Human User, Service Account, API Client, MCP Client, Plugin and Connector are principal types.

`User` means a human authenticated identity.

Roles are bundles. Authorization is capability + scope and is enforced server-side.

Canonical permission grammar: `domain.action` or `domain.resource.action`.

Negative authorization paths are product requirements, including cross-organisation/property denial and expired/revoked access.

## Explicit product exclusions
Do **not** introduce:
- HR management
- payroll
- leave/attendance
- recruitment
- employee performance reviews
- timesheets or time-tracking
- Client Service Consumption / hours-or-credits used-versus-remaining metering

Projects can have assignments, estimates, milestones, deadlines and expenses without timesheets.

## Chatwoot boundary
Chatwoot owns managed support conversations/messages, web chat, inboxes/channels, agents/teams/routing, support attachments, support Knowledge and Captain.

Re:Solve owns Organisation/Property/Service context, support entitlement, SLA/commercial context, incidents, safe conversation references/summaries, analytics and deep links.

Do not rebuild Chatwoot's helpdesk/agent console or mirror every message.

## WhatsApp / Baileys
Primarily Re:Solve-to-client operational communication: project/request updates, reminders, approvals, billing notices, renewals, property alerts and direct operational messages. Not the client's end-customer support inbox.

## Àríyá
The user-facing name of Re:Solve's built-in AI is **Àríyá**. Internal technical types may remain AIProvider/AIRun/AITool/etc.

Àríyá is separate from Chatwoot Captain, inherits caller permissions, uses controlled tools and the Action Registry, shows evidence/freshness and never gets arbitrary SQL or generic Vault secret access.

Avoid generic floating sparkle-button AI UX. Àríyá should be a native TopBar/Command/contextual product surface.

## Attention and Notifications
Notification = durable awareness/delivery that something happened.
Attention Item = a condition that still requires action/awareness now.

Dashboard, My Work, Portal Home and Àríyá briefings consume Attention rather than recreating unrelated risk queries.

Notifications remain a core multi-channel primitive with recipient, priority, grouping, deep link, delivery and policy.

## Action Registry
Meaningful mutations/actions should have a controlled Action definition where reusable across UI, command palette, Àríyá, API, MCP, automations and plugins.

Authorization is checked at execution time. High-impact actions may require confirmation, approval and/or step-up.

## Plugins and connectors
Plugin = business/product capability extension.
Connector = external-system integration.

Optional provider packages may be Plugins that register Connector implementations. Business domains depend on provider-neutral connector capabilities.

## Payments
Billing is provider-neutral. Verified provider events/records establish payment truth; browser return pages do not.

## Monitoring and Property Posture
Re:Solve includes a native Monitoring Engine. Uptime Kuma and external monitoring products are optional connectors, not required dependencies.

Native monitoring grows from HTTP/HTTPS, latency and SSL/domain expiry toward DNS/TCP/heartbeat/backups and independently deployable probe workers.

Property Posture combines explainable evidence from monitoring, renewals, connectors, incidents and relevant application state.

Cloudflare is an optional first-class connector for domain/DNS/edge/health context.

## Renewals
Domain, hosting, certificate, service, contract and other expiry obligations use first-class Renewal/Expiry records and a Renewal Desk rather than isolated date badges.

## Secure Vault / Files
Files = ordinary managed file domain.
Vault = protected confidential domain.

A confidential protected document is a Vault Item and must not retain a second ordinary File access path. Both may share storage infrastructure.

Generic search/AI/offline cache must not expose Vault secrets.

## Document Studio
Document Studio generates/version/reviews/delivers proposals, estimates/quotes, contracts, invoices/receipts/statements and other approved documents.

Business records remain authoritative. Accepted/executed content receives an immutable Final Snapshot. Documenso/SignatureConnector owns signature transaction execution.

Àríyá may draft document narrative, but send/accept/sign remain controlled actions.

## Requests and client lifecycle
Requests are structured asks that can be triaged/converted into Tasks, Projects, Support, Approvals, Opportunities/Estimates, Change Requests or other workflows.

Client Lifecycle coordinates onboarding/active/offboarding using existing records rather than creating shadow copies.

## Data provenance and sync
Synced/derived/imported/AI information should expose source, authority and freshness when material. Every connector declares sync direction/conflict policy.

Do not overwrite authoritative Re:Solve fields merely because an external system also has a value.

## Data extensibility
Custom fields are typed/validated definitions with explicit API/Portal/search/sensitivity rules. Tags and controlled taxonomy are distinct. Do not scatter arbitrary JSON blobs through features.

## Import/export/data quality
Imports require mapping, validation and dry-run. Exports are permission-aware. Data Quality should surface duplicates, stale/missing data and broken mappings. Generic exports exclude Vault secrets.

## Secure External Access
Narrow expiring/revocable guest links may be used for proposal/estimate acceptance, contract signature handoff, requested uploads, surveys/forms, approvals and controlled documents without fake Portal accounts.

## Core UI Component Framework — NON-NEGOTIABLE
Re:Solve has a source-owned Core UI Component Framework.

Mandatory primary sources/influences:
1. Re:Solve Product Design Language
2. shadcn/ui
3. Untitled UI React
4. Tremor
5. React Aria / Base UI / Radix
6. TanStack Table / TanStack Query
7. approved specialist libraries only when needed

Use these heavily, but normalize final components into Re:Solve tokens/composites. Do not create library soup or random page-specific controls.

## Navigation — NON-NEGOTIABLE
Navigation must be simple, intuitive and obvious like a well-structured service CRM.

Use:
- clear left Admin sidebar with text labels;
- shallow major areas;
- strong active state;
- strong TopBar;
- strong avatar/account;
- strong notifications trigger/tray;
- visible Search/Command;
- visible Àríyá entry;
- area tabs/views for child pages.

Avoid:
- Odoo-style app grids/module launchers;
- Twenty-style object/app switching as the primary navigation model;
- endless nested sidebar trees;
- icon-only root navigation;
- every child page in the root.

## Shell quality
FOUND-001 must produce production-quality foundation components for Sidebar, TopBar, ResolveAvatar/AccountMenu, NotificationTrigger/Tray, Search/Command entry, Quick Create, Àríyá trigger/panel foundation, mobile navigation and shared states.

Stock starter-template shell quality is not acceptable.

## Component Gallery
FOUND-001 establishes a development-only Component Gallery/Storybook-equivalent for canonical Core UI components and states.

## PWA/responsive/accessibility
PWA/responsiveness starts with the foundation. Review phone, tablet, laptop and desktop intentionally. Target WCAG 2.2 AA. Portal mobile is especially important. Sensitive data is excluded from unsafe offline caching.

## Design QA
Feature completion includes functional, security, responsive/PWA, accessibility, Core UI consistency, visual hierarchy/polish and degraded/performance review.

## Data/demo rules
Use a coherent fictional demo universe. Airix Media may be the operating entity; client organisations and demo people should be fictional. Never seed real credentials/secrets/private client data.

## Source of truth
When implementation conflicts with Product Bible:
1. stop;
2. identify contradiction;
3. follow Product Bible unless a new decision explicitly changes it;
4. update Product Bible before establishing new product truth.
