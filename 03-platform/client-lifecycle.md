# Client Lifecycle

## Purpose
Client Lifecycle is the cross-domain operating flow that turns a commercial relationship into an active, supportable client and eventually renews/closes/transfers that relationship safely.

It orchestrates existing records rather than creating second copies of them.

## Lifecycle stages
Suggested vocabulary:
- Prospect;
- Qualified;
- Commercial Review;
- Won / Preparing Onboarding;
- Onboarding;
- Active;
- At Risk;
- Paused/Suspended where applicable;
- Renewal / Offboarding;
- Former/Archived.

Organisation lifecycle state may remain configurable, but transitions have explicit operational consequences.

## Commercial commitment / Portal activation
Default commitment gate is Proposal acceptance.

At/after acceptance Re:Solve may idempotently:
- invite the accepting/selected Contact to Portal Membership;
- instantiate the configured Client Journey/onboarding pack;
- create/link Contract;
- create deposit/payment schedule;
- instantiate Project Template;
- create/link Client Service/Recurring Arrangement;
- start approved onboarding Automations.

Pre-commitment Forms/Proposal interactions may use Secure External Access without forcing Portal account creation.

## Client Journey / onboarding pack
The canonical reusable orchestration contract is [Client Journeys and Onboarding Packs](client-journeys.md).

A Journey gives staff/client one coherent progress view while its steps continue to reference authoritative Contract, Invoice, Form Request, File Request, Booking, Approval, Task, Project, Property and Request records.

A Journey does not create a separate onboarding task/work engine.

## Onboarding
An onboarding Journey/plan may coordinate:
- Organisation/profile completion;
- Contacts/roles;
- Account Team assignment;
- accepted Proposal/Contract;
- Client Service/Recurring Arrangement activation;
- billing profile/payment terms/deposit;
- Properties/domain/hosting/platform inventory;
- credential/Vault requests;
- Connector setup/mappings;
- Portal Membership/access;
- Chatwoot support mapping;
- Support Entitlement;
- Monitoring/Property Health setup;
- Project creation from Template;
- Form Requests/questionnaires;
- required Files/File Requests;
- client Approvals/Actions;
- Knowledge/runbook setup;
- communication preferences;
- handoff to steady-state operations.

## Onboarding state
Show:
- Journey progress;
- blockers;
- client actions;
- internal Tasks;
- access/credential readiness;
- Property readiness;
- Billing readiness;
- Support readiness;
- Monitoring readiness;
- next Milestone/action;
- responsible owner.

Attention surfaces blocked/stale onboarding. Ariya can explain why a step is blocked from source evidence.

## Account Team
An Organisation may have named operational responsibilities such as Account Owner, Delivery/Project Owner, Technical Owner, Finance Owner or Support/Relationship Owner. These are business responsibilities, not HR job records.

## Relationship reviews
Active clients may have periodic account-review records capturing:
- Services/Recurring Arrangements;
- Project state;
- Property Health;
- Support/Incidents;
- Renewals;
- receivables;
- risks;
- Opportunities;
- decisions/actions;
- review/feedback state where useful.

A review can generate Tasks, Requests, Opportunities, Review Requests or Knowledge updates.

## Renewal
Renewal may instantiate a Renewal Journey linking:
- renewal/expiry obligation;
- client decision;
- updated Proposal;
- Contract amendment/new Contract;
- Billing/payment;
- Property/provider action;
- continuation/suspension/end;
- verification;
- follow-up Review Request where appropriate.

## Project handover / closure
Completed Projects may instantiate a handover Journey with:
- final Deliverable/Approval;
- final Invoice/balance;
- handover pack/document;
- File/credential transfer;
- client training/meeting;
- outstanding Client Actions;
- Project completion confirmation;
- Review Request;
- ongoing Service/Support activation.

## Offboarding
Offboarding is explicit and safe.

Potential Journey/checklist:
- confirm effective end date;
- close/cancel future service billing;
- settle/credit outstanding Invoices as approved;
- complete/close Projects;
- export/hand over client Files;
- transfer credentials/domains/hosting where contractually required;
- review/revoke Vault access/shares;
- revoke Portal Membership/access;
- disconnect/remap Connectors;
- stop/transfer Monitoring;
- close/transfer Chatwoot support mappings;
- archive relevant Properties/Services;
- provide final signed documents/statements;
- preserve Audit/commercial history;
- apply retention/Trash/Purge policy.

Offboarding never automatically deletes history.

## Dependency/Impact Inspector
Before deactivation/offboarding/archive, inspect remaining dependencies such as open Projects, active Services, unpaid Billing, Portal access, Monitoring, Renewals, Connectors, Approvals and assigned responsibilities.

The lifecycle flow should suggest safe reassignment/archive alternatives instead of blind deletion.

## Reassignment
When a responsible staff User becomes unavailable/deactivated, lifecycle ownership must be reassignable using the shared Dependency Inspector/Tasks/Access model without HR functionality.

## Template Center
Onboarding/Renewal/Handover/Offboarding Journey Templates are discoverable/governed through Template Center while Client Journey remains the owning domain.

## Test / simulation
Proposal-acceptance/client-lifecycle workflows should support dry-run simulation showing the Journey/Portal invite/Contract/Invoice/Project/Service actions that **would** happen, including blockers/idempotency, without creating real records.

## Notifications / Attention / Tasks
Examples:
- onboarding blocked;
- client action overdue;
- required credential missing;
- support/monitoring not ready before go-live;
- renewal/offboarding step overdue;
- access still active after offboarding date.

Assigned staff actions appear in Tasks; persistent conditions create Attention.

## Automations
Examples:
- Proposal accepted -> invite Portal + instantiate onboarding Journey;
- Contract executed -> reveal/activate next steps;
- deposit verified -> advance onboarding;
- Service activated -> request required Property info;
- onboarding blockers cleared -> mark Organisation Active;
- Project completed -> instantiate handover/review Journey;
- offboarding started -> create access/dependency review.

Automations create/advance real steps but cannot bypass permissions/Approvals/source truth.

## Portal
Portal presents only client-relevant Journey actions/progress, uploads, signatures, payments, Approvals and status. Internal transition complexity/cost/risk remains hidden.

## Ariya
Ariya may summarize lifecycle/Journey blockers, explain next action, draft reminders, recommend a Journey Template and Watch overdue dependencies. It cannot revoke/transfer critical assets or mark source steps complete without registered Actions/evidence.

## Acceptance criteria
- commercial commitment connects Portal activation and onboarding coherently;
- Journey orchestrates native domain records rather than duplicating them;
- onboarding/renewal/handover/offboarding reuse one model;
- offboarding revokes/handovers access deliberately;
- operational history is retained according to policy;
- dry run can explain lifecycle consequences before activation;
- client/internal views expose different appropriate detail;
- no HR/timesheet/work-timer dependency is introduced.
