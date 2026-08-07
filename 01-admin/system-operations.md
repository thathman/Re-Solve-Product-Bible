# Admin — System Operations

## Purpose
Provide owners/administrators a safe operational control center for Re:Solve itself: health, jobs, events, logs, backups, updates, storage, diagnostics and failure recovery.

## Navigation
System
- Health
- Jobs & Queues
- Integration Events
- Logs
- Backups
- Storage
- Email Delivery
- Notifications Delivery
- Feature Flags
- Updates
- Diagnostics
- About

## Health
Show application, database, auth, storage, realtime/queue runtime where applicable, email, push, WhatsApp, AI, connectors and installed plugin health. Health must distinguish unknown/unconfigured/degraded/down.

## Jobs & Queues
View scheduled, running, succeeded, retried, failed and dead-letter jobs. Show job type, source, related record, attempts, next retry, duration, error summary and correlation ID. Permit safe retry/cancel where supported and authorized.

## Integration Events
Shared webhook/event runtime shows provider, connector instance, event type, verification, idempotency result, processing state, attempts, error, received time and correlation ID. Raw payload display is permission-controlled and redacted where necessary.

## Logs
Logs are for operational diagnostics, not a replacement for Audit. Filter by severity, component, correlation ID, user/request where permitted and time. Secrets and tokens must be redacted before storage/display.

## Backups
Define backup policy, last successful backup, scope, size, retention, encryption, restore-test status and failures. Backup success without restore testing is insufficient evidence of recoverability.

## Storage
Show provider, health, capacity/usage where available, orphan checks, failed uploads, retention jobs and file-security scan state. Vault storage is identified separately where stricter controls apply.

## Delivery diagnostics
Email/Push/WhatsApp notification delivery views show queued/sent/delivered/failed where provider evidence exists, retry state and template/reference. Do not expose private message content to users lacking permission.

## Feature flags
Flags are controlled rollout tools, not permanent configuration. Show key, description, environment/deployment scope, state, owner, expiry/review date and audit history.

## Updates
For self-hosted portability, define application version, database/schema version, installed plugin versions, compatibility warnings, migration readiness and rollback considerations. This spec does not mandate a specific production updater implementation.

## Diagnostics bundle
Admins may generate a redacted support bundle containing versions, health, non-secret configuration metadata, relevant logs and connector health. Never include credentials/Vault values.

## Notifications
Critical system health issue, repeated job failure, backup failure, restore test overdue, connector auth expiry, storage pressure, update compatibility issue.

## API / MCP
System APIs require privileged scopes. MCP may expose get_system_health and list_failed_jobs to authorized operators; raw logs/configuration and mutation tools are restricted.

## Lovable build slices
1. System Health dashboard.
2. Jobs/queues and integration events.
3. Logs/delivery diagnostics.
4. Backups/storage.
5. Feature flags/updates/diagnostics.