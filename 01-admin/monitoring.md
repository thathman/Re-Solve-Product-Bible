# Admin — Monitoring

## Purpose
Provide staff a unified operational view of property health without rebuilding specialist monitoring engines.

## Scope
Monitoring aggregates and normalizes signals from native checks and MonitoringConnector implementations such as Uptime Kuma. Re:Solve owns business context, incident linkage, client impact, maintenance, alert policy and operational workflow.

## Navigation
Monitoring
- Overview
- Properties
- Uptime
- Domains & SSL
- Backups
- Performance
- Email Health
- Incidents
- Maintenance
- Alert Rules
- Connector Health

## Overview
Prioritize attention rather than chart volume:
- active incidents
- degraded properties
- failing/unknown checks
- upcoming domain/SSL/hosting expiries
- failed/stale backups
- scheduled maintenance
- recently resolved issues
- muted/suppressed alerts

## Property monitoring workspace
Show client, property hierarchy, current health, checks grouped by category, active incident, recent trend, maintenance windows, linked service, responsible staff, support context, related project and notification history.

## Health model
Health is derived and explainable. Recommended states: healthy, informational, degraded, critical, maintenance, unknown. Each health state must show the evidence that produced it. Connector outage must not automatically imply client property outage.

## Incidents
Incident fields: title, impacted properties, severity, status, detected time, source signals, owner, client impact, public/client-safe update, internal timeline, root cause, resolution, follow-up tasks.

Lifecycle: investigating → identified → monitoring → resolved, with optional custom states. Incident updates may trigger staff/client notifications based on severity and visibility.

## Alert policy
Rules support thresholds, duration, deduplication, grouping, maintenance suppression, escalation, business hours, recipient groups and channels. Prevent alert storms.

## Domains/SSL/renewals
Track expiry, provider, renewal ownership, auto-renew state where known, verification status and reminders. Renewal records link into Services/Billing where applicable.

## Backups
Track last successful backup, expected cadence, age, verification, size/location metadata, failure state and restoration-test evidence. Do not store raw backup credentials in normal records.

## Notifications
Critical outage, prolonged degradation, backup failure, expiry windows, connector failure and unresolved incident escalation. Policies determine in-app/push/email/WhatsApp.

## Automations
Create incident from qualifying signals; assign owner; create follow-up task; notify client after defined threshold; auto-resolve when evidence is stable; schedule maintenance suppressions.

## API / MCP
Examples: get_property_health, list_active_incidents, list_expiring_domains, list_failed_backups, create_incident_update. Raw provider tokens and sensitive monitoring internals are excluded.

## Mobile/PWA
On-call staff need a strong mobile incident view. Critical incident acknowledgement and update posting must be phone-friendly. Cached status is labeled with last refreshed time.

## Lovable build slices
1. Monitoring overview with realistic multi-property demo signals.
2. Property monitoring workspace.
3. Incidents.
4. Expiry/backups/maintenance.
5. Alert policy and mobile/on-call polish.