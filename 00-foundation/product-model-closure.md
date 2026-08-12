# Re:Solve Product Model Closure Decisions

## Status
**Canonical closure of the 2026-08 product-model review.**

These decisions complete the current broad feature-discovery/brainstorming pass. They supplement `canonical-expansion-decisions.md` and must be included when the remaining implementation phases are rebuilt.

Implementation remains frozen until the revised phase roadmap/atomic ledgers are produced.

## 1. Universal Template Center
Re:Solve has one cross-domain Template Center for discovery/governance of reusable templates while each source domain remains authoritative.

Initial families include Proposal, Contract/document, Billing document, Project, Task blueprint where useful, Form, Email, Review Request, Client Journey, Automation recipe and Report templates.

Template Center must support versioning, Draft/Published/Archived state, scope/defaults, preview/test, duplicate, search/filter and **Where used?** dependency visibility.

Historical/in-flight usage remains bound to the exact Template Version.

Canonical spec: `03-platform/template-center.md`.

## 2. Client Journeys / Onboarding Packs
Client Journey is a first-class orchestration/progress layer for onboarding, Service activation, Project kickoff/handover, renewal and offboarding.

A Journey references authoritative records such as Contract, Invoice, Form Request, File Request, Booking, Approval, Task, Request and Project. It never creates a duplicate work/commercial engine.

Proposal acceptance can idempotently create Portal Invitation + onboarding Journey according to configured policy.

Canonical spec: `03-platform/client-journeys.md`.

## 3. Project Financial Plan / Commercial Health
Projects support an agency-appropriate Financial Plan using real commercial and explicit cost inputs:
- accepted Proposal/Contract value;
- approved Change Request value;
- Invoiced/Paid/Outstanding/Remaining-to-invoice;
- approved external/operational cost budget;
- Project-linked Expenses/costs;
- expected/current gross margin where currency/input basis is valid.

No labor cost from Timesheets/work timers/utilization exists. Re:Solve does not become a full accounting ledger.

Canonical spec: `01-admin/project-financials.md`.

## 4. Reusable Approval Policies
Approval becomes policy-driven and versioned, supporting:
- single approver;
- any-one;
- everyone/all-of;
- sequential steps;
- parallel steps;
- conditional thresholds/routing.

Examples include discount thresholds, Expenses, nonstandard Contract terms, Refund/Credit/Adjustment, Project Change Requests and high-risk Connector/Automation Actions.

Pending Approval Requests remain tied to the exact Policy Version/evidence they started with.

Canonical spec: `03-platform/approvals.md`.

## 5. Archive -> Trash -> Restore -> Purge
Supported record types use a deliberate lifecycle:
`Active -> Archived -> Trash -> Restore or Pending Purge -> Purged`, subject to domain/retention rules.

Financial/Audit/executed/signed/legal records may never be ordinary purgeable Trash.

A permission-aware Recycle Bin exposes Restore and purge eligibility/retention state.

Canonical spec: `03-platform/reference-numbering-and-record-lifecycle.md`.

## 6. Dependency / Impact Inspector
Before destructive/high-impact Actions, Re:Solve explains what depends on the target and whether the action is blocked, requires reassignment, has warnings or has a safer Archive alternative.

Important targets include Organisation, Staff/User, Property, Service Catalogue Item, Template, Connector and other high-connectivity records.

Impact details/counts remain permission-scoped.

Canonical specs: `03-platform/action-registry.md` and `03-platform/reference-numbering-and-record-lifecycle.md`.

## 7. Test / Preview / Dry-Run Framework
Re:Solve has a shared no-side-effect Test/Dry-Run contract for risky configuration and workflow behavior.

Priority integrations:
- Automation;
- Ariya inbound-email classification/routing;
- late-fee/Adjustment policy;
- Proposal acceptance handoff;
- Approval Policy routing;
- Bulk Actions;
- Connectors/webhooks;
- Template/domain previews.

Dry Run must never be represented as real execution.

Canonical spec: `03-platform/testing-and-simulation.md`.

## 8. Universal permission-aware Bulk Actions
Appropriate lists/directories can expose registered bulk Actions such as assign, tag, archive, send Form Request, create Tasks, export, add to Cadence or create Review Requests.

Bulk capability is explicit per Action. Per-record authorization/eligibility is re-evaluated. High-impact actions require preview/impact review or are not bulk-capable.

Financial/security/legal actions do not become casual bulk operations simply because rows are selectable.

Canonical spec: `03-platform/action-registry.md`.

## 9. Portal Service Requests -> Opportunity -> Proposal
Portal provides a client-readable `Request Something`/Services experience for new or additional work.

When a request is commercial/new paid scope, the canonical flow is:
`Service Request -> Opportunity -> Discovery/Form if needed -> Proposal`.

A client request does not directly create an Invoice or Project merely because a Service Catalogue item exists.

This prevents commercial requests from becoming Support tickets and keeps the sales spine intact.

Canonical spec: `03-platform/requests.md`.

## Boundaries reaffirmed
The closure pass does **not** add:
- HR/payroll/recruitment/leave/attendance/performance management;
- Timesheets/Time Tracking/work timers;
- employee utilization/resource planning based on hours;
- Client Service consumption/credit-hour metering;
- full accounting/general ledger;
- inventory/warehouse/manufacturing/POS;
- native live-chat duplication of Chatwoot;
- marketing campaign suite;
- CMS in the current run.

## Feature-discovery freeze
After this closure, ordinary phase planning should **stop broad competitor-feature hunting**.

New features discovered during implementation are handled through the Product Oversight process and must satisfy at least one of:
- required to complete an already-defined workflow correctly;
- required for security/data integrity/compliance/portability;
- clearly removes a major operational gap revealed by real use/testing;
- explicitly requested/approved by the owner.

Do not reopen horizontal feature expansion merely because another ERP has another module.

## Next product-planning action
Rebuild the remaining Re:Solve phases from the complete Product Bible, then present the **full expanded atomic ledger of the next phase before implementation resumes**, per `10-build/phase-execution-protocol.md`.
