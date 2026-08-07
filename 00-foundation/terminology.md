# Re:Solve Terminology

This document defines canonical product language. Feature specs should reuse these terms unless a deliberate product decision changes them.

## Organisation

A client, prospect, partner, vendor, internal business unit, or other legal/operational entity represented in Re:Solve.

An organisation may have:
- contacts
- properties
- opportunities
- projects
- services
- commercial records
- invoices and payments
- support context
- files
- vault items
- connector mappings
- portal members

"Client" is a business state or relationship, not a separate record type from Organisation.

## Contact

A person associated with an organisation or, where appropriate, acting independently.

A contact may be:
- prospect contact
- client user
- billing contact
- approver
- property manager
- editor
- support contact
- technical contact
- vendor contact

A Contact and an authenticated User are related but not identical concepts.

## User

An authenticated identity able to access Re:Solve.

Users may represent:
- staff
- client organisation members
- contractors
- service accounts

A user may be linked to one or more contacts/memberships depending on the final identity model.

## Membership

A user's relationship to an organisation or workspace, including role, permissions, status, and scope.

Membership is the preferred concept for client portal access rather than embedding access rules directly on Contact.

## Team

A group of users used for ownership, routing, permissions, notifications, reporting, or operational responsibility.

Examples:
- Finance
- Client Success
- Technical Operations
- OJS Support

## Role

A named bundle of permissions.

Roles simplify administration but do not replace granular permissions.

## Permission

A capability that authorizes a user, role, token, plugin, connector, or AI client to read or perform a defined action.

Examples:
- `organisations.read`
- `projects.manage`
- `vault.reveal`
- `plugins.install`

## Property

A first-class digital or operational asset that an organisation owns, operates, publishes, hosts, manages, sells through, or depends on.

Examples:
- website
- journal
- OJS installation
- domain
- server
- hosting account
- store
- application
- infrastructure service

Properties may be nested.

## Property Type

A configurable classification describing the operational meaning and expected capabilities of a property.

Examples:
- Website
- Domain
- Journal
- OJS Installation
- Server
- Hosting
- WooCommerce Store

## Property Relationship

A typed relationship between properties.

Examples:
- parent / child
- hosted on
- published by
- domain for
- monitored by
- depends on

## Service

A defined commercial or operational service offered to or provided for an organisation.

Examples:
- website maintenance
- OJS management
- hosting
- support
- SEO
- development retainer

A service may exist in a catalogue and may be instantiated as an active client service.

## Client Service

An active service relationship between Re:Solve's operating organisation and a client.

It may define:
- scope
- price
- billing cycle
- SLA
- included properties
- support entitlement
- renewal date
- owner
- status

## Lead

An early potential commercial relationship that has not yet matured into a qualified opportunity.

## Opportunity

A qualified potential sale represented within a pipeline.

## Pipeline

A configurable sequence of commercial stages through which opportunities progress.

## Proposal

A commercial document describing an offered solution, scope, terms, and/or price before acceptance.

## Estimate / Quote

A priced commercial offer or estimate. Exact terminology may be configurable by deployment, but the underlying record should remain semantically clear.

## Contract

A first-class commercial record representing agreed terms. The signed document may be executed by an external signing connector while Re:Solve retains contract status and references.

## Project

A bounded body of work performed for an organisation, usually with outcomes, dates, participants, tasks, milestones, deliverables, files, and client-facing visibility.

## Task

A unit of actionable work assigned to one or more responsible users/teams with status, priority, dates, dependencies, and related context.

## Milestone

A significant project checkpoint, target, or phase boundary.

## Deliverable

A defined output intended for internal completion and/or client review, approval, delivery, or acceptance.

## Client Action

An explicit action required from a client before work can progress or close.

Examples:
- provide content
- approve design
- submit credentials
- sign contract
- pay invoice

## Approval

A structured decision request with outcomes such as:
- approve
- reject
- request changes

