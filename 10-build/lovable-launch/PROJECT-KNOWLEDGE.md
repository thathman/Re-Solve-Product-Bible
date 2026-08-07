# Re:Solve — Lovable Project Knowledge

Paste the content below into **Project settings → Knowledge**.

## Product and build discipline
Re:Solve is a reusable business operating system for client relationships, digital Properties, projects/delivery, sales/documents, billing, support context, monitoring/renewals, requests, knowledge, confidential data, automation, plugins/connectors and API/MCP. Airix Media is the first Operating Entity/deployment.

Build one app with two shells: dense/keyboard-forward Admin OS and calmer/mobile-first Client Portal. They share canonical data, identity, permissions, platform services and Core UI tokens.

Build only the current bounded slice. Adjacent Product Bible features are context, not permission to implement them. Preserve canonical terminology. If requirements conflict or would establish new product truth, stop/report instead of silently deciding. Use fictional demo data only; never use real client secrets/private data. Do not scaffold every future module.

## Architecture / portability
Favor Lovable's current strongest React/full-stack patterns over legacy NestJS/GraphQL/TypeORM. Supabase is acceptable for development DB/auth/storage/realtime/server functions. Exported source must remain maintainable/self-hostable without Lovable runtime dependency.

Keep business/provider/data logic behind shared domain/service/repository/connector boundaries where practical; avoid scattered direct provider/Supabase calls in presentation components. Version migrations. Storage/provider ids are not canonical business identity. Background work uses explicit jobs/events. API/MCP/Àríyá use controlled application services/Actions, not UI scraping or arbitrary DB access.

## Identity / authorization
Workspace = deployment boundary. Operating Entity/Brand = business doing the work; Airix Media is the first. Organisation = client/prospect/vendor/partner/institution; do not model Airix Media as an ordinary client Organisation. Contact = real person. User = authenticated human. Principal = User, Service Account, API Client, MCP Client, Plugin or Connector acting under authorization. Membership links people to Organisation/context; email alone is not canonical identity.

Roles are permission bundles. Authorization = capability + scope and is enforced server-side. Permission grammar: `domain.action` or `domain.resource.action`. Require negative cross-Organisation/Property tests.

## Explicit exclusions
Never introduce HR, payroll, recruitment, leave/attendance, employee performance reviews, Timesheets/Time Tracking, or Client Service Consumption/remaining-hours/service-credit metering. Projects may still have assignments, estimates, milestones, deadlines, recurring tasks and operational Expenses.

## System boundaries
Chatwoot owns managed support conversations/messages, web chat, inboxes/channels, routing, agents/teams, support attachments, support Knowledge and Captain. Re:Solve owns client/property/service context, entitlement, incidents, safe references/summaries, analytics and deep links. Do not rebuild Chatwoot helpdesk/agent console or mirror every message.

WhatsApp/Baileys is primarily Re:Solve↔client operational communication: status, reminders, approvals, billing/renewal/property alerts and direct operational messages; not client end-customer support.

Billing is provider-neutral. Verified provider events/records establish payment truth; browser returns do not. Plugins add product capability; Connectors integrate external systems. A provider package may be a Plugin that registers a Connector implementation.

## Àríyá / platform primitives
The user-facing Re:Solve AI is **Àríyá**. It is separate from Chatwoot Captain, inherits caller permissions, uses controlled tools/registered Actions, shows evidence/freshness, distinguishes fact from inference, and never gets arbitrary SQL or generic Vault secret access. Avoid a generic floating sparkle AI bubble; use TopBar/Command/contextual entry and a native assistant workspace.

Attention = unresolved condition needing action/awareness now. Notification = recipient-specific awareness/delivery. Activity = durable business chronology. Audit = append-only evidentiary history. Do not collapse them or use unread Notification state as business-resolution truth.

Reusable consequential mutations use the Action Registry so UI, Command Palette, Àríyá, API, MCP, Automations and plugins share one action contract with permission/scope, risk, validation, confirmation, approval/step-up, idempotency/side effects and audit.

