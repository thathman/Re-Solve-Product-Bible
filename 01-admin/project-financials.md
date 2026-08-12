# Admin — Project Financial Plan and Commercial Health

## Purpose
Project Financial Plan gives Re:Solve an agency-appropriate view of Project commercial health without Timesheets, time budgets, employee utilization or full accounting.

It answers:
- what commercial value was agreed;
- what approved changes increased/decreased that value;
- what explicit external/operational costs are known;
- what has been invoiced;
- what has been paid;
- what remains to invoice/collect;
- what expected gross margin is supported by real data.

## Principles
- financial truth is linked from Sales/Billing/Expense records rather than copied manually;
- no labor cost is inferred from hours because Re:Solve has no time tracking;
- unlike currencies are never silently combined;
- margin/profitability is shown only when the underlying revenue/cost inputs are meaningful and currency-compatible;
- accepted Proposal/Contract and approved Change Requests preserve historical commercial commitments;
- Project financial views never become a statutory ledger.

## Project Financial Plan
A Project may have a Financial Plan summarizing/planning the commercial frame.

Potential fields/derived components:
- Operating Entity;
- Organisation;
- currency or explicit multi-currency context;
- accepted Proposal/Contract source;
- original contracted value;
- approved Change Request additions/reductions;
- approved discounts/credits affecting Project economics where relevant;
- deposit/payment schedule summary;
- planned/approved external cost budget;
- cost categories;
- expected gross margin amount/percentage when valid;
- internal notes/assumptions;
- current plan version/status.

The Financial Plan does not replace Invoice/Payment/Expense truth.

## Revenue context
Derive from authoritative records where possible:
- accepted Proposal lines tied to Project;
- executed Contract value where authoritative;
- approved Change Requests;
- linked Invoices;
- Credit Notes/Adjustments that affect Project-linked revenue;
- linked Recurring Arrangement/Client Service where the Project is part of activation/delivery.

Useful derived views:
- contracted/approved revenue;
- invoiced;
- not yet invoiced;
- paid;
- outstanding;
- credited/adjusted;
- remaining scheduled billing.

## Cost context
Explicit costs may come from:
- Project-linked Expenses;
- approved vendor/external costs;
- service/platform/license purchases;
- hosting/domain/provider costs allocated to Project where meaningful;
- approved one-off contractor cost records if modeled as ordinary operational Expense/vendor cost, not HR/payroll.

Do not estimate hidden employee labor cost from salary/hour assumptions in core Re:Solve.

## Cost budget
A Project can define an approved external/operational cost budget by category, for example:
- contractors/vendors;
- software/licenses;
- hosting/infrastructure;
- travel/non-employee operational cost where deployment supports it;
- materials/printing;
- miscellaneous approved cost.

This is a financial planning limit/reference, not procurement or accounting.

## Margin / commercial health
Where revenue and cost data share a valid currency basis:

`expected gross margin = approved project revenue - approved/expected explicit project costs`

`realized/current gross margin context = recognized/selected revenue basis - actual explicit costs`

The UI must label which basis is used. Do not call something profit if it excludes known required categories without explaining the scope.

If multiple currencies exist and no explicit conversion policy/rate is available, show per-currency values rather than one false margin total.

## Changes and scope
Approved Change Requests can change commercial value/cost expectations through controlled Sales/Billing Actions.

The original Proposal/Contract remains intact. Financial Plan shows:
- original value;
- approved changes;
- current approved value;
- pending changes separately.

Pending/unapproved Change Requests are not counted as committed revenue.

## Budget warnings / Attention
Potential explainable conditions:
- explicit costs exceed approved cost budget;
- Project has delivered/completed work with material amount not invoiced;
- payment is overdue against Project-linked Invoice;
- Change Request approved but Billing/Proposal follow-up missing;
- expected margin falls below configured threshold;
- cost/revenue data incomplete/stale;
- multi-currency prevents valid aggregate.

These create Attention only when policy makes them actionable.

## Admin UX
Project `Financials`/`Cost & Commercial` should show a calm decision view:
- Approved value;
- Invoiced;
- Paid;
- Outstanding;
- Remaining to invoice;
- Approved external cost budget;
- Actual explicit costs;
- expected/current margin where valid;
- Change Request impact;
- related Proposal/Contract/Invoices/Expenses.

Users can drill into source records rather than editing derived totals directly.

## Portal
Client Portal may show only approved client-safe commercial information such as Proposal/Contract value, Invoices, Payments and approved Change Request pricing.

Internal cost budget, vendor cost and margin are staff-only unless a deployment explicitly exposes a specific client-safe field.

## Reports
Project/portfolio reporting may aggregate currency-compatible values by Operating Entity, client, service, Project status, date and category.

Unlike currencies remain separate unless a defined conversion/reporting policy is explicitly applied and visible.

## Ariya
Ariya may:
- explain Project financial state;
- answer how much is contracted/invoiced/paid/outstanding;
- identify unbilled approved work;
- explain why margin changed;
- flag missing cost/revenue links;
- draft a billing follow-up;
- recommend a Change Request/commercial review when authorised evidence suggests scope changed.

Ariya cannot invent costs, convert currencies silently or mark revenue/Payment authoritative from inference.

## Approvals
High cost-budget changes, unusual margins/discounts, write-offs or commercial changes may use Approval Policies.

## API / MCP
Possible read operations:
- `get_project_financial_summary`;
- `get_project_billing_status`;
- `list_unbilled_project_value`;
- `list_project_costs`.

Writes route to underlying Proposal/Change Request/Billing/Expense/Financial Plan Actions.

## Acceptance criteria
- Project financial view links to authoritative Sales/Billing/Expense truth;
- original and changed approved commercial value are distinguishable;
- unapproved changes do not inflate revenue;
- cost budgets track explicit non-time costs only;
- margin is shown only with valid inputs/currency basis;
- internal cost/margin never leaks to Portal by default;
- no Timesheets/work timers/utilization/full accounting are introduced.

## Build slices
1. Project Financial Plan + source relationships.
2. Billing/revenue summary.
3. Expense/cost budget summary.
4. Change Request financial impact.
5. Attention/reporting/Ariya.
6. Portal-safe separation and multi-currency review.
