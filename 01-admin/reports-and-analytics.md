# Admin — Reports & Analytics

## Purpose
Turn Re:Solve operational/commercial data into trustworthy permission-aware reporting without every domain inventing incompatible metrics.

## Navigation
Within Reports:
- Executive
- Clients
- Sales
- Projects
- Finance
- Support
- Properties & Renewals
- Requests / Lifecycle
- Automations / Platform
- Àríyá / AI Usage
- Data Quality
- Custom / Saved Reports

There is no Team & Workload, HR, Timesheet or employee-utilization reporting area.

## Principles
- every metric has a defined source/formula/period;
- authoritative versus derived/synced metrics are identifiable;
- connector data shows source/freshness;
- permissions apply to rows **and aggregates**;
- live operational counters are distinguished from historical period reporting;
- charts answer a real question and have accessible detail/table paths;
- Tremor strongly influences metrics/visualization composition while Re:Solve Core UI remains authoritative;
- no dashboard/report should invent a metric that cannot be explained.

## Metric definition contract
A reusable metric/report definition should declare:
- stable id/name;
- purpose/question answered;
- source records;
- filters/date semantics;
- formula/aggregation;
- currency/units;
- freshness expectation;
- authority/provenance;
- required permissions;
- client-safe availability;
- drill-down path;
- null/unknown behavior.

Do not render `0` when the truth is unavailable/stale.

## Executive
Potential sections:
- client portfolio Health/Attention;
- onboarding/offboarding status;
- active Project/delivery risk;
- Sales Pipeline/forecast;
- receivables/collections;
- recurring Billing/renewal exposure;
- Property Posture/Incidents;
- Renewal Desk exposure;
- Support escalations;
- major operational/platform changes.

No staff capacity/utilization/Timesheet metrics.

## Clients / Client Success
- Client Health distribution with explainable drivers;
- onboarding status/blockers;
- relationship reviews due/completed;
- active Services/Projects;
- Property Posture exposure;
- overdue receivables;
- renewals;
- Support/Incident pressure;
- relationship inactivity/follow-up;
- expansion/Renewal Opportunity trends.

## Sales
- Pipeline value by stage/period;
- qualified volume;
- conversion/win-loss;
- lead/source;
- cycle duration;
- weighted forecast/target comparison;
- Proposal/Estimate acceptance/expiry;
- Contract execution;
- Service mix;
- renewal/expansion pipeline;
- activity/cadence outcome where meaningful.

Reporting by owner/team is acceptable operationally, but Re:Solve does not provide employee performance-review scoring.

## Projects
- active/completed/at-risk;
- milestone performance;
- cycle duration;
- Client Action delay;
- Deliverable approval duration;
- Change Request frequency/value;
- Requests converted to Project work;
- Risks/Issues;
- project health trends;
- approved Expenses/commercial value where permitted.

Explicitly exclude Timesheets, hours logged and utilization.

## Finance
- invoiced/issued;
- collected;
- outstanding;
- overdue aging;
- payment-provider/method summary;
- unmatched/reconciliation exceptions;
- recurring Billing;
- deposits/payment schedules;
- Credit Notes/Refunds;
- approved operational Spend;
- client concentration;
- Account Statement/balance reporting;
- credit-control exposure.

Statutory accounting reports remain optional Accounting Plugin territory.

## Support
Use Chatwoot/SupportConnector normalized metrics plus Re:Solve context:
- safe conversation volume/trends;
- escalation/SLA risk;
- Support by Organisation/Property/Service;
- Incidents;
- entitlement/plan distribution;
- repeated support patterns.

Do not report employee agent productivity or recreate Chatwoot's native agent-console analytics unnecessarily.

Do not include Client Service Consumption hours/credits.

## Properties & Renewals
- Posture distribution;
- native Monitoring availability/latency summaries;
- Incidents/recovery;
- Domains/Hosting/SSL Renewal exposure;
- auto-renew unknown/off;
- backup/heartbeat freshness;
- Maintenance;
- recurring Posture causes;
- connector/source freshness;
- client decision/payment blockers;
- renewal completion/verification.

Cloudflare/Uptime Kuma/provider-derived metrics identify source.

## Requests / Client Lifecycle
- Requests by type/source/state;
- triage/clarification/completion duration;
- conversion outcomes;
- onboarding completion/blockers;
- offboarding/open access-review state;
- account-review cadence.

## Documents / Commercial performance
May appear in Sales/Executive or custom reports:
- Proposals sent/accepted/declined/expired;
- Estimate outcomes;
- Contracts awaiting/executed;
- document delivery/render failures;
- Secure External Access completion.

## Feedback / Goals
Where enabled:
- survey response/score distributions;
- project/service feedback trends;
- business goal progress;
- forecast versus goal.

Chatwoot remains owner of its support CSAT source.

## Automations / Platform
Authorized views may include:
- Automation success/failure;
- retry/dead-letter trends;
- Connector health/freshness;
- Monitoring Worker health;
- notification delivery failures;
- Plugin health;
- API/MCP usage/limits.

## Àríyá / AI usage
Authorized administration only:
- usage/cost by period/model/feature;
- provider/fallback failures;
- tool/action invocation;
- confirmation/denial rate where useful;
- user feedback;
- budget state.

Do not expose sensitive prompt bodies simply for analytics.

## Data Quality
- duplicate candidates;
- missing required data;
- stale Contacts;
- broken Connector Mappings;
- stale syncs;
- missing Renewal ownership;
- orphan/invalid relationships;
- resolution trend.

## Saved reports
Save permitted filters, date ranges, groupings, columns and visualization choice. Visibility can be private/team/workspace. Sharing never grants underlying data access.

## Custom report framework
A later controlled report builder may choose approved datasets, fields, aggregations and visualization types. It must not become unrestricted SQL.

Plugin-provided datasets/metrics declare permissions and provenance.

## Export / scheduled delivery
CSV/XLSX/PDF where useful. Large exports are background jobs with expiry/revocation and Audit for sensitive exports.

Document Studio may render formal branded reports/statements.

Scheduled report delivery uses Notifications/Communications and evaluates permissions at generation time.

## API / MCP / Àríyá
Report APIs expose defined metric/dataset contracts.
MCP uses approved analytical tools rather than arbitrary database query.
Àríyá may explain/trend/summarize authorized report data with source/formula/freshness visible.

## PWA/mobile
Key summaries and drill-down lists are excellent on mobile. Complex custom-report authoring may optimize for large screens while output remains readable.

## Acceptance criteria
- metrics have explicit source/formula/freshness;
- inaccessible data does not leak through aggregates;
- stale/unavailable is distinct from zero;
- charts are purposeful and Core UI/Tremor-aligned;
- Report Saved Views do not grant access;
- native Monitoring/Renewal/Client Success/Data Quality are covered;
- no HR, Timesheet, utilization or Client Service Consumption reporting exists.

## Lovable build slices
1. Reports shell + metric contract + Executive.
2. Clients / Sales / Projects / Finance.
3. Support / Properties & Renewals / Requests.
4. platform / Àríyá / Data Quality.
5. Saved Reports + export/scheduling.
6. controlled custom-report framework + mobile polish.
