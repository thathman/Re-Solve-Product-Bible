# Sales & Commercial

## Purpose
Sales & Commercial manages the journey from potential work to agreed commercial commitment while preserving context through Opportunity, Discovery, Proposal, Contract/Client Service, delivery, Billing and renewal.

## Canonical records
Lead, Opportunity, Pipeline, Stage, Service Catalogue Item, Service Package, Proposal, Proposal Revision/Decision, Contract, Commercial Approval, Price Book/Rate Card, Discount Rule, Tax Reference, Sales Activity, Cadence, Recurring Arrangement and Renewal Opportunity.

**Proposal is the only first-class commercial offer. Quote and Estimate are presentation styles/migration aliases, not separate product records or modules.**

Document rendering/version/delivery uses shared Document Studio.

## Principles
- never duplicate Organisation/Contact truth;
- preserve links across Opportunity -> Discovery/Form -> Proposal -> Contract/Service -> Project -> Billing/Renewal;
- accepted Proposal content gets an immutable Final Snapshot;
- sent Proposal revisions are versioned rather than silently edited;
- payment providers remain Connector implementations;
- client documents never expose internal notes/margin;
- no Timesheet/work-timer/Client Service Consumption dependency.

## Opportunity lifecycle
Suggested default: New -> Qualified -> Discovery -> Solutioning -> Proposal -> Negotiation -> Verbal Commit -> Won / Lost / Dormant.

Pipelines/stages may be configurable. Track expected close, stage age, probability, next action, loss reason, owner and related Organisations/Contacts/Properties/Services.

## Discovery
Discovery may use Notes, Activities, Files and the shared Forms engine. Project questionnaires/briefs can be sent before Portal activation using Secure External Access.

Ariya may summarize discovery responses, extract requirements and propose Service Catalogue items, Proposal structure, risks and next actions.

## Service Catalogue and pricing
Catalogue items may define:
- name/code/category/descriptions;
- pricing basis `flat`, `quantity`, or `duration`;
- default price/currency;
- quantity unit or duration unit/default duration;
- tax behavior;
- renewal/recurring eligibility;
- default Project/onboarding template;
- Support Entitlement and Property applicability.

Duration supports at least day, week, month, quarter and year. A duration-priced item is not automatically recurring.

Price Books/Rate Cards can provide Operating Entity, client-class or Organisation-specific prices with effective dates. Accepted historical prices remain stable.

Service Packages may bundle items or provide Proposal options such as Starter/Growth/Commerce while activation preserves clear underlying service relationships.

## Proposal — unified offer engine
A Proposal can present as:
- **Detailed Proposal** — narrative problem/solution/scope/deliverables/timeline/pricing/terms;
- **Quote-style Proposal** — concise commercial line-item offer;
- **Estimate-style Proposal** — indicative pricing presentation where uncertainty is explicit.

All styles share one record, numbering, lifecycle, revision history, acceptance evidence and downstream conversion.

### Proposal content
May include:
- title/cover/introduction/executive summary;
- scope/deliverables/exclusions/assumptions;
- timeline/milestones;
- services/packages/options;
- flat, quantity or duration line items;
- optional/add-on items;
- line/document fixed or percentage discounts;
- taxes;
- deposit/payment schedule;
- terms/validity;
- attachments;
- client comments/questions;
- acceptance/decline.

### Lifecycle
Suggested:
`Draft -> Internal Review/Ready -> Sent -> Viewed -> Negotiation/Revision -> Accepted / Declined / Expired / Withdrawn`.

`Viewed` is recorded only from real access/provider evidence and is not equivalent to acceptance.

Once sent, commercially meaningful edits create a new Proposal Revision. Acceptance/decline references the exact immutable revision the recipient saw.

### Acceptance evidence
Store recipient/User/Contact, exact revision snapshot, accepted/declined timestamp, secure-session/auth evidence, terms/version and Audit. Optional counterparty e-signature may be required by policy; authenticated acceptance can remain sufficient where configured.