Approvals may attach to deliverables, proposals, estimates, contracts, change requests, or other records.

## Change Request

A structured request to modify previously agreed scope, deliverables, timing, or implementation.

## Invoice

A first-class billing record requesting payment.

## Payment

A confirmed monetary transaction or recorded payment event allocated against invoices or other receivables.

## Payment Provider

An external provider that moves or confirms money. Payment providers are implemented through plugins/connectors rather than hard-coded core assumptions.

## Subscription

A recurring commercial billing arrangement, distinct from a payment-provider-specific subscription object.

## Recurring Service

A service that renews or bills on a recurring schedule, potentially linked to a subscription or recurring invoice process.

## Credit Note

A financial record reducing or reversing all or part of an invoice amount.

## Receipt

A client-facing proof-of-payment document generated from confirmed financial events.

## Support Conversation

A support interaction whose message truth lives in Chatwoot. Re:Solve may retain references, context, summaries, metrics, related records, and operational metadata.

## Support Entitlement

The support level a client/service/property is entitled to receive, potentially including SLA, hours, channels, categories, or escalation rules.

## Incident

An operational event representing service degradation, outage, security issue, or other condition requiring coordinated response.

## Notification

A user-facing awareness item generated from an event and delivered through one or more channels according to policy and preference.

## Domain Event

A structured fact that something meaningful happened in Re:Solve.

Examples:
- `project.created`
- `invoice.paid`
- `property.degraded`
- `vault.item.revealed`

Domain events may drive notifications, automations, connectors, audit entries, analytics, and plugins.

## Automation

A configured workflow triggered by events, schedules, manual invocation, webhooks, or other supported triggers, executing one or more controlled actions.

## Plugin

An installable extension that adds or modifies business capabilities inside Re:Solve through supported extension points.

## Connector

An integration implementation that connects Re:Solve to an external system or provider.

## Connector Type

The reusable integration definition, such as Chatwoot, Bachs, OJS, or WooCommerce.

## Connector Instance

A configured connection to a specific external account/system/site.

Examples:
- Kampala University OJS
- Airix Store WooCommerce
- Primary Chatwoot account

## Integration Event

An inbound or outbound external event processed through the connector runtime with verification, idempotency, retry, status, and audit metadata.

## Secure Vault

The protected subsystem used for controlled storage and sharing of confidential information and files.

## Vault Item

A protected confidential item, which may represent a credential, secret, note, file, document, or other sensitive content.

## File

A managed binary/document object with metadata, ownership, access, relationships, versioning where required, and storage abstraction.

## Knowledge Article

A structured knowledge record owned by Re:Solve for internal or controlled client use. This is distinct from Chatwoot's support knowledge base.

## Activity

A human-readable business timeline event attached to one or more records.

Activity is optimized for user understanding; Audit is optimized for accountability and security evidence.

## Audit Event

A durable record of a sensitive, consequential, or security-relevant action including actor, action, target, time, context, and relevant metadata.

## API Client

A non-human integration identity authorized to use Re:Solve APIs through scoped credentials.

## MCP Client

An AI/agent client authorized to access approved Re:Solve MCP tools and resources under explicit scopes and audit rules.

## MCP Tool

A controlled Re:Solve operation exposed through Model Context Protocol.

## AI Provider

A provider used by Re:Solve's built-in AI system. It is independent of Chatwoot's AI configuration.

## AI Tool

A controlled operation the Re:Solve AI system may invoke, subject to permissions, policy, confirmation, and audit.

## Workspace

The top-level operational installation or tenant boundary when needed by the product model.

The first product deployment may operate as a single workspace. Multi-workspace SaaS behavior is not assumed as a core requirement unless later specified.

## Admin OS

The staff-facing Re:Solve experience.

## Client Portal

The client-facing Re:Solve experience.

## Product Bible

The canonical specification set defining Re:Solve product truth, behavior, flows, rules, states, acceptance criteria, and planned build slices.