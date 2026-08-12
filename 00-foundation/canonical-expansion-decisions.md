# Re:Solve Canonical Expansion Decisions

## Purpose
This document records cross-cutting product decisions that override ambiguous or older wording elsewhere in the Product Bible. Existing specs must be interpreted consistently with these rules and updated as they are touched.

## Product scope exclusions
Re:Solve is not an HR system and does not include employee HR records, payroll, leave/absence management, recruitment, performance reviews, attendance, workforce HR administration, Timesheets/Time Tracking, work timers, or Client Service Consumption/remaining-hours/credit metering.

Projects may still have dates, estimates, deadlines, owners, assignees, milestones, effort notes and delivery status. Services may have scope, SLA, price, billing cadence, duration, renewal, included Properties and contractual terms.

A headless/public-site CMS is a **distant-future expansion only**. It is explicitly outside the current product run and must not create current schemas, routes, phase dependencies or implementation work.

## Workspace and Operating Entities
Every installation has one canonical Workspace even when multi-workspace SaaS behavior is not enabled.

An Operating Entity is the business/legal/brand identity using Re:Solve to deliver services. Airix Media is an Operating Entity in the first deployment; it is not modeled as an ordinary client Organisation.

A Workspace may eventually contain multiple Operating Entities/Brands while still remaining one installation.

## Identity and Portal commitment gate
`Principal` is the general authorization actor. Principals may include Human User, Service Account, API Client, MCP Client, Plugin and Connector.

`User` means an authenticated human identity. Contact remains a business person record and does not itself grant Portal access.

Permissions and access grants target Principals and are always combined with scope.

The default Client Portal account/invitation trigger is **commercial commitment, normally Proposal acceptance**. Lead, Contact, Organisation and Opportunity creation do not automatically create Portal users.

Before commitment, Discovery Forms, Proposals and other narrow actions use Secure External Access/guest links where appropriate. A staff user may manually invite a client earlier when a real workflow requires it.

Portal Membership lifecycle is conceptually `none -> invited -> active -> suspended -> revoked`. Suspended/revoked Membership grants no data authority.

## Permission naming
Canonical permission grammar is `domain.action` when no meaningful sub-resource exists, or `domain.resource.action` when it does.

## Canonical staff work surface: Tasks
The staff execution surface is called **Tasks**, not `My Work`.

Tasks is the universal human-work queue and may project/relate authoritative work from Tasks, Approvals, Requests, Reminders, Renewals, Incidents, Mentions, onboarding steps, commercial follow-up and plugin work providers without creating shadow business truth.

Saved views such as `Assigned to me`, `Today`, `Overdue`, `Waiting on client`, `Property health` or `Ariya-created` are views of Tasks, not separate root modules.

## Canonical commercial offer: Proposal
**Proposal is the single commercial-offer domain. Quote and Estimate are not separate first-class product records.**

A Proposal may use presentation styles such as:
- detailed/narrative proposal;
- quote-style commercial offer;
- estimate-style indicative offer.

All use one lifecycle, revision model, acceptance evidence, numbering and downstream handoff. Existing Quote/Estimate implementation or historical data may be migrated/aliased into Proposal, but new product truth must not recreate parallel Quote/Estimate domains.

The commercial spine is:
`Lead -> Organisation/Contact -> Opportunity -> Discovery/Form -> Proposal -> Acceptance -> Portal Invitation -> Contract/Onboarding -> Project/Delivery -> Invoice/Adjustments -> Payment -> Renewal/Review`.

Proposal acceptance may create or trigger a Contract, Project, Invoice/deposit/payment schedule, Client Service or Recurring Arrangement according to configured workflow. Handoffs are idempotent and auditable.

## Service Catalogue pricing basis
A Service Catalogue item and a Proposal/Invoice line may use an explicit pricing basis:
- **flat** — fixed price;
- **quantity** — quantity × unit price;
- **duration** — duration × rate.

Duration supports at least day, week, month, quarter and year. Examples include hosting for 12 months and a domain for 2 years.

A duration-priced line is not automatically recurring. Renewal/Recurring Arrangement is a separate commercial decision.

Service packages/options, Price Books/Rate Cards, client-specific agreed prices and optional/add-on items are supported commercial concepts while accepted historical pricing remains immutable.

## Discounts, fees and financial adjustments
Proposal and Invoice pricing may support line-level and document-level fixed/percentage discounts where policy allows.

