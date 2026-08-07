# Client Portal — Billing

## Purpose
Let authorized client Users understand financial/commercial obligations, initiate approved payment, verify resulting state, retrieve Receipts/Statements and review recurring Services/Renewals without staff intervention.

## Sections
Keep navigation simple:
- Overview
- Invoices
- Payments
- Receipts
- Services & Renewals
- Statements

Credit Notes/Refunds/payment schedules appear contextually where relevant rather than as unnecessary top-level tabs for every client.

## Authorization
Financial content is role/capability gated. Organisation Owner/Admin, Billing Contact and other client roles may have different rights.

Users without Billing permission should not see redacted counts/balances that reveal financial state.

Payment initiation does not imply authority to change Billing settings, commercial terms or client membership.

## Overview
Prioritize:
- outstanding balance;
- overdue balance;
- Invoice/deposit/payment milestone requiring action;
- recent verified Payments;
- next recurring Billing/Service renewal;
- Domain/Hosting/property Renewal requiring payment/decision;
- failed/pending verification state;
- recent Receipt;
- Account Statement shortcut;
- Billing Contact/update-request path.

## Invoice workspace
Show:
- human reference/number;
- issue/due date;
- status;
- currency;
- line items/tax/discount;
- linked Service/Project/Property/Contract where client-visible;
- deposit/payment schedule relationship;
- Payment allocations/history;
- Credits/Refund state;
- client-safe notes/terms;
- Document Studio rendered web/PDF version;
- permitted payment options;
- delivery/payment verification status.

Issued historical content must not change because a template changed later.

## Payment flow
Re:Solve remains provider-neutral.

Typical flow:
1. user opens payable Invoice/milestone;
2. selects available provider/method;
3. Re:Solve creates provider-backed Payment intent/link through PaymentConnector;
4. provider flow completes/returns;
5. Portal shows `Pending verification` if provider truth has not yet been confirmed;
6. verified provider event/reconciliation updates Payment/Invoice;
7. Receipt becomes available according to policy.

**Browser return page never establishes `Paid`.**

Failures, duplicate callbacks and provider outages must preserve truthful state.

## Payments
Show permitted Payment records with amount/currency/date, verification status, allocations, method/provider-safe label, Receipt and any reversal/refund state.

Do not expose provider credentials/internal settlement secrets.

## Receipts
Receipts derive from verified/approved Payments, use Document Studio and preserve immutable historical snapshot. Client can view/download according to access policy.

## Credit Notes / Refunds
Where applicable, show safe adjustments/refunds against affected Invoices/Payments with state and resulting balance.

Client self-service refund request, if ever supported, is a controlled Request/Action—not an automatic provider refund button.

## Services & Renewals
Show:
- active Client Service;
- covered Properties;
- commercial status;
- Billing cadence/amount where authorized;
- start/renewal/end;
- related Contract;
- Support Entitlement summary where useful;
- Renewal action/documents/Invoice.

Also show relevant Property Renewal Obligations such as Domain/Hosting when client payment/decision is required.

There is **no Client Service Consumption/remaining hours/credits**.

## Deposits / payment schedules
Clients can understand:
- deposit required/paid;
- installment/milestone amounts;
- due dates;
- linked Invoice/payment status;
- remaining scheduled obligations.

Do not present a schedule line as a completed Payment before verification.

## Account Statements
Authorized Users can generate/view/download a period statement showing opening/closing balance, Invoices, Payments, Credits/Refunds and outstanding items.

Statements use Document Studio and authoritative Billing data.

## Renewals and commercial documents
Renewal actions may link to Proposal/Estimate/Contract/Invoice rendered through Document Studio or Secure External Access where appropriate.

## Requests
Portal can provide controlled Requests such as:
- change Billing Contact;
- request Invoice correction/review;
- request payment-plan discussion;
- ask a Billing question outside Support as product policy chooses.

Requests must not mutate financial truth automatically.

## Attention / Notifications
Client Attention examples:
- Invoice overdue;
- deposit/payment milestone due;
- renewal decision/payment;
- Payment verification issue requiring action.

Notifications may cover Invoice issued/due/overdue, Payment pending/verified/failed, Receipt/Credit/Refund, Statement ready and Renewal events.

Reading the Notification does not resolve the underlying payment/renewal Attention.

## Àríyá
Optional Portal Àríyá may explain an authorized Invoice, balance, payment status, Statement or Renewal using source records/freshness.

It cannot mark an Invoice Paid, change terms or expose internal margin/provider secrets.

## API / MCP
Client-safe operations may include:
- list_my_invoices
- get_my_invoice
- list_my_payments
- get_my_receipt
- list_my_services
- get_my_account_statement
- list_my_renewals

Payment initiation/high-impact operations require explicit client capability/confirmation and use registered Actions.

## PWA/mobile
Invoice/document/line item/Statement presentation must be excellent on phones. Provider flows open safely where required.

Payment/financial mutations require connectivity. Caching financial documents is conservative and follows data classification; Vault-protected documents are never ordinary Billing cache content.

## Accessibility
Money/status is never color-only. Tables recompose for mobile and remain screen-reader understandable. Provider-return/pending states clearly announce verification status.

## Acceptance criteria
- unauthorized client roles cannot infer Billing state;
- provider return never establishes Payment truth;
- Payment pending/verified/failed is explicit;
- Receipts/Statements derive from authoritative data and stable document snapshots;
- Service/Property Renewals provide clear next actions;
- mobile Billing is usable without desktop-table squeezing;
- no Client Service Consumption, Timesheet or HR behavior appears.

## Lovable build slices
1. Overview + Invoice list.
2. Invoice workspace + Document Studio rendering.
3. provider-neutral Payment handoff/verification states.
4. Payments/Receipts/Credits/Refund display.
5. Services/Renewals + deposits/payment schedules.
6. Account Statements + Requests + mobile polish.
