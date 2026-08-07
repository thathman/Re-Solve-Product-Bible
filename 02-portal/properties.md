# Client Portal — Properties

## Purpose
Give client Users a clear, safe view of permitted managed Properties, current **Property Posture**, work/Support context and Renewal actions without exposing internal monitoring/provider complexity.

## Primary flows
1. Browse/search permitted Properties.
2. Understand current client-safe Posture and what is being managed.
3. Open a Property workspace.
4. Review Projects, Requests, Support, Services, Files/Knowledge, Monitoring summary, Incidents/Maintenance and Renewals.
5. Complete an Approval/Request/File/renewal action where authorized.
6. Access explicitly shared Vault Items separately when granted.

## Property list
Each row/card may show:
- name/type;
- parent/hierarchy context;
- lifecycle status;
- client-safe Posture;
- current Service;
- active Project/Request indicator;
- client action count;
- next Renewal;
- active Incident/Maintenance;
- last updated/freshness where material.

Filters:
- type;
- lifecycle status;
- Posture;
- Service;
- parent;
- requires my action;
- Renewal window.

Search name, domain, human reference and permitted aliases.

Users see only Properties allowed by Membership + Property grants. Hidden descendants cannot leak through counts/search.

## Property workspace
Recommended sections:
- Overview
- Projects / Requests
- Support
- Services
- Files / Knowledge
- Status & Monitoring
- Renewals
- Vault when authorized
- Activity

Keep client navigation simple; sections may combine when content is light.

## Overview
Prioritize:
- what the Property is;
- lifecycle status;
- client-safe Property Posture and explanation;
- current client Attention/actions;
- active Project/Request;
- Service/support coverage;
- active Incident/Maintenance;
- next Renewal;
- recent meaningful update.

## Property Posture
Portal presents a simplified state such as:
- Healthy
- Attention needed
- Degraded
- Maintenance
- Unknown / awaiting fresh status

Reasons may include `Website responding slowly`, `Domain renewal due`, `Backup status needs attention`, `Active incident`, etc.

Do **not** expose internal topology, private endpoints, credentials, raw monitor errors, Connector logs or irrelevant provider implementation.

### Source/freshness
Show `Last updated` and safe source context when it matters, especially when status is stale/unknown.

A Cloudflare/Uptime Kuma/other Connector failure should appear as `Status data unavailable/stale` when appropriate—not falsely as `Property down`.

## Native Monitoring summary
Client-safe summary may include:
- availability/uptime trend where policy allows;
- current response state;
- recent confirmed Incident;
- certificate/domain expiry;
- backup/heartbeat freshness where client-relevant;
- Maintenance.

Raw samples/technical diagnostics stay staff-only.

## Incidents / Maintenance
Client can see permitted:
- status/severity language;
- affected Property;
- detected/update/resolved times;
- client-safe updates;
- planned Maintenance window;
- recovery state.

Incident internal root-cause work/technical notes are staff-only until deliberately published.

## Renewals
Show first-class Renewal/Expiry Obligations such as Domain, Hosting, Certificate, Service/Contract where related.

Client-safe fields/actions:
- item;
- expiry/renewal date;
- state;
- auto-renew status if relevant and safe;
- whether client decision/payment is required;
- next action;
- related Invoice/Proposal/Contract where authorized;
- completion/verification state.

Do not show a bare red expiry badge without workflow/context.

## Requests
Property workspace can provide `New Request`/existing Requests for changes, access, maintenance or service asks. Request triage remains separate from Chatwoot Support and Projects.

## Support
Show Support Entitlement, active Incident/safe references and clear `Open/Start Support` action through Chatwoot. Do not recreate Chatwoot conversation UI.

## Services
Show client-visible Service name, scope summary, covered Property, status and renewal. No hours/credits consumed or Client Service Consumption.

## Files / Knowledge
Ordinary shared Files and client-visible Knowledge follow their own permission models.

Protected confidential documents/items belong in Vault and must not appear as a parallel ordinary File download.

## Vault
Only explicitly granted Items/actions appear. Reveal/download may require step-up and are audited. No offline cache.

## Activity
Client-safe meaningful chronology only. Internal Notes/Audit/provider logs remain hidden.

## Attention / Notifications
Property client Attention may include:
- Renewal decision/payment;
- requested File/access;
- Approval;
- active Incident requiring awareness/action;
- maintenance acknowledgement where configured.

Notifications deliver awareness/deep links; reading one does not resolve the source Attention.

## Àríyá
Optional Portal Àríyá may answer `Why is this Property marked Attention?` or `When does my domain renew?` using client-safe evidence/freshness.

It cannot expose staff-only diagnostics/Vault/provider credentials.

## API / MCP
Client APIs/tools expose authorized safe projections:
- list_my_properties
- get_my_property
- get_property_posture
- get_property_upcoming_renewals
- list_property_incidents
- list_property_requests

No generic hidden monitor/Vault details.

## Mobile/PWA
Cards/stacked rows are primary mobile representation. Status/action remains visible without horizontal scrolling. Safe summaries may cache read-only with last-refresh state; payments, Approvals, Vault and high-impact actions require connectivity according to policy.

## Plugins / Connectors
Plugins may add portal-safe Core UI tabs/cards/actions in approved slots. Connectors contribute normalized evidence/references, not raw provider consoles.

## Acceptance criteria
- only permitted Properties/descendants appear;
- Posture is understandable/client-safe/explainable;
- stale source differs from confirmed outage;
- Renewal is actionable workflow;
- Chatwoot remains Support engine;
- Vault/ordinary Files remain separate;
- mobile is excellent;
- no Timesheet/HR/Client Service Consumption concept appears.

## Lovable build slices
1. Property list + responsive cards/Saved filters.
2. workspace Overview + Posture demo.
3. Projects/Requests/Support/Services.
4. Monitoring/Incidents/Maintenance/Renewals.
5. Files/Knowledge/Activity.
6. Vault + permission/stale/offline states.