Payment is evidence of money received and must not be mutated to represent a fee or penalty.

Late fees, penalties, service charges, credits, write-offs, refund adjustments and similar changes to amount due are represented as controlled **Commercial/Invoice Adjustments** or appropriate Credit Note/Refund records with reason, source, actor, timestamp and audit evidence.

Late-fee policies may generate append-only adjustments after a configured grace period. Invoice balance remains derived from authoritative lines, taxes, adjustments, credits and Payment allocations.

## Forms as a platform primitive
Forms is one reusable engine for discovery, Project questionnaires, creative briefs, onboarding, surveys, feedback, review requests, lead/proposal intake, Client/Service/Support Requests, internal operational forms and future plugin use.

Canonical concepts are:
- Form Template/Version;
- Form Request/Assignment — a specific recipient/context/deadline/expiry;
- Submission — immutable submitted answers plus Files;
- Mapping/Routing/Automation — deliberate transformation into authoritative domain records.

Forms support public, Secure External Access, Portal and internal modes, conditional logic, sections/pages, file uploads, versioning, validation and mobile-first completion.

Ariya may summarize a permitted Submission, extract requirements and propose Tasks/Milestones/Project setup. Resulting writes still use normal validation, Action Registry and permissions.

## Communications and email
Communications is a first-class cross-domain capability, not only transactional email delivery.

It includes provider-neutral Connected Mailboxes/Shared Inbox, outbound email, inbound email ingestion, threading via real message identifiers, business-record linking, delivery evidence, review requests, operational announcements and other configured channels.

Email rendering is composable:
`Universal head/styles -> Operating Entity/Brand header -> template/body -> Staff personal HTML signature OR Operating Entity/system signature -> footer/legal content`.

Staff personal HTML email signatures are configured in their own profile and remain separate from Workspace/Operating Entity signature/branding.

Inbound messages may be classified by Ariya using sender identity, Organisation, Property, Project, open Support context, intent, urgency, dates, attachments and requested actions. High-confidence routing may create/attach authoritative Support/CRM/Billing/Project work only when an explicit policy permits it. Uncertain mail goes to Inbox Triage. Email text alone never establishes Payment truth.

Review Requests may be triggered from Project completion, resolved Support, full Payment or manual/automated policy and may target Google, Facebook, Clutch, Trustpilot or a custom destination. Completion is recorded only when there is real evidence.

## Portal live chat and Chatwoot
The canonical Portal live-chat path is:
`Client Portal -> Ariya -> Chatwoot -> Ariya -> Client`.

Chatwoot is the conversation transport/human-support surface. Ariya is the Re:Solve intelligence layer. Re:Solve must not build a duplicate native live-chat console.

Ariya identifies the Portal user and authorised Organisation/Property/Project/Billing/Support context, can answer within Portal scope, can create/attach Support work through controlled actions, and can hand off to a human through Chatwoot. Client-facing Ariya never exposes staff-only notes, other clients, internal financials/security detail or Vault secrets.

Chatwoot Captain remains separate from Ariya and does not power Ariya.

## Ariya is the intelligence fabric
The user-facing name of Re:Solve's built-in AI is **Ariya (Àríyá)**. Internal technical concepts may use names such as `AIProvider`, `AIRun`, `AIProfile`, `AIConnector` and `AITool`.

Ariya is not a bolt-on module. It is the intelligence fabric across every authorised domain and surface.

Canonical operating modes:
- **Ask** — explain/search permitted Re:Solve truth;
- **Draft** — create proposed content/work;
- **Act** — execute a registered authorised action;
- **Watch** — continuously observe a condition and react through policy/Automation;
- **Investigate** — correlate evidence across domains and explain likely causes;
- **Recommend** — proactively surface useful next actions.

Ariya may know everything the caller is authorised to know, but never expands authority. Every material claim should expose source/evidence/freshness when useful. Every consequential mutation routes through permission checks, Action Registry, confirmation/Approval policy and Audit.

Ariya monitors Property Health/Posture, Communications, Projects, Tasks, Support, Billing, Forms, renewals, system health and other authorised domains. It can use protected capability handles where designed, but generic AI retrieval must not reveal raw Vault secrets.

