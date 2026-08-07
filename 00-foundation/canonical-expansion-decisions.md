# Re:Solve Canonical Expansion Decisions

## Purpose
This document records cross-cutting product decisions that override ambiguous or older wording elsewhere in the Product Bible. Existing specs should be interpreted consistently with these rules and updated as they are touched.

## Product scope exclusions
Re:Solve is not an HR system.

The core product must not add:
- employee HR records
- payroll
- leave/absence management
- recruitment
- performance reviews
- attendance
- workforce HR administration
- timesheets or time-tracking as a product feature

Projects may still have dates, estimates, deadlines, owners, assignees, milestones, effort notes and delivery status, but Re:Solve does not require staff to submit timesheets.

Re:Solve also does not implement Client Service Consumption/allowance-metering as a core feature. Services may have scope, SLA, price, billing cadence, renewal, included properties and contractual terms, but the product does not need an hours/credits consumed-versus-remaining ledger.

## Workspace and operating entities
Every installation has one canonical Workspace even when multi-workspace SaaS behavior is not enabled.

An Operating Entity is the business/legal/brand identity using Re:Solve to deliver services. Airix Media is an Operating Entity in the first deployment; it is not modeled as an ordinary client Organisation.

A Workspace may eventually contain multiple Operating Entities/Brands while still remaining one installation.

## Identity
`Principal` is the general authorization actor.

Principals may include:
- Human User
- Service Account
- API Client
- MCP Client
- Plugin
- Connector

`User` means an authenticated human identity. Staff, client users and contractors are human-user contexts.

Permissions and access grants target Principals and are always combined with scope.

## Permission naming
Canonical permission grammar is:

`domain.action` when no meaningful sub-resource exists, or `domain.resource.action` when it does.

Examples:
- `organisations.read`
- `properties.access.manage`
- `vault.metadata.read`
- `vault.secret.reveal`
- `connectors.credentials.rotate`
- `connectors.events.replay`
- `api.tokens.manage`
- `mcp.clients.manage`

Specs should not invent alternate word order for the same capability.

## Files and Secure Vault
A protected confidential document is a Vault Item, not simultaneously an ordinary File record with a second access path.

Files and Vault Items may share the same provider-neutral storage infrastructure, but they have separate domain identities and permission models.

Moving ordinary content into Vault must remove ordinary access paths or create a new protected representation with the original record linked as provenance.

Commercial records such as Proposal and Contract remain first-class business records and may reference a protected Vault Item containing a confidential/final document version.

## Plugins and connectors
A Plugin adds Re:Solve business/product capability. A Connector integrates an external system.

Optional provider packages may be distributed as plugins that register connector implementations.

Example:
`Billing Core -> PaymentConnector contract -> Bachs provider package registers BachsPaymentConnector`.

Business domains must depend on provider-neutral connector capabilities, not provider names.

## Monitoring
Re:Solve owns a native Monitoring Engine and Property Posture model.

External systems such as Cloudflare, Uptime Kuma and hosting/monitoring vendors are optional Monitoring Connectors that contribute signals. Uptime Kuma is not a required deployment dependency.

The native engine should grow incrementally from HTTP/HTTPS, latency and certificate/domain expiry into DNS, TCP, heartbeat, backup freshness and independent probe workers.

## Re:Solve AI
The user-facing name of Re:Solve's built-in AI is **Àríyá**.

Internal technical concepts may still use names such as `AIProvider`, `AIRun`, `AIProfile`, `AIConnector`, and `AITool`.

Àríyá is separate from Chatwoot Captain.

## Navigation and UI
Re:Solve navigation must be simple, obvious and task-oriented.

Positive qualities:
- clear left navigation similar in legibility to well-structured service CRMs such as Perfex/Brevo
- obvious section names
- shallow hierarchy
- strong active state
- strong top bar
- excellent avatar/account control
- excellent notifications entry and tray
- global search/command access
- visible Àríyá entry

Anti-patterns:
- Odoo-style app launchers/module grids
- Twenty-style object/app navigation that requires product knowledge to understand where work lives
- deeply nested expanding navigation trees
- exposing every sub-page in the root navigation
- icon-only primary navigation
- workspace complexity presented before users need it

## Core UI Component Framework
The Re:Solve Core UI Component Framework is mandatory and is product infrastructure, not optional polish.

Primary sources/influences:
1. Re:Solve product design language
2. shadcn/ui
3. Untitled UI React
4. Tremor
5. React Aria / Base UI / Radix where their primitive behavior is strongest
6. TanStack Table/Query and approved specialist libraries

External components must be normalized into Re:Solve-owned tokens, components and composites. The product must not look like several component libraries stitched together.

## Attention
Notification and Attention are different concepts.

A Notification records that something happened and may be delivered through channels.
An Attention Item represents a condition that still deserves awareness or action now.

Dashboard, My Work, Portal Home, digests and Àríyá briefings may consume the same Attention Engine.

## Data authority
Synced, derived, imported and AI-produced information must expose source/authority/freshness where material.

Connector synchronization must declare ownership direction and conflict policy rather than silently overwriting records.

## Audit
Security/accountability Audit Events are append-only. Corrections create subsequent events/annotations rather than rewriting historical evidence.
