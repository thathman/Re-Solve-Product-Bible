# Client Portal — Billing

## Purpose
Let authorized client users understand commercial obligations, pay or verify invoices, retrieve receipts and review active recurring services without needing staff intervention.

## Sections
- Overview
- Invoices
- Payments
- Receipts
- Services
- Renewals
- Credits/Adjustments where applicable

## Overview
Show outstanding balance, overdue balance, invoices requiring attention, recent payments, next recurring charge/renewal, payment issues and billing contact information. Financial information is role-gated.

## Invoice workspace
Show number, issue/due dates, status, currency, line items, tax/withholding fields where applicable, related service/project/property, payment history, credits, downloadable invoice and approved payment methods.

## Payment flow
Core remains provider-neutral. A selected provider plugin/connector creates the payment experience. Browser return pages never establish payment truth; verified provider event/reconciliation does. UI shows pending verification distinctly from paid.

## Receipts
Receipts are immutable generated records tied to verified allocations. Clients can download/retrieve them according to permission.

## Recurring services and renewals
Show service, covered property, billing cadence, amount where authorized, current period, next renewal, renewal state and any required client decision.

## Permissions
Billing Viewer, Billing Contact and Organisation Owner may have different rights. Payment initiation does not imply authority to alter organisation billing settings.

## Notifications
Invoice issued, due soon, overdue, payment pending verification, payment confirmed, payment failed, credit issued, receipt ready, renewal upcoming, renewal action required.

## API / MCP
Read tools: list_my_invoices, get_my_invoice, list_my_payments, get_my_receipt, list_my_recurring_services. Payment-creating tools are high risk and require explicit scope/confirmation. Provider secrets are never exposed.

## PWA/mobile
Invoices and line items must remain legible on phones. Payment flows open safely in provider context where required. Recently viewed invoices/receipts may be cached only when policy permits and confidential storage protections are respected.

## Lovable build slices
1. Billing overview and invoice list.
2. Invoice detail/download states.
3. Payment provider handoff and verification states.
4. Payments/receipts.
5. Services/renewals and mobile polish.