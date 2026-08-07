# Native Monitoring Engine and Property Posture

## Purpose
Re:Solve includes its own monitoring capability for the common checks required to operate client Properties. External monitoring products are optional signal sources, not required infrastructure.

The Monitoring Engine answers whether a Property is reachable/healthy. Property Posture answers whether it is operationally safe and well-maintained.

## Architecture

```text
Native Re:Solve Probes        External Connector Signals       Property Obligations
HTTP/HTTPS                    Cloudflare                       Domain expiry
SSL/certificate               Uptime Kuma                      Hosting expiry
DNS/TCP                       Hosting providers                Renewal status
Heartbeat                     WordPress/OJS                    Backup freshness
Content check                 future monitors                  Service coverage
        \                         |                            /
         -> normalized Monitoring Signal / Posture Evidence <-
                              |
                        Property Posture
                              |
              Attention / Incident / Notification
```

## Native checks
Build incrementally.

### Initial
- HTTP/HTTPS availability
- expected status-code range
- request timeout
- response latency
- redirect behavior
- SSL certificate validity
- certificate expiry
- domain expiry/registration state where a reliable source is available
- consecutive failure/recovery confirmation
- maintenance windows

### Later
- DNS resolution
- nameserver checks
- DNSSEC signal
- TCP/port check
- content/keyword expectation
- heartbeat/dead-man check for backup/cron/jobs
- backup freshness
- more advanced certificate chain checks
- independent probe locations

## Probe runtime
Monitoring execution must not depend solely on the main web request process.

The architecture should support a separately deployable Re:Solve Monitoring Worker/Probe that:
- receives monitor definitions
- executes checks
- returns signed/authenticated results
- survives ordinary UI/API process restarts
- can later run in multiple regions

FOUND-001 does not build this worker.

## Monitor definition
Fields may include:
- property
- check type
- target
- interval
- timeout
- expected result
- failure threshold
- recovery threshold
- enabled state
- maintenance policy
- client-visible policy
- responsible team/user
- tags
- probe location/pool

Credentials or private monitor auth values are protected through the Vault/secret abstraction.

## Monitoring signal
A signal records:
- monitor
- property
- source
- observed state
- observed value
- checked at
- duration/latency
- evidence/error category
- consecutive state count
- freshness
- correlation id

High-volume raw samples may have a separate retention policy from business incidents/attention.

## Availability state
Suggested monitor states:
- UP
- DEGRADED
- DOWN
- MAINTENANCE
- UNKNOWN
- DISABLED

Do not declare a Property down because a connector itself is unavailable. Unknown provider state and confirmed target failure are different.

## Property Posture
Property Posture aggregates explainable evidence such as:
- availability
- latency/performance
- SSL/certificate
- domain registration/expiry
- DNS health
- hosting expiry/status
- backup freshness
- application version/update state
- WordPress/OJS health signals
- active incidents
- unresolved maintenance
- credential rotation where relevant
- connector freshness

Posture states may be:
- HEALTHY
- ATTENTION
- DEGRADED
- CRITICAL
- MAINTENANCE
- UNKNOWN

Each state must expose the reasons and source freshness that produced it.

## Renewal/expiry obligations
Domain, hosting, SSL, license and other expiry concerns should use first-class Renewal/Expiry Obligation records rather than isolated date fields.

A renewal should know:
- property/asset
- obligation type
- provider/vendor
- source
- expiry date
- auto-renew state
- renewal owner
- responsible client/contact
- related service/contract
- estimated/actual cost where known
- approval requirement
- payment/billing state where relevant
- reminder policy
- status
- last verified
- evidence after renewal

## Renewal Desk
Admin should have a Renewal Desk focused on:
- overdue renewals
- next 7/30/60/90 days
- auto-renew disabled
- unknown renewal state
- client decision required
- payment required
- renewal completed but not verified

## Incident integration
Qualifying outages/degradation may create or attach to an Incident.

Incident state remains a business/operational record, not simply a monitor alert.

## Alert noise controls
Support:
- consecutive-failure threshold
- recovery threshold
- grouping
- deduplication
- maintenance suppression
- dependency awareness where useful
- escalation windows
- flapping detection

## Notifications
Property events can trigger staff/client notifications based on policy:
- outage
- recovery
- prolonged degradation
- domain/hosting/SSL expiry
- failed/stale backup
- monitoring worker failure
- renewal/client decision due

Do not send client alerts for transient unconfirmed failures by default.

## Attention
Monitoring/Posture should produce Attention Items when a condition remains actionable.

## Connectors
External systems can contribute normalized signals through `MonitoringConnector` or more specialized capability contracts.

Initial relevant connectors:
- Cloudflare
- Uptime Kuma optional
- WordPress
- OJS
- hosting providers

## API/MCP/Àríyá
Expose safe operations such as:
- get_property_posture
- list_active_outages
- list_expiring_properties
- get_monitor_history
- acknowledge_incident_attention

Àríyá can explain Posture using source evidence and freshness, but must not invent health facts.

## Client Portal
Portal shows a simplified client-safe posture:
- status
- active incident
- planned maintenance
- renewal action if client involvement is required
- last updated/source-safe explanation

Do not expose internal endpoints, sensitive topology or security details.

## Acceptance criteria
- fresh Re:Solve installation can perform basic monitoring without Uptime Kuma
- external monitoring systems remain optional connector sources
- confirmed target failure and connector failure are distinct
- expiry/renewal is actionable workflow, not a date badge
- posture is explainable down to evidence and freshness
- monitoring can later run independently of the main app process
- client-visible alerts are policy-controlled and noise-resistant
