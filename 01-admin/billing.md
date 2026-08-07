# Billing & Finance Operations

## Purpose
Billing converts commercial commitments into invoices, payments, receipts, credits, refunds, recurring charges, and operational financial visibility without hard-coding any payment provider.

## Core records
Invoice, Invoice Item, Payment, Payment Allocation, Receipt, Credit Note, Refund, Subscription, Recurring Service, Billing Schedule, Payment Method Reference, Reconciliation Record, Tax Snapshot, Currency Snapshot, Dunning Event.

## Principles
- financial records are immutable where legally/accountingly relevant
- provider callbacks never override verified payment truth without validation
- payment providers are plugins/connectors
- amounts use integer minor units or equivalent precise money representation
- invoice numbering, tax, currency, and payment terms are configurable
- all write actions are auditable

## Billing overview
Show:
- outstanding receivables
- overdue receivables
- invoices due soon
- payments received
- recurring revenue due
- failed/unmatched payments
- credit/refund activity
- aging buckets
- client concentration and cash-flow indicators when permitted

Avoid vanity charts; prioritize operational actions.

## Invoices
Fields: number, organisation, billing contact, currency, issue date, due date, status, line items, tax snapshot, discount, subtotal, total, paid, balance, payment terms, linked contract/proposal/project/service, notes, client-visible memo, attachments, delivery history.

States: Draft → Approved → Issued → Partially Paid → Paid; plus Overdue, Void, Written Off where permitted.

Issued invoices cannot be edited in-place when changes affect financial meaning. Use credit/reissue or approved adjustment rules.

## Payments
Payments may originate from payment connectors, manual bank transfer, cash/manual record, reconciliation import, or approved internal adjustment.

Fields: provider, external reference, payer, amount, currency, received time, verified time, status, allocations, fees if known, evidence, reconciliation state, source.

States: Pending, Verified, Partially Allocated, Allocated, Failed, Reversed, Refunded.

## Payment provider plugin contract
A provider plugin may implement:
- create payment intent/link
- query transaction
- verify webhook
- fetch transaction
- refund where supported and permitted
- health check
- reconciliation metadata
- provider-specific settings UI

Core Billing must not know provider-specific fields beyond a generic provider metadata envelope.

## Reconciliation
Support unmatched payment queue, suggested invoice matches, manual matching, split allocation, overpayment/credit balance, duplicate detection, reconciliation audit, and provider/bank statement import through plugins.

## Receipts
Receipts are generated only from verified/approved payment records. Each receipt has immutable reference, linked payment allocations, issue timestamp, downloadable document, and re-send history.

## Credit notes
Credit Notes adjust issued invoice value through controlled reason codes and linked line items. They may reduce balance, create account credit, or support refund workflows.

## Refunds
Refund request → approval when required → provider/manual execution → verification → allocation/accounting result. Failed refund attempts remain visible; never silently mark complete.

## Subscriptions and recurring services
Recurring Service ties a Service to client, price, billing frequency, start/end/renewal dates, quantity, tax, payment terms, property scope, contract, support entitlement, and status.

Billing schedules generate invoice drafts or charges according to policy. Never auto-issue or auto-charge unless explicitly configured.

## Dunning
Configurable stages for due soon, due, overdue, escalation, service-risk warning, and final handling. Channels may include in-app, email, WhatsApp, and manual task creation. Respect client/contact preferences and mandatory finance notices.

## Portal experience
Clients can view invoices, download invoices/receipts/credit notes, see balance, payment status, available payment actions, recurring services, renewals, and payment history according to permissions.

## Permissions
billing.read, invoices.create, invoices.approve, invoices.issue, payments.read, payments.record, payments.reconcile, credits.manage, refunds.request, refunds.approve, subscriptions.manage, pricing_sensitive.read, billing_settings.manage.

## Notifications
invoice approved/issued/viewed/due/overdue, payment verified/failed/unmatched, receipt issued, credit note issued, refund requested/approved/completed/failed, recurring invoice upcoming, renewal approaching.

## Automations
- accepted contract → create recurring service/billing schedule
- schedule due → draft invoice
- invoice overdue → dunning policy
- verified payment → allocate where deterministic and issue receipt
- unmatched payment → finance queue
- full payment → update linked commercial/project status when configured

## API
Versioned API for invoices, payments, allocations, receipts, credits, refunds, subscriptions, schedules, reconciliation, and provider-neutral payment actions. Webhook ingestion must be signature-verified, idempotent, replayable, and auditable.

## MCP
Candidates: get_invoice, list_overdue_invoices, get_client_balance, get_payment_status, list_unmatched_payments, get_subscription, list_upcoming_renewals, draft_invoice. Issuing invoices, recording payments, approving refunds, or changing financial records require high-trust scopes and confirmation.

## PWA/mobile
Mobile supports invoice review, payment verification summary, reconciliation triage, receipt lookup, client payment view, and approvals. Destructive or high-risk finance actions require online confirmation and step-up controls where configured.

## Acceptance criteria
- browser return pages never establish payment truth
- duplicate provider webhooks do not duplicate payments
- receipt cannot exist without verified/approved payment record
- issued invoices preserve immutable financial history
- cross-client financial access is denied server-side
- provider outage does not corrupt core billing records

## Lovable build slices
1. billing overview + invoice list/workspace
2. invoice creation/issue lifecycle
3. payment records + allocations + receipts
4. provider plugin interface + demo provider
5. recurring services + schedules + dunning
6. reconciliation + credits + refunds
