# Re:Solve — Lovable Project Knowledge

Paste this content into **Project settings → Knowledge** for the Re:Solve Lovable project.

## Product
Re:Solve is a modular business operating system for client relationships, digital Properties, delivery/projects, sales/commercial documents, billing, support context, monitoring/renewals, requests, knowledge, confidential information, automation, plugins/connectors, API/MCP and operations.

Airix Media is the first Operating Entity/deployment, but Re:Solve must remain reusable for other businesses and external deployments.

Build one application with two role-shaped shells: dense/keyboard-forward Admin OS and calmer/mobile-first Client Portal. They share canonical data, auth, permissions, platform services and Core UI tokens.

## Build discipline
- Build only the current bounded slice. Adjacent Product Bible features are context, not permission to implement them.
- Preserve canonical terminology and product boundaries.
- When requirements conflict or reveal missing product truth, stop/report rather than silently inventing a rule.
- Use realistic fictional demo data. Never use real client credentials/secrets/private data.
- Do not create placeholder schemas/routes for every future module.

## Architecture and portability
- Favor Lovable's current strongest React/full-stack patterns over the legacy NestJS/GraphQL/TypeORM architecture.
- Supabase is acceptable for development database/auth/storage/realtime/server functions.
- Exported source must remain maintainable and independently self-hostable without a Lovable runtime dependency.
- Keep business/provider/data logic behind shared domain/service/repository/connector boundaries where practical; avoid scattered direct provider/Supabase calls in presentation components.
- Version schema/data migrations. Do not use storage URLs/provider ids as canonical business identity.
- Background work uses explicit jobs/events. API/MCP/Àríyá use controlled application services/Actions, not UI scraping or arbitrary DB access.

## Canonical identity
- Workspace = one Re:Solve deployment boundary.
- Operating Entity/Brand = business doing the work; Airix Media is the initial Operating Entity.
- Organisation = client/prospect/vendor/partner/institution. Do not model Airix Media as an ordinary client Organisation.
- Contact = real person/business contact.
- User = authenticated human identity.
- Principal = any authorization actor: User, Service Account, API Client, MCP Client, Plugin or Connector.
- Membership links Contact/User to Organisation/context. Email is not canonical identity by itself.
- Roles are permission bundles. Authorization is capability + scope and is enforced server-side.
- Permission naming: `domain.action` or `domain.resource.action`.
- Negative cross-Organisation/Property authorization paths are required.

## Explicit exclusions
Never introduce HR management, payroll, recruitment, leave/attendance, employee performance reviews, Timesheets/Time Tracking, or Client Service Consumption/remaining-hours/service-credit metering. Projects may still have assignments, estimates, milestones, deadlines, recurring tasks and operational Expenses.

## Specialist-system boundaries
- Chatwoot owns managed support conversations/messages, web chat, inboxes/channels, routing, agents/teams, support attachments, support Knowledge and Captain. Re:Solve owns client/property/service context, entitlement, incidents, safe references/summaries, analytics and deep links. Do not rebuild Chatwoot helpdesk/agent console or mirror every message.
- WhatsApp/Baileys is primarily Re:Solve↔client operational communication: status, reminders, approvals, billing/renewal/property alerts and direct operational messages; not client end-customer support.
- Billing is payment-provider-neutral. Verified provider events/records establish payment truth; browser returns do not.
- Plugins add business capability. Connectors integrate external systems. Provider packages may be Plugins that register Connector implementations.

## Àríyá
The user-facing Re:Solve AI is **Àríyá**. Internal technical types may remain AIProvider/AIRun/AITool.
Àríyá is separate from Chatwoot Captain, inherits caller permissions, uses controlled tools/registered Actions, exposes evidence/freshness, distinguishes fact from inference, and never receives arbitrary SQL or generic Vault secret access.
Avoid a generic floating purple/sparkle AI bubble. Use strong TopBar/Command/contextual entry and a native assistant workspace/panel.

## Platform primitives
- Attention Item = unresolved condition requiring action/awareness now.
- Notification = recipient-specific awareness/delivery that something happened.
- Activity = durable business chronology.
- Audit = append-only evidentiary history.
Do not collapse these concepts or use unread notification state as business resolution truth.

Reusable consequential mutations use the Action Registry so UI, Command Palette, Àríyá, API, MCP, Automations and plugins share one action contract. Actions declare permission/scope, risk, validation, confirmation, approval/step-up, idempotency/side effects and audit.

