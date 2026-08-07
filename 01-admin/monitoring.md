# Admin — Monitoring and Property Posture

## Purpose
Provide staff a unified operational view of Property health using Re:Solve's native Monitoring Engine plus optional external connector signals.

Re:Solve no longer assumes Uptime Kuma or another monitoring product is required.

See `03-platform/monitoring-engine.md`.

## Scope
Re:Solve owns:
- native monitor definitions;
- normalized monitoring signals;
- Property Posture;
- renewal/expiry obligations;
- incident linkage;
- maintenance windows;
- alert policy;
- client/business context;
- Attention and Notification integration.

External products such as Cloudflare, Uptime Kuma, hosting providers, WordPress and OJS may contribute signals through connectors.

## Navigation
Within Operations -> Monitoring:
- Overview
- Properties
- Native Monitors
- Incidents
- Domains & SSL
- Backups / Heartbeats
- Performance
- Maintenance
- Alert Rules
- Probe/Worker Health
- External Sources

Cross-domain `Renewals` has its own Renewal Desk navigation while Monitoring links relevant expiry/posture evidence.

## Overview
Prioritize attention rather than chart volume:
- active incidents;
- confirmed outages;
- degraded/critical Properties;
- unknown/stale checks;
- upcoming domain/SSL/hosting expiry;
- failed/stale backups;
- scheduled maintenance;
- recently recovered issues;
- muted/suppressed alerts;
- native probe/worker health;
- external source degradation.

## Native monitor workspace
Show:
- Property/target;
- check type;
- current state;
- last check/last success;
- latency/observed value;
- failure/recovery threshold;
- monitor interval;
- maintenance state;
- source/probe location;
- history;
- related incident;
- recent errors;
- owner;
- actions.

Initial check types:
- HTTP/HTTPS;
- expected status;
- response latency;
- SSL validity/expiry;
- domain expiry/registration where reliable source exists.

Later types:
- DNS;
- TCP/port;
- content expectation;
- heartbeat/dead-man check;
- backup freshness;
- richer certificate checks;
- multiple probe locations.

## Probe/worker model
The UI should anticipate a separately deployable Re:Solve Monitoring Worker/Probe. Staff can eventually see probe health/location/freshness without needing deployment internals in ordinary workflows.

## Property Posture workspace
Show:
- client/Organisation;
- Property hierarchy;
- overall posture;
- exact reasons/evidence;
- source/freshness;
- availability;
- certificate/domain state;
- DNS/hosting state where known;
- backup/application connector signals;
- active incident;
- maintenance;
- renewals;
- linked service;
- responsible staff;
- support context;
- related projects/requests;
- notification history.

Posture states:
- healthy
- attention
- degraded
- critical
- maintenance
- unknown

Connector outage must not automatically imply client Property outage.

## Incidents
Incident fields include title/reference, affected Properties, severity, status, detected time, source evidence, owner, client impact, client-safe update, internal timeline, root cause, resolution and follow-up actions.

Lifecycle: investigating -> identified -> monitoring -> resolved -> optional postmortem/closed.

## Alert policy
Rules support:
- failure/recovery thresholds;
- duration;
- dedupe/grouping;
- flapping suppression;
- maintenance suppression;
- business hours/escalation;
- recipients/channels;
- client notification threshold.

Prevent alert storms.

## Domains / SSL / hosting expiry
Expiry is represented through Renewal/Expiry Obligations with provider/source, expiry date, owner, auto-renew state, client responsibility, related service/contract/billing, reminder policy and verification state.

## Backups / heartbeats
Track expected cadence, last success, freshness, evidence and restoration-test metadata where connectors/native heartbeat supply it. Raw backup credentials never live in ordinary records.

## Cloudflare
Cloudflare is a first-class optional connector for registrar/domain/DNS/edge/health signals. See `06-connectors/cloudflare.md`.

## Uptime Kuma
Uptime Kuma remains an optional MonitoringConnector for deployments that already use it. It is not a required Re:Solve dependency.

## Attention
Monitoring/Posture generates Attention for persistent actionable conditions such as outage, renewal due, stale backup, unknown monitoring source or unresolved incident.

## Notifications
Policy-driven events include confirmed outage/recovery, prolonged degradation, expiry windows, backup failure, incident updates and monitoring/probe failures. Client notifications should avoid unconfirmed transient failures.

## Automations
Examples:
- qualifying failures -> create/link Incident;
- repeated degradation -> assign technical owner;
- expiry threshold -> create renewal Attention;
- client decision required -> Portal action/notification;
- maintenance window -> suppress/annotate alerts;
- stable recovery -> resolve relevant monitor Attention and update Incident workflow.

## API / MCP / Àríyá
Examples:
- get_property_posture
- list_active_incidents
- list_expiring_properties
- get_monitor_history
- list_failed_heartbeats
- create_incident_update

Àríyá explains posture from source evidence/freshness and must not invent health facts.

## Mobile/PWA
On-call/technical staff need strong phone views for incident/posture, acknowledgement and updates. Cached status is always labeled with last-refresh time.

## Lovable build slices
1. Monitoring/Posture overview with realistic native demo signals.
2. Native monitor definition/detail UI.
3. Property Posture workspace.
4. Incidents.
5. Renewal/expiry/backups/maintenance integration.
6. probe/worker model and real native check execution.
7. Cloudflare/external connector signals.
8. alert policy and mobile/on-call polish.
