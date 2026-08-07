# Admin — Reports & Analytics

## Purpose
Turn Re:Solve operational data into trustworthy, permission-aware reporting without forcing every module to invent its own analytics model.

## Navigation
Reports
- Executive
- Clients
- Sales
- Projects
- Finance
- Support
- Properties
- Team & Workload
- Automations
- AI Usage
- Custom/Saved Reports

## Principles
- every metric has a defined source and formula
- live operational counters are distinguished from period reporting
- connector-derived metrics show source/freshness
- role and organisation/property permissions apply to report rows and aggregates
- charts exist only when they improve comprehension
- every visual has a table/detail path where practical

## Executive report
Potential sections: client portfolio health, active work, delivery risk, receivables, recurring services, support pressure, property incidents, renewals, staff capacity and material changes over the selected period.

## Client analytics
Client health distribution, revenue/service mix, active projects, support load, overdue client actions, upcoming renewals, relationship inactivity, risk flags and portfolio trends.

## Sales
Pipeline value, conversion, win/loss, source, cycle duration, forecast, proposal/estimate outcomes, service mix and salesperson/team performance where relevant.

## Projects
On-time delivery, milestone performance, cycle time, client-action delay, change requests, risk/issues, utilisation/time where enabled, outcome completion and project health trends.

## Finance
Invoiced, collected, outstanding, overdue aging, payment method/provider, recurring revenue, credits/refunds, expenses and reconciliation exceptions. Accounting-specific reports belong to an accounting plugin if full accounting is enabled.

## Support
Use normalized Chatwoot/support connector metrics plus Re:Solve business context: conversation volume, response/resolution trends, support by client/property/service, escalations, incidents and entitlement consumption. Do not recreate Chatwoot's agent-console reporting unnecessarily.

## Properties
Health distribution, uptime summaries, incidents, expiry risk, backup freshness, maintenance, recurring issues and service coverage.

## Saved reports
Users can save filters/date ranges/groupings/columns where permitted. Sharing a saved report never grants data permissions the recipient lacks.

## Export
CSV/XLSX/PDF where justified; large exports become background jobs with notification on completion. Sensitive exports are audited and expire when delivered as files.

## API / MCP
Report APIs expose defined metric endpoints and permission-filtered datasets. MCP may answer analytical questions using approved report tools rather than unrestricted database queries.

## PWA/mobile
Key summaries and drill-down lists work on mobile; large custom report building may be desktop-optimized while remaining readable on tablet.

## Lovable build slices
1. Reports shell + Executive report.
2. Client/Project/Finance reports.
3. Support/Properties reports.
4. Saved reports/export.
5. Custom report framework and mobile polish.