## Properties / monitoring / renewals
Property is a first-class central object with hierarchy, services, projects, support, files, Vault, connectors, access, monitoring and renewals.
Re:Solve contains a native Monitoring Engine. Uptime Kuma/external monitors are optional connectors, not dependencies. Native monitoring begins with HTTP/HTTPS, latency, SSL/domain expiry and grows through explicit slices. Monitoring Worker/Probe must be independently deployable conceptually.
Property Posture is explainable and source/freshness-aware; provider outage is not automatically property outage.
Domain, hosting, certificate, service, contract and similar expiry obligations use first-class Renewal/Expiry records and Renewal Desk.
Cloudflare is an optional first-class domain/DNS/edge/health connector; high-risk writes such as DNS changes require narrow Actions/confirmation.

## Files / Vault / documents
Files = ordinary managed documents. Secure Vault = protected confidential information/files. A protected confidential document must not retain a second ordinary File access path. Vault values are excluded from generic search, logs, notification previews, unsafe offline caches and ordinary Àríyá/MCP retrieval.

Document Studio generates/version/reviews/delivers Proposals, Estimates/Quotes, Contracts, Invoices, Receipts, Statements and other approved documents. Accepted/executed content receives an immutable Final Snapshot. Documenso/SignatureConnector owns signature transaction execution; Re:Solve owns business document truth. Àríyá may draft content but does not silently send/accept/sign.

## Data provenance/extensibility
Synced/imported/derived/AI data should show source, authority and freshness when material. Every Connector declares sync direction/conflict policy; external ids are mappings, not canonical identity.
Custom Fields are typed/validated definitions with explicit search/API/Portal/sensitivity rules. Tags/taxonomy are distinct. Avoid arbitrary feature-specific JSON blobs.
Imports require mapping, validation and dry-run; exports are permission-aware; Data Quality handles duplicates/stale/broken mappings; generic exports exclude Vault secrets.

## Core UI Component Framework — NON-NEGOTIABLE
Re:Solve owns the final UI system. Mandatory major sources/influences:
1. Re:Solve Product Design Language
2. shadcn/ui
3. Untitled UI React
4. Tremor
5. React Aria / Base UI / Radix
6. TanStack Table / TanStack Query
7. approved specialist libraries only when a demonstrated flow needs them

Use shadcn, Untitled UI and Tremor heavily, then normalize into Re:Solve-owned tokens/components. Do not create library soup or page-specific design systems.

Core application components include AppShell, AdminSidebar, PortalNavigation, TopBar, ResolveAvatar/AccountMenu, GlobalSearch/CommandPalette, QuickCreate, NotificationTrigger/Tray/Item, AriyaTrigger/Panel, PageHeader/RecordHeader/Tabs, FilterBar/SavedViewPicker/BulkActionBar, AttentionItem, Activity/Audit timelines, Health/Freshness/Connector status, PermissionGate/StepUpDialog, SensitiveValue/FileCard and complete loading/empty/error/permission/offline/not-built/connection states.

FOUND-001 must create a development-only Component Gallery/Storybook-equivalent for reusable components/states.

## Navigation — NON-NEGOTIABLE
Use simple, shallow, labeled business navigation closer to Perfex/Brevo clarity. Admin has one strong labeled left Sidebar plus a strong TopBar. Child pages use area tabs/views.
Reject Odoo-style app grids/module launchers, Twenty-style object/module switching as the main mental model, icon-only root nav, endless nested accordion trees, duplicate destinations and uncontrolled plugin root entries.
TopBar should support current context/breadcrumb, visible Search/Command, Quick Create, Àríyá, Notifications, meaningful degraded status only when needed, and useful Avatar/Account.
Mobile is deliberately recomposed, not a hidden/squeezed desktop sidebar.

## PWA / responsive / accessibility / quality
PWA and responsiveness start at foundation. Review phone, tablet, laptop, desktop and standalone mode intentionally. Portal common flows must work on phone; Admin essential actions remain usable. Sensitive data is never cached unsafely. Target WCAG 2.2 AA.
Every relevant screen includes loading/skeleton, empty/first-use, success, error, partial/stale, permission/read-only, degraded provider and offline states.
A slice is complete only after functional, security, responsive/PWA, accessibility, Core UI/design, test and portability review.

## Source of truth
The private Re-Solve-Product-Bible is canonical. File paths mentioned in build prompts are traceability references; do not assume direct access to that private repo. This Project Knowledge, installed canonical `resolve-*` skills and the current build prompt provide the direct instructions needed for implementation. If implementation would establish a new product rule, report it before proceeding.
