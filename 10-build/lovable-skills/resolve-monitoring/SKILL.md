---
name: resolve-monitoring
description: Use when building or reviewing Re:Solve native monitors, Monitoring Workers/Probes, monitoring signals, Property Posture, incidents, renewal/expiry monitoring, alert rules, or monitoring-provider connectors.
---

# Re:Solve Monitoring

Read `03-platform/monitoring-engine.md`, Admin Monitoring, Properties, Attention Engine, Notifications, Renewal rules, provenance/sync and relevant connector specs.

## Architecture
Native Monitoring is a Re:Solve capability. External providers such as Cloudflare Health Checks or Uptime Kuma are optional signal sources, not required architecture.

Keep monitoring execution separable from the main web process through a Monitoring Worker/Probe contract so the application can eventually monitor even when the primary web node is unavailable.

## Monitor definition
Declare target/property, monitor type, interval, timeout, expected result, retry/consecutive-failure threshold, maintenance policy, severity/impact mapping and last/next check.

Initial native monitor types include HTTP/HTTPS availability, expected status, latency, SSL validity/expiry and domain expiry evidence. Add DNS/TCP/content/heartbeat/backup freshness only in their explicit slices.

## Signal truth
A Signal records observation, timestamp, source/probe, result, latency/details and confidence/verification where applicable. Provider/connector failure is not automatically target failure.

## Property Posture
Posture combines explainable evidence from native checks, renewals, incidents, connectors and relevant application state. Always show contributing reasons and freshness; never paint unexplained red/yellow/green health.

## Incident/Attention
Use threshold/dedup logic before creating Incident, Attention or Notification. Prevent alert storms. Recovery should be explicit and stable before auto-resolution where policy requires it.

## Renewals
Domain/hosting/certificate/service/contract expiries use Renewal/Expiry Obligation records, not isolated badges. Notifications and Attention derive from those records.

## Security
Monitoring must not leak credentials in target URLs, logs, notifications or APIs. Restricted network targets and SSRF-sensitive checks require explicit safeguards.

## Completion
Verify transient failures do not create noisy incidents, source/freshness is visible, maintenance suppresses appropriately, recovery is handled, provider outage is distinguished from target outage, and mobile incident/attention review remains usable.