## Native Monitoring and Property Health
Re:Solve owns a native Monitoring Engine and Property Health/Posture model. External systems such as Cloudflare, Uptime Kuma and hosting/monitoring vendors are optional Connector signal sources.

Monitoring grows from HTTP/HTTPS, latency, redirects, certificate/domain expiry into DNS, TCP, keyword/JSON/API checks, heartbeat, backup freshness, application/OJS/WordPress/hosting signals and independent probe workers.

A Health/Operational Incident is a real record with evidence, start/recovery and affected Properties. Ariya may Watch, correlate, investigate and propose/create Tasks, Incidents or Support work according to policy. Client-safe status and optional status pages may expose only approved evidence.

## Documents, PDFs and signatures
Document Studio is mandatory shared infrastructure.

**Every issued/final Re:Solve-generated PDF is signed.** This includes Proposals, Contracts, Invoices, Receipts, Credit Notes, Account Statements, renewal documents, formal Project/Service/Incident reports, handover packs and other official generated PDFs.

Draft previews may be watermarked `DRAFT` and may remain unsigned.

Every final PDF stores an immutable exact snapshot including:
- document/business-record reference and version;
- template version and Operating Entity/Brand identity;
- issuer/signatory identity and title;
- signature snapshot used at issue time;
- issued timestamp;
- document hash (for example SHA-256);
- verification code/reference;
- delivery/acceptance/signature evidence as applicable.

Staff have a separate personal **Document/PDF Signature** configuration from their HTML email signature. Operating Entities define default signatory rules by document family (named staff, issuing staff, record owner, or entity-authorised signature where allowed).

Invoices and Receipts require issuer signature; they do not normally require client signature. Contracts and other agreement/approval documents may additionally require counterparty e-signatures. Counterparty signing may use a SignatureConnector, while issuer signing must not depend on a third-party signing provider.

Later template/brand/staff-signature changes must never rewrite historical signed PDFs. Public verification may confirm safe metadata and hash validity without exposing confidential document contents.

Certificate/X.509 cryptographic PDF signing is an optional advanced layer; the initial product contract is visible authorised signature + immutable PDF + hash + verification evidence + Audit.

## Files and Secure Vault
A protected confidential document is a Vault Item, not simultaneously an ordinary File record with a second access path. Files and Vault Items may share provider-neutral storage while retaining separate identities and permissions.

## First-run setup and installation
First-time setup/installation is a first-class product capability, not only deployment documentation.

Setup Mode must verify system/runtime/environment, database/Supabase/migrations, storage, public URL/HTTPS, workers/jobs/health, bootstrap the first Owner securely, configure Workspace and Operating Entity identity, commercial defaults/numbering, email, storage/backups, optional integrations/imports and finish with a readiness verification.

After successful setup the installer is **locked**. `/setup` must never silently bootstrap another owner after lock. Ongoing diagnostics move to System Operations/Health.

## Admin and Client Portal experience reset
The current Admin and Portal functional shells are **not final visual/experience authority**. A dedicated experience architecture and redesign pass is required before product completion.

Admin should be clean, record-centric and task-oriented with shallow navigation, universal search/Quick Create/Saved Views, contextual Ariya, configurable dashboards/module visibility and significantly less card/border clutter.

Client Portal should not mirror Admin. It should prioritize `Needs Your Attention`, active Projects, Billing, Support, Files and client actions with a much calmer client-specific information hierarchy. Staff must have a safe read-only `Preview as Client` capability.

## Plugins and connectors
A Plugin adds Re:Solve business/product capability. A Connector integrates an external system. Business domains depend on provider-neutral capabilities rather than provider names.

## Core UI Component Framework
The Re:Solve Core UI Component Framework remains mandatory. External component sources are normalized into Re:Solve-owned tokens/components rather than library soup.

## Attention, Notifications, Activity and Audit
Notification records that something happened and may be delivered. Attention represents a condition that still deserves awareness/action. Activity is user-readable narrative. Security/accountability Audit is append-only evidence. They must not be conflated.

## Data authority
Synced, derived, imported and AI-produced information exposes source/authority/freshness where material. Connector synchronization declares ownership direction and conflict policy rather than silently overwriting records.

## Phase execution governance
Before any development phase begins, its complete atomic numbered task ledger must be expanded and presented to the owner. Every completion/checkpoint report must show the current phase's full task status, including all pending and deliberately deferred items. Broad roadmap Steps must never substitute for the phase ledger.
