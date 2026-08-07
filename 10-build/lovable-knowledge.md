# Re:Solve Lovable Knowledge

## Purpose
This document defines the persistent product and engineering rules that should be loaded into Lovable Knowledge so every build slice inherits the same decisions without repeating the entire Product Bible.

Lovable Knowledge must be concise enough to stay useful, strict enough to prevent architectural drift, and stable enough to remain valid across many feature slices.

## Product identity
Re:Solve is a modular operating system for running client services, digital properties, projects, billing, support context, knowledge, confidential information, automations, and operations from one coherent application.

Re:Solve is not a generic CRM template and must not devolve into disconnected CRUD pages or interchangeable KPI dashboards.

## Build philosophy
- Build in small, bounded slices.
- Never implement future slices just because they are mentioned in a spec.
- Prefer complete flows over broad but shallow feature coverage.
- Every slice must include loading, empty, error, permission, responsive, and accessibility behavior relevant to that slice.
- Preserve Product Bible terminology and business ownership boundaries.
- Do not silently invent new product concepts when a canonical concept already exists.

## Lovable-first implementation
- Favor Lovable's current preferred frontend/backend patterns over the legacy Re:Solve architecture.
- Supabase may be used freely for database, authentication, storage, realtime, and development/demo workflows.
- The application must remain portable after export and must not rely on Lovable-only runtime services to function.
- Avoid scattering direct provider SDK calls through UI components or domain logic.
- Use service/repository boundaries where practical so data and providers can be replaced later.
- Do not preserve NestJS, TypeORM, GraphQL, Apollo, Vite, or other legacy implementation choices merely because they exist in the old Re:Solve repository.

## Application structure
Re:Solve is one application with two role-shaped experiences:
- Admin OS for staff and operators.
- Client Portal for client users.

They share identity, permissions, data, notifications, files, audit, plugin infrastructure, connector infrastructure, and design tokens, but they do not share identical navigation density or page composition.

## Core domain ownership
Core owns:
- identity
- organisations
- contacts
- memberships
- roles and permissions
- properties
- projects
- commercial records
- billing records
- notifications
- files
- Secure Vault metadata/access policy
- Re:Solve Knowledge
- approvals
- activity/audit
- automations
- settings
- plugin runtime
- connector runtime
- API and MCP policy

## Chatwoot boundary
Chatwoot owns managed client support operations:
- helpdesk conversations
- website chat on client properties
- support channels/inboxes
- support agents and teams
- routing and assignment
- support attachments
- support knowledge base
- Chatwoot Captain and Chatwoot AI

Re:Solve must not rebuild the Chatwoot agent console.

Re:Solve may surface support summaries, conversation references, business context, property context, support entitlement, SLA context, incidents, analytics, and deep links.

Do not mirror every Chatwoot message into Re:Solve unless a specific product requirement explicitly calls for it.

## WhatsApp / Baileys boundary
WhatsApp/Baileys is primarily for Re:Solve-to-client operational communication such as:
- ticket/status updates
- project updates
- reminders
- approval requests
- invoice/payment notifications
- renewal notices
- property alerts
- direct operational messages

It is not the primary system for a client's own end-customer support; that remains Chatwoot.

## AI boundary
Re:Solve has its own built-in AI system.
Chatwoot AI remains separate.
Do not make Re:Solve AI a wrapper around Chatwoot Captain.

Re:Solve AI must inherit caller permissions, respect organisation/property scope, expose controlled tools, and never receive arbitrary SQL or unrestricted Vault access.

## Plugins and connectors
Plugins add business capability.
Connectors integrate specialist external systems.

Do not collapse these concepts.

Plugin examples:
- OJS publishing operations
- advanced journal management
- SEO operations
- advanced accounting
- WooCommerce operations

Connector examples:
- Chatwoot
- WhatsApp/Baileys
- Bachs/payment providers
- OpenRouter
- Documenso
- Uptime Kuma
- OpenBao
- OJS
- WordPress
- WooCommerce
- email/calendar providers

## Payment providers
Core billing is provider-neutral.
Payment providers are added through plugins/connectors.
Verified provider events establish payment truth; browser return pages do not.

## Secure Vault
Secure Vault is for controlled sharing of confidential information and files, including:
- passwords
- API keys
- SSH keys
- recovery material
- confidential notes
- proposals
- contracts
- certificates
- sensitive client documents

Vault content requires stronger permissions, reveal/download controls, audit, and step-up authentication where configured.
Generic search and AI retrieval must not index raw Vault values.

## Notifications
Notifications are a core platform primitive.
Every meaningful business event must consider:
- recipient
- priority
- in-app
- push
- email
- WhatsApp
- grouping/deduplication
- deep link
- escalation
- mandatory vs user-configurable behavior

Do not treat notifications as toast messages only.

## API and MCP
Meaningful UI operations should normally have an API equivalent unless deliberately excluded.
Re:Solve exposes a first-class API and MCP surface for tools such as Claude, ChatGPT, OpenClaw/Hermes, Codex, and future agents.

API/MCP operations must be scoped, permission-aware, auditable, rate-limited where appropriate, and safe by default.
Dangerous write actions require stronger controls than ordinary reads.

## PWA and responsiveness
PWA and responsive behavior are requirements from the beginning.
Every slice must be tested conceptually at phone, tablet, laptop, and desktop widths.

The Client Portal should have especially strong mobile ergonomics.
Sensitive Vault data must never be cached for offline use.
Offline behavior must distinguish safe cached data from online-only sensitive operations.

## UI system
Use shadcn/ui and Radix-style accessible primitives as the default foundation.
Use stronger alternatives when they materially improve complex interactions such as data grids, editors, charts, calendars, command palettes, or drag-and-drop.

Do not create random bespoke controls when a mature accessible primitive exists.
Do not create a generic admin-dashboard visual language.

The intended experience is:
- dense but calm
- operational
- fast
- highly legible
- deliberate hierarchy
- strong record relationships
- keyboard-friendly on Admin
- touch-friendly on Portal

## Design anti-patterns
Avoid:
- walls of identical KPI cards
- excessive gradients
- meaningless glassmorphism
- decorative charts without operational value
- excessive pills/badges
- giant empty hero areas in operational pages
- cramped mobile tables
- hidden critical actions
- inconsistent spacing and radii
- inline one-off design systems per page

## Data and demo rules
Use realistic Re:Solve/Airix-style demo records when implementation requires data.
Avoid generic Acme Corp / John Doe filler when realistic examples reveal product behavior better.

Demo data should exercise:
- organisation hierarchy
- multiple contacts and roles
- nested properties
- active and completed projects
- invoices in multiple states
- approvals
- property health variation
- notification variety
- support references
- Vault metadata without real secrets

## Permissions and audit
Use capability-based permissions, not only broad role checks.
Every sensitive mutation and access action should consider audit requirements.

Negative authorization paths are product requirements:
- cross-organisation denial
- cross-property denial
- insufficient permission
- expired/disabled identity
- Vault access denial

## Extension safety
Plugins and connectors must use declared extension points.
They must not silently alter core navigation, schemas, permissions, or secrets outside approved contracts.

## Source of truth
When implementation details conflict with the Product Bible:
1. stop
2. identify the contradiction
3. follow the Product Bible unless a new decision explicitly changes it
4. update the Product Bible before establishing a new product rule