## Properties / monitoring / renewals
Property is first-class with hierarchy, services, projects, support, files, Vault, connectors, access, monitoring and renewals. Re:Solve includes native Monitoring; Uptime Kuma/external monitors are optional connectors. Native monitoring starts with HTTP/HTTPS, latency, SSL/domain expiry and grows only through explicit slices. Monitoring Worker/Probe must be independently deployable conceptually.

Property Posture is explainable and source/freshness-aware; provider outage is not automatically Property outage. Domain, hosting, certificate, service, contract and similar expiry obligations use first-class Renewal/Expiry records and Renewal Desk. Cloudflare is an optional domain/DNS/edge/health connector; high-risk writes such as DNS changes require narrow Actions/confirmation.

## Files / Vault / documents / data
Files = ordinary documents. Secure Vault = protected confidential information/files. A protected document must not retain an ordinary File bypass path. Vault values are excluded from generic search/logs/notification previews/unsafe offline cache/ordinary Àríyá or MCP retrieval.

Document Studio handles Proposals, Estimates/Quotes, Contracts, Invoices, Receipts, Statements and approved generated documents. Accepted/executed content gets an immutable Final Snapshot. Documenso/SignatureConnector executes signatures; Re:Solve owns document truth. Àríyá may draft but cannot silently send/accept/sign.

Synced/imported/derived/AI data should show source, authority and freshness when material. Every Connector declares sync direction/conflict policy; external ids are mappings. Custom Fields are typed/validated with search/API/Portal/sensitivity rules. Imports require mapping/validation/dry-run; exports are permission-aware; generic exports exclude Vault secrets.

## Core UI Component Framework — NON-NEGOTIABLE
Re:Solve owns the final UI system. Mandatory major sources/influences:
1. Re:Solve Product Design Language
2. shadcn/ui
3. Untitled UI React
4. Tremor
5. React Aria / Base UI / Radix
6. TanStack Table / TanStack Query
7. approved specialist libraries only when a demonstrated flow needs them

Use shadcn, Untitled UI and Tremor heavily, then normalize into Re:Solve-owned tokens/components. No library soup or page-specific design systems.

Core application components include AppShell, AdminSidebar, PortalNavigation, TopBar, ResolveAvatar/AccountMenu, GlobalSearch/CommandPalette, QuickCreate, NotificationTrigger/Tray/Item, AriyaTrigger/Panel, PageHeader/RecordHeader/Tabs, FilterBar/SavedViewPicker/BulkActionBar, AttentionItem, Activity/Audit timelines, Health/Freshness/Connector status, PermissionGate/StepUpDialog, SensitiveValue/FileCard and complete loading/empty/error/permission/offline/not-built/connection states. FOUND-001 creates a development Component Gallery/Storybook-equivalent.

## Navigation — NON-NEGOTIABLE
Use simple, shallow, labeled business navigation closer to Perfex/Brevo clarity. Admin has one strong labeled left Sidebar plus a strong TopBar; child pages use area tabs/views. Reject Odoo-style app grids/module launchers, Twenty-style object/module switching as the main model, icon-only root nav, endless nested trees, duplicate destinations and uncontrolled plugin root entries.

TopBar should provide context/breadcrumb, visible Search/Command, Quick Create, Àríyá, Notifications, meaningful degraded status only when needed, and useful Avatar/Account. Mobile is deliberately recomposed, not a squeezed desktop sidebar.

## PWA / accessibility / quality
PWA/responsiveness start at foundation. Review phone, tablet, laptop, desktop and standalone mode intentionally. Portal common flows work on phone; Admin essential actions remain usable. Never cache sensitive data unsafely. Target WCAG 2.2 AA.

Relevant screens include loading/skeleton, empty/first-use, success, error, partial/stale, permission/read-only, degraded-provider and offline states. A slice is complete only after functional, security, responsive/PWA, accessibility, Core UI/design, test and portability review.

## Source of truth
The private `Re-Solve-Product-Bible` is canonical. File paths in prompts are traceability references; do not assume direct access. This Project Knowledge, installed canonical `resolve-*` skills and the current build prompt are the direct implementation context.
