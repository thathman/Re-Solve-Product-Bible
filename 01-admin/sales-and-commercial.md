# Sales & Commercial

## Purpose
Sales & Commercial manages the journey from potential work to an agreed commercial commitment while preserving context through proposal, estimate, contract, service activation, project delivery, billing and renewal.

## Core records
Lead, Opportunity, Pipeline, Stage, Service Catalogue Item, Service Package, Proposal, Estimate/Quote, Contract, Commercial Approval, Price Book Item, Discount Rule, Tax Reference, Sales Activity, Cadence and Renewal Opportunity.

Document rendering/version/delivery uses shared Document Studio.

## Principles
- never duplicate Organisation/Contact truth;
- preserve links across Opportunity -> Proposal/Estimate -> Contract -> Client Service -> Project -> Billing/Renewal;
- accepted commercial content gets an immutable Final Snapshot;
- pricing history is versioned after acceptance;
- payment providers remain Connector implementations;
- client documents never expose internal notes/margin by accident;
- no Client Service Consumption/usage-credit metering;
- no Timesheet dependency.

## Lead conversion
A Lead may exist before a complete Organisation is known. Qualification should search/link/create Organisation and Contact deliberately with duplicate review rather than blindly create records.

## Opportunity lifecycle
New -> Qualified -> Discovery -> Solutioning -> Proposal -> Negotiation -> Verbal Commit -> Won / Lost / Dormant.

Pipelines/stages are configurable. Stage changes may require fields/approvals. Track expected close, stage age, probability, next action, loss reason and owner.

## Opportunity workspace
Tabs:
- Overview
- Contacts
- Needs & Notes
- Activities / Cadence
- Solution
- Proposal / Estimate
- Contract
- Files
- Collaboration / Activity

Summary: value, probability, expected close, stage age, source, client, properties/service interests, next action, risks and latest activity.

## Service Catalogue
Fields may include name, code, category, description, delivery model, pricing model, default price/currency, billing frequency, tax behavior, lead time, default Project template, renewal behavior, Support Entitlement, Property applicability, client-facing description and active state.

Core pricing models may include:
- fixed one-time;
- recurring fixed;
- milestone/installment;
- package/bundle;
- custom quote.

Manual quantity/unit-price lines can still exist in Estimates/Invoices, but Re:Solve does not require automated usage metering or Timesheet-derived hourly billing.

## Price lists / client pricing
Support reusable price-book items, client-specific agreed prices, packages and effective dates where needed. Historical accepted prices remain stable.

## Proposals
Proposal is a first-class commercial record rendered/delivered through Document Studio.

Builder/content may support:
- reusable template/sections;
- services/packages;
- pricing table;
- optional/add-on items;
- recurring + one-time charges;
- assumptions/exclusions;
- timeline/milestones;
- terms;
- attachments;
- client comments/questions;
- versions;
- expiration;
- Secure External Access/Portal delivery;
- accept/decline.

States: Draft -> Internal Review -> Sent -> Viewed -> Negotiation -> Accepted / Declined / Expired / Withdrawn.

Accepted content receives immutable Final Snapshot.

Àríyá may draft proposal scope/narrative from authorized context. User review remains required before send.

## Estimates / Quotes
Structured priced offers supporting line items, quantity/unit price, discounts, taxes, optional items, validity, deposit, payment schedule, currency and conversion workflow.

An Estimate may be standalone or referenced by a Proposal.

## Contracts
Re:Solve owns Contract lifecycle/metadata/commercial relationship and Final Snapshot. Actual signing uses a SignatureConnector such as Documenso.

States: Draft -> Review -> Ready for Signature -> Sent -> Partially Signed -> Executed -> Active -> Expired / Terminated / Superseded.

## Document Studio
Document Studio owns templates, rendering, versions, web/PDF output, branded Secure External Access and delivery evidence. It does not replace Proposal/Estimate/Contract business records.

## Deposits / payment schedules
Commercial terms may define:
- deposit amount/percentage;
- milestone installments;
- scheduled payments;
- due offsets;
- invoice-generation rules after acceptance/execution.

Unusual schedules may require Commercial Approval.

## Commercial approvals
Use shared Approval for high discounts, nonstandard terms, write-offs, unusual payment schedules, high-value proposals or sensitive services.

## Cadences / reminders
Sales follow-up can use shared Cadence/Reminder primitives for lead/opportunity/proposal follow-up without building a separate workflow engine.

## Forecasting and goals
Sales can provide weighted Pipeline forecast using expected close/value/stage probability and business-goal comparison. Assumptions remain visible.

## Renewals
Client Services/Contracts may generate Renewal Opportunities ahead of renewal with owner, value, risk, client decision and proposed changes.

Property expiry obligations belong to Renewal Desk but may create commercial Opportunities when paid work/renewal is required.

## Requests / public intake
Public/Portal Forms may create quote/service Requests that triage into Leads/Opportunities/Estimates according to routing and duplicate rules.

## Permissions
Canonical capabilities may include sales.read, leads.manage, opportunities.manage, proposals.manage, proposals.send, estimates.manage, contracts.manage, contracts.send, commercial.approve, services.manage, pricing.manage and renewals.manage.

## Attention / Notifications
Attention examples: stale Opportunity, expiring Proposal, contract signature waiting, Renewal Opportunity with no action.

Notifications include assignment, approval, proposal delivery/view where policy permits, expiry, comment, accept/decline, signature/execution and renewal events.

## Automations
- qualified Lead -> Opportunity;
- Proposal accepted -> approved Contract/Service/Project path;
- Contract executed -> activate Service/billing workflow;
- renewal window -> Renewal Opportunity;
- inactive Opportunity -> Reminder/Attention;
- lost Opportunity -> require reason/optional cadence stop.

## API / MCP / Àríyá
Expose scoped commercial resources/actions with version/final-snapshot rules.

MCP candidates: search_opportunities, get_opportunity, list_stale_opportunities, draft_proposal_outline, get_service_catalogue, get_contract_status and list_upcoming_renewals.

Sending/accepting/signing/financially consequential changes use Action Registry and stronger confirmation/approval.

## PWA/mobile
Mobile supports pipeline review, opportunity detail, follow-up, proposal/contract review/status, approvals and renewal actions. Deep document authoring may optimize for larger screens while rendered documents remain excellent on phone.

## Acceptance criteria
- accepted/executed commercial content is immutable;
- conversions preserve source links;
- discounts/schedules cannot bypass Approval policy;
- internal notes/margin never leak to clients;
- all material send/view/accept/decline/signature events are traceable;
- Document Studio is shared rather than custom per document type;
- no Timesheet or Client Service Consumption dependency exists.

## Lovable build slices
1. Pipeline + Opportunity workspace.
2. Service Catalogue + pricing.
3. Document Studio template foundation + Estimates.
4. Proposals + Secure External Access/acceptance.
5. Contracts + SignatureConnector states.
6. Approvals + deposits/payment schedules + renewals + forecast/cadences.
