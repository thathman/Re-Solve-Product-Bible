# Operational Spend and Expenses

## Purpose
Re:Solve may track operational/project/client-related expenses needed for commercial visibility without becoming a full accounting/ERP system.

This area is optional in early builds and does not introduce payroll, HR or timesheets.

## Expense record
Potential fields:
- reference
- date
- amount/currency
- tax where relevant
- category
- vendor Organisation
- description
- client Organisation
- project/property/service context
- billable to client yes/no
- billing status
- receipt/file
- approval state
- payment method/reference metadata
- owner/submitted by
- status

## Recurring cost
A recurring operational cost may represent:
- hosting/vendor subscription
- domain/SSL/provider fee
- software/tool subscription
- contractor/vendor service cost

It is not an employee payroll record.

## Billable expenses
Where contract/workflow permits, an approved billable expense may be proposed as an Invoice line with traceability back to the expense.

Do not silently invoice an expense merely because it is marked billable.

## Approval
Expense approvals use the shared Approval platform where enabled.

## Files
Receipts and ordinary evidence use Files. Protected financial/confidential evidence may use Vault according to policy.

## Reporting
Useful outputs:
- spend by vendor/category/client/project/property
- unbilled approved expenses
- recurring vendor obligations
- project/client cost context

These are operational finance reports, not statutory accounting statements.

## Vendor Organisations
Vendors use the same Organisation model with appropriate relationship type. Future Procurement may add purchase orders/vendor bills as a plugin/advanced module.

## API/MCP/Àríyá
Àríyá may summarize authorized costs or draft explanations, but financial mutations remain controlled actions.

## Acceptance criteria
- expenses can link to clients/projects/properties/vendors without creating parallel entity models
- billable expenses require deliberate invoice conversion
- no payroll, HR or timesheet functionality is implied
- full accounting remains optional/extension territory
