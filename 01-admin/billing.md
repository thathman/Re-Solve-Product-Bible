# Billing & Finance Operations

## Purpose
Billing converts commercial commitments into Invoices, Payments, Receipts, Credits, Adjustments, Refunds, recurring charges and operational financial visibility without hard-coding a payment provider or becoming a full statutory accounting/ERP suite.

## Core records
Invoice, Invoice Item, Invoice/Commercial Adjustment, Payment, Payment Allocation, Receipt, Credit Note, Refund, Billing Schedule, Provider Subscription Mapping, Payment Schedule, Deposit Requirement, Payment Method Reference, Reconciliation Record, Tax Snapshot, Currency Snapshot, Dunning Event, Account Statement Reference and Credit-Control Action.

## Principles
- financial records preserve immutable history where financially consequential;
- Payment is evidence of money received, not a container for penalties/discounts;
- provider callbacks/events do not establish truth without verification;
- payment capability is provider-neutral through PaymentConnector implementations;
- amounts use precise integer minor-unit representation;
- unlike currencies are never silently aggregated;
- material writes are audited;
- generated final Billing PDFs are signed through Document Studio;
- Billing does not depend on Timesheets/Time Tracking/work timers/Client Service Consumption.

## Navigation
`Overview | Invoices | Payments | Receipts | Credit Notes & Adjustments | Recurring | Reconciliation | Statements / Credit Control`

Refunds, deposits and advanced actions can live contextually rather than bloating top-level navigation.

## Invoices
Fields may include human reference/number, Operating Entity, Organisation, Billing Contact, currency, issue/due dates, status, lines, tax snapshot, discounts, adjustments, subtotal/total, paid/balance, payment terms, linked Contract/Proposal/Project/Client Service, notes/client memo, signed Document Studio snapshot and delivery history.

Suggested lifecycle: Draft -> Approved -> Issued -> Partially Paid -> Paid, plus Overdue, Void and Written Off where permitted.

Issued Invoices are not edited in place when financial meaning changes. Use controlled Adjustment, Credit Note, void/reissue or approved correction rules.

## Invoice line pricing
An Invoice line may preserve pricing semantics from its Proposal/Service source:
- flat amount;
- quantity × unit price;
- duration × rate.

Duration units support at least day, week, month, quarter and year. Calculations remain database/server authoritative and precise.

## Discounts
Discounts can be explicit line-level or Invoice-level fixed/percentage values where allowed. The reason/source may be required by policy and material discounts may require Approval.

Discounts must remain visible financial inputs; do not hide them inside Payment or tax calculations.

## Commercial / Invoice Adjustments
Adjustments represent amount-due changes that are not Payments.

Potential types:
- late fee;
- penalty;
- service charge;
- approved discount correction;
- write-off;
- credit application;
- refund adjustment;
- other approved fee/correction.

Adjustment evidence includes Invoice, type, fixed/percentage/calculation basis, amount/currency, reason, source/policy, actor, timestamp, approval where required, reversal/supersession link where applicable and Audit.

Historical Adjustments are corrected with new compensating evidence rather than silent destructive edits.

## Late-fee / penalty policy
Settings may define policies such as:
- grace period;
- fixed or percentage fee;
- once versus permitted recurrence;
- maximum/cap;
- eligible Invoice states/types;
- client-safe notice text;
- approval/waiver rules.

When a policy fires, it creates a real Adjustment. It does not mutate the original Payment or fabricate a Payment.

## Authoritative balance
Invoice amount due/balance derives from authoritative lines, taxes, explicit discounts, Adjustments/Credit Notes and effective Payment allocations. It is not independently editable shadow truth.

## Payments
Payments may originate from verified provider events, approved manual bank/cash/offline recording, reconciliation import or another approved source.

Fields include provider/Connector Instance, external reference, payer, amount/currency, received/verified timestamps, status, allocations, provider fees where known, evidence, reconciliation state, source/provenance and correlation.

Suggested states include Pending, Verified, Partially Allocated, Allocated, Failed, Reversed and Refunded.

**Browser return/success pages and inbound email text never establish Payment truth.**

Ariya may recognize a payment-proof email and route it to reconciliation review, but cannot mark the Payment verified from prose/attachment alone without the configured evidence workflow.

## Payment provider contract
Payment providers implement a provider-neutral PaymentConnector. Capabilities may include create payment intent/link, query transaction, verify/normalize provider event, refund, settlement/reconciliation metadata and health.

