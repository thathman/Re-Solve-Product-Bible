# Billing & Finance Operations

## Purpose
Billing converts commercial commitments into invoices, payments, receipts, credits, refunds, recurring charges and operational financial visibility without hard-coding any payment provider or becoming a full statutory accounting/ERP suite.

## Core records
Invoice, Invoice Item, Payment, Payment Allocation, Receipt, Credit Note, Refund, Subscription, Billing Schedule, Payment Schedule, Deposit Requirement, Payment Method Reference, Reconciliation Record, Tax Snapshot, Currency Snapshot, Dunning Event, Account Statement Reference and Credit-Control Action.

Client Service remains linked from the Service domain. A recurring Client Service may have a Billing Schedule/Subscription, but Re:Solve does **not** maintain Client Service Consumption, hours used/remaining or usage-credit ledgers.

## Principles
- financial records preserve immutable history where financially consequential;
- provider callbacks/events do not establish truth without verification;
- payment capability is provider-neutral through PaymentConnector implementations;
- optional provider packages may be Plugins that register PaymentConnector implementations;
- amounts use precise money representation;
- numbering, tax, currency and terms are configurable;
- material writes are audited;
- billing does not depend on Timesheets/Time Tracking;
- generated invoice/receipt/statement presentation uses Document Studio.

## Navigation
Within Billing:
`Overview | Invoices | Payments | Receipts | Credit Notes | Recurring | Reconciliation | Statements / Credit Control`

Refunds and advanced actions can live contextually rather than bloating top-level navigation.

## Billing overview
Prioritize operational decisions:
- outstanding receivables;
- overdue receivables;
- due soon;
- payments received;
- failed/unmatched payments;
- recurring invoices/charges upcoming;
- deposits/payment milestones due;
- credit/refund activity;
- aging buckets;
- clients requiring credit-control attention;
- reconciliation issues.

Use Tremor-style metrics/trackers/charts only when they add real decision value.

## Invoices
Fields may include human reference/number, Operating Entity, Organisation, billing Contact, currency, issue/due dates, status, lines, tax snapshot, discounts, subtotal/total, paid/balance, payment terms, linked Contract/Proposal/Project/Client Service, notes/client memo, Document Studio version and delivery history.

States: Draft -> Approved -> Issued -> Partially Paid -> Paid, plus Overdue, Void and Written Off where permitted.

Issued invoices are not edited in place when financial meaning changes. Use controlled adjustment, Credit Note, void/reissue or approved correction rules.

## Document rendering
Invoice, Receipt, Credit Note and Account Statement documents use Document Studio templates/versioning/branding.

A historical issued financial document must always be reproducible from its stored snapshot/context and must not silently change because a template was edited later.

## Payments
Payments may originate from PaymentConnector events, approved manual bank/cash/offline recording, reconciliation import or approved adjustment.

Fields include provider/Connector Instance, external reference, payer, amount/currency, received/verified timestamps, status, allocations, fees where known, evidence, reconciliation state, source/provenance and correlation.

States may include Pending, Verified, Partially Allocated, Allocated, Failed, Reversed and Refunded.

**Browser return/success pages never establish payment truth.**

## Payment provider contract
Payment providers implement the provider-neutral PaymentConnector contract.

Capabilities may include:
- create payment intent/link;
- query/get transaction;
- verify/normalize provider event;
- refund where supported and permitted;
- settlement/reconciliation metadata;
- health.

Provider-specific configuration/UI belongs to the provider package/Connector Instance, not scattered across Billing records.

## Reconciliation
Support:
- unmatched payment queue;
- suggested matches;
- manual matching;
- split allocation;
- overpayment/credit handling where enabled;
- duplicate detection;
- provider/bank import through approved connector/importers;
- provenance and reconciliation Audit.

Suggestions must not silently mutate financial records.

## Receipts
Generated only from verified/approved Payment truth. A Receipt has its own human reference, linked Payment allocations, issue timestamp, Document Studio snapshot and delivery history.

## Credit Notes
Controlled reason, amount/lines, linked Invoice and resulting balance/refund/credit behavior. Historical meaning remains immutable.

## Refunds
Request -> Approval where required -> provider/manual execution -> verification -> allocation/accounting result.

Failed attempts remain visible. Re:Solve never marks refund complete solely because a browser/provider UI returned success.

## Recurring billing / Subscriptions
A recurring Client Service may link to a Subscription/Billing Schedule containing:
- Organisation;
- Client Service;
- price/currency;
- billing frequency;
- start/end/renewal;
- quantity when commercially meaningful;
- tax;
- payment terms;
- related Properties;
- Contract;
- Support Entitlement;
- state.

