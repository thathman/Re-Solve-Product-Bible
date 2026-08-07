---
name: re-solve-spec
description: Create and refine implementation-ready Re:Solve product specifications before any build work. Use for product areas, pages, workflows, settings, notifications, portals, APIs, MCP tools, plugins, connectors, permissions, PWA behavior, acceptance criteria, and Lovable build slices.
---

# Re:Solve Spec Creator

This skill adapts GitHub Spec Kit's specification-first discipline for the Re:Solve Product Bible.

The Product Bible is the canonical source of product truth. Comprehensive planning belongs here. Implementation work must be broken into small, reviewable Lovable build slices rather than dumping entire product areas into one build prompt.

## Workflow

### 1. Constitution check
Read the product constitution and any existing related specs before drafting. Preserve locked decisions and call out contradictions instead of silently replacing them.

### 2. Define the problem
State:
- purpose
- user problem
- desired outcome
- why this capability exists
- primary and secondary users

Focus first on what the product must do and why. Only prescribe technology where architecture rules require it.

### 3. Define scope
Explicitly state:
- in scope
- out of scope
- dependencies
- related records
- related modules
- plugin implications
- connector implications
- notification implications
- automation implications
- API implications
- MCP implications

### 4. Specify the complete experience
For every page, panel, modal, drawer, widget, list, record workspace, settings section, or portal surface, specify as applicable:
- route/surface
- navigation placement
- users
- permissions
- header
- summary information
- primary actions
- secondary actions
- tabs/sections
- cards/widgets
- tables and columns
- search
- filters
- sorting
- saved views
- bulk actions
- forms and fields
- validation
- related records
- activity/timeline
- loading state
- skeleton state
- empty state
- first-use state
- error state
- partial-data state
- offline state
- permission-denied state
- disabled/read-only state
- success/confirmation state
- responsive behavior
- PWA behavior
- keyboard behavior
- accessibility
- audit events
- notifications
- automation events
- API exposure
- MCP tool candidates
- plugin extension slots
- connector interactions
- analytics/telemetry

### 5. Define business rules and states
Enumerate:
- record states
- transitions
- ownership
- permissions
- calculations
- constraints
- edge cases
- destructive actions
- recovery behavior
- organisation isolation
- property isolation

### 6. Define data requirements
Identify required business records and relationships without prematurely locking database implementation.

Distinguish clearly between:
- first-class records
- connector mappings
- files
- vault items
- derived values
- cached external data
- audit history

Mark sensitive/confidential data and retention requirements.

### 7. Design notifications deliberately
For each meaningful event specify:
- event
- recipient
- priority
- in-app eligibility
- push eligibility
- email eligibility
- WhatsApp eligibility
- whether mandatory or user-configurable
- grouping/deduplication key
- deep link/action
- expiry
- escalation behavior

Notifications are a platform primitive, not an afterthought.

### 8. Define API and MCP behavior
Meaningful UI operations should normally have a documented API equivalent unless explicitly excluded.

Specify:
- read/write scope
- authentication
- permission scope
- filtering/pagination
- idempotency where required
- audit requirements
- dangerous action handling
- MCP tool candidates
- confirmation requirements
- redaction rules

### 9. Define acceptance criteria
Acceptance criteria must be observable and testable.

Include where relevant:
- happy path
- invalid input
- permission denial
- cross-organisation denial
- cross-property denial
- empty state
- failure state
- offline/PWA behavior
- mobile behavior
- accessibility
- audit behavior
- notification behavior

### 10. Define realistic demo data
Describe realistic records needed to demonstrate the feature in Lovable. Avoid generic Acme Corp / John Doe examples when domain-realistic examples reveal more product behavior.

### 11. Quality review
Before finalizing, check for:
- contradictions
- missing states
- hidden assumptions
- duplicate functionality
- generic dashboard patterns
- unnecessary dependencies
- unclear ownership
- missing permissions
- missing notification behavior
- missing API/MCP exposure
- missing mobile/PWA behavior
- missing accessibility
- missing extension points

### 12. Break into Lovable build slices
The spec may be exhaustive. The build slices must be small.

Each slice should:
- have one clear objective
- touch a bounded surface
- be independently reviewable
- include its acceptance criteria
- avoid implementing future slices prematurely

## Re:Solve product rules

- Re:Solve is a loaded operating system, not a generic SaaS dashboard.
- Prefer deliberate information architecture, dense-but-calm operational UX, and workflow speed over decorative KPI-card grids.
- PWA and responsive behavior are requirements from the beginning.
- Use a coherent design system. Build implementation around shadcn/ui and strong alternatives when they materially improve usability rather than creating random bespoke controls.
- Core features, plugins, and connectors are distinct concepts.
- Payment providers are extensible through plugins/connectors and must not be hard-coded as core dependencies.
- Chatwoot owns managed client support: helpdesk, client-property web chat, support conversations, support knowledge, support agents/teams, and Chatwoot's own AI engine.
- Re:Solve AI is a separate system and must not become a wrapper around Chatwoot AI.
- WhatsApp/Baileys is primarily for Re:Solve-to-client operational communication, ticket/status updates, messages, reminders, and notifications.
- The Secure Vault is for controlled sharing of confidential credentials, passwords, keys, files, proposals, contracts, and other sensitive information.
- Every important capability must consider permissions, audit, notifications, automations, API, MCP, plugins, connectors, responsive/PWA behavior, security, and accessibility.
- Re:Solve must expose a first-class API and MCP surface suitable for integrations with tools such as Claude, ChatGPT, OpenClaw/Hermes, Codex, and future agents.
- Do not preserve legacy Re:Solve implementation technology merely because it exists. Product behavior is the source of truth; implementation should favor the current Lovable-compatible model unless a product requirement dictates otherwise.

## Standard major-spec structure

1. Purpose
2. Goals
3. Non-goals
4. Users
5. Roles and permissions
6. Information architecture
7. Detailed user experience
8. Business rules and states
9. Data requirements
10. Notifications
11. Automations
12. API
13. MCP
14. Plugins and extension points
15. Connectors
16. Security and audit
17. Responsive/PWA behavior
18. Accessibility
19. Analytics
20. Loading/empty/error/offline states
21. Acceptance criteria
22. Demo data
23. Open questions and deferred decisions
24. Lovable build slices

## Spec Kit lineage

This skill follows GitHub Spec Kit's core discipline: establish governing principles, specify intent and behavior, clarify ambiguity, plan deliberately, break work into tasks, validate consistency, and only then implement. Re:Solve adapts that workflow to a long-lived Product Bible rather than treating each feature specification as disposable build context.