Provider-specific UI/configuration belongs to Connector instances/packages, not scattered Billing state.

## Reconciliation
Support unmatched payment queue, suggested matches, manual matching, split allocation, overpayment/credit handling, duplicate detection and provider/bank import. Suggestions do not silently mutate financial records.

## Receipts
Generated only from verified/approved Payment truth. Receipt has its own reference, linked allocations, issue timestamp, **signed immutable PDF snapshot** and delivery history.

## Credit Notes and Refunds
Credit Notes preserve issued-Invoice history through controlled reason/amount/lines and balance/refund/credit behavior.

Refund lifecycle: Request -> Approval where required -> provider/manual execution -> verification -> allocation/financial result. Failed attempts remain visible.

## Recurring billing / arrangements
A Recurring Arrangement/Client Service may link to a Billing Schedule. The schedule can define price/currency, frequency, start/end, tax, payment terms, Properties and Contract/Proposal source.

Schedules may create Invoice drafts or provider charges according to explicit policy. Auto-issue/auto-charge is never assumed.

## Deposits and payment schedules
Accepted Proposals/Contracts may define percentage or fixed deposit, milestone installment, selected-line billing or remaining-balance schedule. Downstream Invoice generation is idempotent and linked to the originating terms.

## Dunning and credit control
Configurable stages can include due soon, due, overdue, escalation, account/service risk warning, payment-plan discussion and final handling.

Service/account hold is a deliberate registered Action and should not be triggered by one noisy event.

## Account Statements
Generate signed client-facing statements from authoritative Invoice, Payment, Credit Note and Adjustment truth. Period/opening/closing balance and transactions must be reproducible.

## Operational spend linkage
Approved Expense records may be associated with Organisation/Project/Property/Service and proposed for Invoice conversion where contractually allowed. Project financial reporting may compare committed revenue/approved scope against explicit expenses/costs without Timesheet labor costing.

## Signed Billing documents
Every final/issued Invoice, Receipt, Credit Note and Account Statement PDF must carry issuer signature and immutable Document Studio evidence:
- exact rendered version;
- Operating Entity/Brand;
- authorised signatory/signature snapshot;
- issue timestamp;
- document hash;
- verification reference/code.

Invoices/Receipts normally need issuer signature only, not client signature.

## Portal
Clients can view permitted signed Invoices, Payment status/history, Receipts, Credit Notes/Adjustments safe for client, available payment action, recurring arrangements/active services, deposits/payment milestones, Account Statements and renewals requiring payment/decision.

## Attention / Notifications
Examples: Invoice overdue, late-fee policy pending/applied, deposit overdue, unmatched Payment, failed refund, provider auth issue, credit-control review, recurring-generation failure.

Avoid duplicate reminders; Attention resolves only when source condition resolves.

## Ariya
Ariya may explain balances and why they changed, summarize receivables, identify overdue risk, draft collection messages, recognize incoming payment evidence for triage, and recommend reconciliation matches. It must cite authoritative evidence and never fabricate Payment truth.

## Permissions
Examples include `billing.read`, `billing.manage`, `billing.invoices.create`, `billing.invoices.approve`, `billing.invoices.issue`, `billing.payments.record`, `billing.payments.reconcile`, `billing.adjustments.manage`, `billing.credits.manage`, `billing.refunds.request`, `billing.refunds.approve`, `billing.recurring.manage` and `billing.settings.manage`.

## Acceptance criteria
- browser/email text never establishes Payment truth;
- duplicate provider events do not duplicate Payments;
- Receipt cannot exist without verified/approved Payment;
- Payment is not mutated to hold penalties/discounts;
- late fees/penalties are real audited Adjustments;
- Invoice balance is derived from authoritative components;
- every issued Billing PDF is signed and immutable;
- historical templates/signatures cannot rewrite old documents;
- cross-client access is denied server-side;
- no Timesheet/work-timer/HR/consumption dependency exists.

## Build slices
1. Billing overview + Invoice list/workspace.
2. Invoice creation/approval/issue + signed Document Studio output.
3. Adjustment/Credit model + discount/late-fee policy.
4. Payment records/allocations/Receipts/reconciliation.
5. PaymentConnector + provider evidence.
6. Recurring Billing + deposits/payment schedules + dunning.
7. Refunds/Statements/project-financial context.