Schedules generate Invoice drafts or provider charges according to policy. Do not auto-issue/auto-charge unless explicitly configured.

No consumption-meter/remaining-hours feature exists.

## Deposits and payment schedules
Commercial terms may define:
- deposit amount/percentage;
- due event/date;
- milestone installment;
- remaining balance schedule;
- invoice-generation rule;
- completion/payment state.

Deposits/payment schedules remain linked to Proposal/Estimate/Contract and downstream Invoices rather than becoming disconnected records.

## Dunning and credit control
Configurable stages can include:
- due soon;
- due;
- overdue;
- escalation;
- account/service risk warning;
- payment-plan discussion;
- final handling.

Credit-control context may include:
- overdue exposure;
- aging;
- client risk/hold policy;
- deposit/prepayment requirement;
- responsible Account/Finance owner;
- latest communication/action;
- next action.

Any service/account hold is a deliberate registered Action and should not be triggered by one noisy provider event.

## Account Statements
Generate client-facing statements from authoritative Invoice, Payment, Credit Note and balance data using Document Studio.

Statement period, opening/closing balance, transactions and outstanding items must be reproducible and permission-scoped.

## Operational spend linkage
Approved Expense records may be associated with Organisation/Project/Property/Service and may be proposed for Invoice conversion where contractually allowed.

Billing does not include payroll, employee expenses or labor-time costing.

## Portal
Clients can view permitted:
- Invoices;
- Payment status/history;
- Receipts;
- Credit Notes;
- available payment action;
- recurring billing/active services;
- deposits/payment milestones;
- Account Statements;
- renewals requiring payment/decision.

Client Service Consumption is not shown because the product does not track it.

## Attention
Examples:
- invoice overdue;
- deposit overdue;
- unmatched payment requiring reconciliation;
- failed refund requiring action;
- payment-provider authentication issue;
- client over credit threshold/hold review;
- recurring billing generation failure.

Attention resolves from the underlying condition.

## Notifications
Invoice approved/issued/due/overdue, payment verified/failed/unmatched, receipt issued, Credit Note, refund lifecycle, recurring billing upcoming and renewal/payment action events.

Use preference/dunning policy and avoid duplicate reminders.

## Automations
Examples:
- executed Contract -> create approved Billing Schedule;
- schedule due -> draft Invoice;
- Invoice overdue -> dunning Attention/notifications;
- verified Payment -> deterministic allocation + Receipt where policy allows;
- unmatched Payment -> Finance Attention;
- full Payment -> update linked commercial state through registered action when configured.

## Permissions
Canonical examples:
- `billing.read`
- `billing.manage`
- `billing.invoices.create`
- `billing.invoices.approve`
- `billing.invoices.issue`
- `billing.payments.read`
- `billing.payments.record`
- `billing.payments.reconcile`
- `billing.credits.manage`
- `billing.refunds.request`
- `billing.refunds.approve`
- `billing.subscriptions.manage`
- `billing.pricing_sensitive.read`
- `billing.settings.manage`

## API / MCP / Àríyá
Versioned API exposes provider-neutral Billing resources/actions with idempotency and Audit.

Candidate MCP tools:
- get_invoice
- list_overdue_invoices
- get_client_balance
- get_payment_status
- list_unmatched_payments
- get_subscription
- get_account_statement_summary
- draft_invoice

Issuing, recording, refunding, crediting, holding an account or changing financial records uses Action Registry + high-trust scope/confirmation.

Àríyá may explain balances, reconcile context or draft client follow-up using evidence, but never fabricates Payment truth.

## PWA/mobile
Mobile supports invoice/statement review, payment summary, reconciliation triage, receipt lookup, client payment view and approvals. High-impact finance actions require connectivity and stronger confirmation where configured.

## Acceptance criteria
- browser return pages never establish Payment truth;
- duplicate provider events do not duplicate Payments;
- Receipt cannot exist without verified/approved Payment;
- issued financial records preserve history;
- Document Studio rendering cannot rewrite historical issued content;
- cross-client access is denied server-side;
- provider outage does not corrupt core records;
- Account Statements derive from authoritative Billing data;
- no Timesheet, HR or Client Service Consumption dependency exists.

## Lovable build slices
1. Billing overview + Invoice list/workspace.
2. Invoice creation/approval/issue + Document Studio rendering.
3. Payment records + allocations + Receipts.
4. PaymentConnector contract + demo provider.
5. Recurring billing + deposits/payment schedules + dunning.
6. Reconciliation + Credits + Refunds.
7. Account Statements + credit-control operations.
