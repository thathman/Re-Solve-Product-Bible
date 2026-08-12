# Native Monitoring Engine and Property Health / Posture

## Purpose
Re:Solve includes native monitoring for common checks required to operate client Properties. External monitoring products are optional signal sources, not required infrastructure.

The Monitoring Engine answers whether a Property/target is reachable/healthy. Property Health/Posture answers whether it is operationally safe, current and well-maintained. Ariya consumes both as first-class OS intelligence.

## Architecture

```text
Native Re:Solve Probes      External Connector Signals      Property Obligations
HTTP/HTTPS                  Cloudflare                      Domain expiry
SSL/certificate             Uptime Kuma                     Hosting expiry
DNS/TCP                     Hosting providers               Renewal status
Heartbeat                   WordPress/OJS                   Backup freshness
Keyword/JSON/API check      future monitors                 Service coverage
       \                         |                           /
        -> normalized Monitoring Signal / Health Evidence <-
                             |
                    Property Health / Posture
                             |
          Attention / Incident / Notification / Ariya
```

## Native checks
### Initial/core
- HTTP/HTTPS availability;
- expected status-code range;
- request timeout;
- response latency;
- redirect behavior;
- SSL certificate validity/expiry;
- domain expiry/registration where a reliable source exists;
- consecutive failure/recovery confirmation;
- maintenance windows.

### Expanded
- DNS resolution/nameserver expectations/DNSSEC signal;
- TCP/port check;
- content/keyword expectation;
- JSON/API response expectation;
- heartbeat/dead-man checks for backup/cron/jobs;
- backup freshness;
- certificate-chain depth;
- WordPress/OJS/application health;
- hosting/server/container connector signals;
- independent probe locations.

## Probe runtime
Monitoring execution must not depend solely on the main web request process. Architecture supports separately deployable scoped Monitoring Workers/Probes that receive definitions, execute checks and return authenticated results.

A Probe is a narrow Service Account Principal, not broad database/application authority.

## Monitor definition
May include Property, check type, target, interval, timeout, expected result, failure/recovery thresholds, enabled state, maintenance policy, client-visible policy, responsible Team/User, tags and probe location/pool.

Private auth values use Vault/secret capability abstractions.

## Monitoring Signal
Records monitor/property/source, observed state/value, checked time, latency, evidence/error category, consecutive state count, freshness and correlation.

High-volume samples can have separate retention from durable Incidents/Attention.

## Availability states
Suggested: UP, DEGRADED, DOWN, MAINTENANCE, UNKNOWN, DISABLED.

Connector/probe failure is not target failure. Unknown/stale and confirmed DOWN are distinct.

## Property Health / Posture
Aggregates explainable evidence such as availability, latency, SSL, domain registration/expiry, DNS, hosting status, backup freshness, application version/update state, WordPress/OJS health, Incidents, maintenance, credential/Connector freshness and renewals.

Suggested states: HEALTHY, ATTENTION, DEGRADED, CRITICAL, MAINTENANCE, UNKNOWN.

Every state exposes reasons/source freshness; no opaque score may become authority.

## Renewal/expiry obligations
Domain, hosting, SSL, license, Client Service and other expiry concerns use first-class Renewal/Expiry Obligation records with provider/source, expiry, auto-renew state, owner, responsible client/contact, related service/contract, cost where known, approval/payment state, reminder policy, status and last verified evidence.

## Incidents
Qualifying outage/degradation creates or attaches to a real Incident with affected Properties, start, impact, evidence, updates, recovery timestamp/duration and postmortem links as appropriate.

Incident is not just a monitor alert.

## Noise controls
Consecutive-failure/recovery thresholds, grouping/dedupe, maintenance suppression, dependency awareness, escalation windows and flapping detection prevent noisy false client alerts.

## Ariya — Watch / Investigate / Recommend
Ariya is a first-class consumer of Monitoring/Posture evidence.

It may:
- explain why a Property is Healthy/Degraded/Critical;
- cite the exact monitors/Connector signals/renewals and freshness;
- Watch for failures, expiry windows, backup staleness and recovery;
- correlate recurring failures or simultaneous signals;
- Investigate likely cause while labeling inference;
- recommend remediation;
- create/attach a Task, Incident or Support item through an approved Automation/Action policy;
- draft staff/client incident updates;
- recognize when the monitor/Connector itself is stale rather than calling the Property down.

Ariya cannot invent health facts or bypass target credentials/permissions.

## Notifications / Attention / Tasks
Confirmed outage/recovery, prolonged degradation, domain/hosting/SSL expiry, failed backup, Worker failure and renewal/client decision can generate policy-controlled notifications.

Persistent actionable conditions generate Attention. Assigned remediation can surface in Tasks.

## Connectors
External systems contribute normalized signals through MonitoringConnector/specialized capabilities. Relevant sources include Cloudflare, optional Uptime Kuma, WordPress, OJS and hosting providers.

## Client Portal
Portal shows simplified client-safe Health:
- status;
- active Incident;
- planned maintenance;
- renewal action if client involvement is required;
- approved explanation/last updated.

Do not expose sensitive topology/endpoints/security details.

## Optional status pages
A deployment may expose client/public status pages for selected Properties/services/incidents using only explicitly approved client/public-safe Health/Incident data. This is optional and must not reveal internal monitor details.

## API / MCP
Safe operations may include `get_property_health`, `list_active_outages`, `list_expiring_properties`, `get_monitor_history`, `get_incident` and controlled acknowledgement/remediation Actions.

## Acceptance criteria
- fresh installation can perform basic monitoring without Uptime Kuma;
- external systems remain optional sources;
- connector/probe failure and confirmed target failure are distinct;
- renewals are workflow, not date badges;
- Health/Posture is explainable down to evidence/freshness;
- Ariya can Watch/investigate using real evidence;
- monitoring can run independently of main app;
- client/public exposure is policy-controlled/noise-resistant;
- no sensitive topology/secret leaks.

## Build slices
1. HTTP/HTTPS + latency/SSL native monitoring.
2. Posture/Health derivation + evidence/freshness.
3. Incidents + Attention/Tasks/notifications.
4. Worker/Probe runtime.
5. DNS/TCP/content/JSON/heartbeat/backups.
6. Ariya Watch/Investigate/Recommend.
7. Connector signals + client-safe Portal/status page.