Every final Proposal PDF is issuer-signed through Document Studio.

## Proposal downstream handoff
Proposal acceptance is the default commercial commitment gate and normally triggers the Portal invitation workflow for the accepting/selected Contact.

Depending on Proposal/template policy, acceptance may create/link idempotently:
- Contract;
- Project from a Project Template;
- Client Service;
- Recurring Arrangement;
- Invoice for full amount;
- percentage/fixed deposit Invoice;
- selected Proposal items;
- milestone/payment schedule;
- onboarding pack/journey.

Retries must not duplicate downstream records. The accepted Proposal remains linked as source truth.

## Contracts
Re:Solve owns Contract lifecycle, metadata, commercial relationships and immutable signed final snapshot. Counterparty signing may use a SignatureConnector.

Suggested states: Draft -> Review -> Ready for Signature -> Sent -> Partially Signed -> Executed -> Active -> Expired / Terminated / Superseded.

Every final Contract PDF includes issuer signature; executed Contracts additionally preserve required counterparty signature evidence.

## Recurring Arrangements
First-class commercial arrangements for hosting, maintenance, retainers and similar services define frequency, start/end/renewal, Catalogue lines, Properties, Contract, next billing date, pause/cancel and billing behavior.

Recurring Arrangement is distinct from one-time duration pricing and from external provider subscriptions.

## Deposits and payment schedules
Commercial terms may define deposit amount/percentage, milestone installments, scheduled payments, due offsets and Invoice-generation rules after acceptance/execution. Unusual schedules may require Commercial Approval.

## Commercial approvals
Use shared Approval for high discounts, nonstandard terms, write-offs, unusual payment schedules, high-value Proposals or sensitive services.

## Forms / public intake
Public/Portal Forms may create Lead/Request/Opportunity/Discovery flows with duplicate review and preserved Submission provenance. Forms do not create shadow Quote/Estimate records.

## Portal / Secure External Access
Before commitment, Proposal/Discovery can use narrow secure guest access. Proposal acceptance normally creates/invites Portal Membership. Manual earlier invitation remains allowed for legitimate workflows.

## Attention / Notifications
Examples: stale Opportunity, unanswered discovery, Proposal expiring, Proposal viewed but no response, contract signature waiting, recurring/renewal decision required.

## Ariya
Ariya may:
- summarize discovery/communication;
- recommend next action;
- draft Proposal narrative/scope/exclusions;
- suggest Catalogue items/packages based on authorised context;
- compare similar historical work without leaking client scope;
- flag unusual pricing/discounts;
- prepare follow-up/review requests;
- Watch stale Opportunities/expiring Proposals.

Draft/send/accept/financial actions follow normal Action Registry/Approval rules.

## Permissions
Canonical capabilities may include `sales.read`, `leads.manage`, `opportunities.manage`, `proposals.manage`, `proposals.send`, `contracts.manage`, `contracts.send`, `commercial.approve`, `services.manage`, `pricing.manage` and `renewals.manage`.

Do not introduce new `quotes.*` or `estimates.*` permissions except temporary migration compatibility.

## Acceptance criteria
- Proposal is the only current offer domain;
- detailed/quote-style/estimate-style presentations share one lifecycle;
- accepted content/pricing is immutable;
- duration pricing calculates explicitly and does not imply recurrence;
- discounts are explicit;
- downstream acceptance handoffs are idempotent;
- Portal invitation occurs at configured commitment gate;
- internal notes/margin never leak;
- every final Proposal/Contract PDF is signed;
- no Timesheet/work-timer/consumption dependency exists.

## Build slices
1. Opportunity/pipeline + Discovery/Forms relationships.
2. Service Catalogue + pricing basis + Price Books/packages.
3. Proposal unified data model + migration from historical Quote/Estimate truth.
4. Proposal builder/presentation/revisions + Secure External Access.
5. acceptance evidence + Portal invitation + idempotent handoff.
6. Contracts + signatures.
7. Recurring Arrangements + deposits/payment schedules + renewals/forecast/cadences.
