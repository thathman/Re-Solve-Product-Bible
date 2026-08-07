# Sales & Commercial

## Purpose
Sales & Commercial manages the journey from potential work to an agreed commercial commitment. It must preserve context from first opportunity through proposal, estimate, contract, service activation, project creation, and billing.

## Core records
Lead, Opportunity, Pipeline, Stage, Service, Service Package, Proposal, Estimate, Contract, Commercial Approval, Price Book Item, Discount Rule, Tax Rule Reference, Sales Activity, Renewal Opportunity.

## Principles
- never duplicate organisation/contact truth
- proposals, estimates, contracts, projects, subscriptions, and invoices remain linked
- pricing history is immutable after acceptance; later edits create versions
- payment providers are plugins/connectors, not hard-coded commercial logic
- client-visible documents must be versioned and auditable

## Opportunity lifecycle
New → Qualified → Discovery → Solutioning → Proposal → Negotiation → Verbal Commit → Won / Lost / Dormant.

Pipelines and stages are configurable. Stage changes can require fields or approvals.

## Opportunity workspace
Tabs:
- Overview
- Contacts
- Needs & Notes
- Activities
- Solution
- Proposal/Estimate
- Contract
- Files
- Timeline

Summary: value, probability, stage age, owner, expected close, source, client, related properties, service interests, next action, risks, latest activity.

## Services catalogue
Services are first-class commercial definitions used by sales, projects, billing, client portal, and reporting.

Fields: name, code, category, description, delivery model, pricing model, default price/currency, billing frequency, tax behavior, lead time, default project template, renewal behavior, support entitlement, client-facing description, active status.

Pricing models may include fixed, recurring, usage-based, milestone, hourly, custom quote, and bundled.

## Proposals
Proposal builder supports structured sections, reusable blocks, services, optional items, assumptions, exclusions, timeline, terms, expiration, attachments, versioning, internal notes, client comments, and acceptance.

States: Draft → Internal Review → Sent → Viewed → Negotiation → Accepted / Declined / Expired / Withdrawn.

No accepted proposal may be silently edited. Revisions create a new version.

## Estimates
Estimates are structured commercial calculations and can exist independently or inside proposals. They support line items, quantities, unit prices, discounts, taxes, optional items, validity dates, deposits, payment schedule, currency, notes, and conversion to invoice/project/service.

## Contracts
Re:Solve owns the contract record, lifecycle, commercial metadata, versions, linked proposal/service/project and signing status. Actual signing may be performed through a Signature Connector such as Documenso.

States: Draft → Review → Ready for Signature → Sent → Partially Signed → Executed → Active → Expired / Terminated / Superseded.

## Commercial approvals
Configurable approval policies for discounts, nonstandard terms, write-offs, unusual payment schedules, high-value proposals, or sensitive services.

## Renewals
Recurring services can generate renewal opportunities ahead of renewal date with owner, renewal value, risk, client decision, proposed changes, and notification schedule.

## Permissions
sales.read, leads.manage, opportunities.manage, proposals.manage, proposals.send, estimates.manage, discounts.apply, contracts.manage, contracts.send, commercial.approve, services.manage, pricing.manage, renewals.manage.

## Notifications
Examples: lead assigned, opportunity stale, stage SLA exceeded, proposal viewed, proposal expiring, client commented, proposal accepted/declined, contract requires signature, contract executed, renewal due, commercial approval requested/decided.

## Automations
- qualified lead → create opportunity
- proposal accepted → optionally create contract/project/service activation
- contract executed → activate service and billing schedule
- renewal window reached → create renewal opportunity
- opportunity inactive → reminder/escalation
- lost opportunity → require reason and optional nurture flow

## API/MCP
API exposes leads, opportunities, services, proposals, estimates, contracts, renewals, and activities with scoped write operations and immutable-version rules.

MCP candidates: search_opportunities, get_opportunity, list_stale_opportunities, draft_proposal_outline, get_service_catalogue, get_contract_status, list_upcoming_renewals. Sending/accepting/signing commercial documents requires confirmation and stronger permissions.

## PWA/mobile
Mobile focuses on pipeline review, opportunity details, activity capture, proposal status, approvals, renewal actions, and quick contact. Full proposal authoring may optimize for larger screens but remains readable and reviewable on mobile.

## Acceptance criteria
- accepted commercial documents remain immutable
- conversion to project/billing preserves source links
- discounts requiring approval cannot bypass policy
- client-facing documents never expose internal margin/notes unless explicitly configured
- all send/view/accept/decline/signature events are auditable

## Lovable build slices
1. pipeline + opportunity workspace
2. service catalogue
3. estimates + proposal versions
4. contracts + signature connector states
5. approvals + renewals + automation
