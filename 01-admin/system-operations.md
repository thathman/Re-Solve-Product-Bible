# Admin — System Operations

## Purpose
Provide Owners/authorized administrators a safe control center for Re:Solve itself: application/runtime health, jobs, Integration Events, Monitoring Workers, logs, backups, storage, delivery, updates and failure recovery.

## Navigation
System:
- Health
- Jobs & Queues
- Integration Events
- Monitoring Workers / Probes
- Logs
- Backups
- Storage
- Delivery Diagnostics
- Feature Flags
- Updates
- Diagnostics
- About

## Health
Show current state/freshness for:
- application/API;
- database/auth;
- storage;
- queue/job runtime;
- realtime where used;
- Monitoring Worker/Probe runtime;
- email/push/WhatsApp delivery;
- Àríyá AI provider;
- Connectors;
- Plugins;
- backup/restore readiness;
- critical dependencies.

Health states distinguish healthy, degraded, unavailable, unknown/stale, disabled and unconfigured.

Do not show false `healthy` because a check itself stopped reporting.

## Jobs & Queues
View scheduled/queued/running/waiting/succeeded/retried/failed/dead-letter jobs.

Show job type/source/owner, related record, attempts, next retry, duration, safe error, correlation and idempotency/replay context.

Authorized Actions may retry/cancel/requeue where safe. High-impact jobs preserve original evidence and cannot be `fixed` by editing history.

## Integration Events
Shared Connector event runtime shows:
- provider/Connector Instance;
- event type/external id;
- verification;
- idempotency/duplicate result;
- processing state;
- source/freshness;
- attempts/error;
- received/processed timestamps;
- correlation.

Raw payload display is strongly permissioned/redacted. Replay routes through registered Connector/Action policy.

## Monitoring Workers / Probes
Native Re:Solve Monitoring supports separately deployable worker/probe processes.

System Ops should eventually show:
- Worker/Probe identity;
- location/pool;
- version;
- status;
- last heartbeat;
- queue/assignment state;
- check success/failure rate;
- clock/time health where relevant;
- authentication/credential state;
- stale/offline status;
- recent safe errors.

A Worker/Probe is a scoped Service Account Principal and should not receive broad application/database authority.

A Probe outage creates Monitoring-system Attention and may make Property evidence `unknown/stale`; it does **not** automatically mark monitored Properties down.

## Logs
Operational diagnostics, not Audit.

Filter by time, severity, component, correlation, job/event/probe/Connector and safe request/Principal context where permitted.

Redact credentials, Vault content, auth/session tokens, Secure External tokens and unnecessary private provider payloads before storage/display.

## Backups / restore readiness
Track:
- policy/scope;
- provider/destination;
- last success;
- size where useful;
- retention;
- encryption state where applicable;
- restore-test date/result;
- failure;
- next expected run;
- owner.

Backup success without restore-test evidence is not sufficient proof of recoverability.

Persistent failure/restore-test overdue can create Attention.

## Storage
Show ordinary File storage and protected Vault storage context distinctly where policy/provider differs:
- provider/health;
- capacity/usage where available;
- failed/abandoned uploads;
- orphan/Data Quality state;
- retention/trash/purge jobs;
- scan/processing failures.

Never expose protected content in storage diagnostics.

## Delivery Diagnostics
Unified read-only operational views for Notification/Communication delivery:
- channel;
- provider/Connector;
- queued/sent/provider-accepted/delivered/failed states where evidence exists;
- attempts/retry;
- safe destination/reference;
- template/event;
- correlation.

Do not imply `delivered` or `read` beyond provider evidence.

## Feature Flags
Controlled rollout/development tool, not permanent product configuration.

Fields: key, description, environment/deployment scope, state, owner, created, expiry/review, Audit.

Business configuration belongs to Settings/Plugins, not indefinite flags.

## Updates / compatibility
Show Re:Solve version, schema/migration version, Plugin versions, Connector compatibility, pending migrations, compatibility warnings and rollback/readiness information.

This does not mandate a specific production deployment updater.

## Diagnostics bundle
Authorized admin can generate a redacted support/diagnostic package with:
- versions;
- health snapshot;
- non-secret configuration metadata;
- selected redacted logs;
- Connector/Plugin health;
- failed job/event/probe summaries.

Never include raw credentials, Vault values, guest tokens or private documents.

## Attention / Notifications
Examples:
- critical system degradation;
- repeated/dead-letter job failure;
- Integration Event backlog;
- Monitoring Worker/Probe offline;
- backup/restore-test failure;
- storage pressure;
- Connector authentication expiry;
- Notification delivery outage;
- incompatible Plugin/update.

Attention persists until the underlying condition resolves. Notifications deliver awareness/escalation.

## Audit
System Actions such as replay, retry of sensitive job, backup restore, feature-flag change, diagnostic export, Plugin/update operation and privileged configuration changes use append-only Audit.

## API / MCP / Àríyá
Privileged APIs/tools may expose safe:
- get_system_health
- list_failed_jobs
- list_dead_letter_events
- get_monitoring_worker_health
- get_backup_status
- get_delivery_health

Raw logs/configuration and mutation tools remain restricted.

Àríyá may summarize authorized system Attention/evidence but cannot execute destructive maintenance simply from natural language without registered Action/confirmation.

## Core UI
System Ops uses strong status/health tables, timelines and Tremor-influenced operational metrics without turning into a wall of identical infrastructure cards. Freshness/unknown states are visually explicit.

## PWA/mobile
Phone supports urgent health/Attention triage and safe retry/acknowledgement where appropriate. Deep diagnostics/logs may optimize for larger screens.

## Acceptance criteria
- system/Connector/Probe unknown is distinct from healthy;
- Probe failure cannot falsely mark client Properties down;
- secrets/protected content are redacted from logs/bundles;
- backup and restore-test state are visible;
- persistent failures create actionable Attention;
- sensitive retries/replays/exports are permissioned/audited;
- system UI uses Core UI/freshness standards.

## Lovable build slices
1. System Health + Attention.
2. Jobs/Queues + Integration Events.
3. Monitoring Worker/Probe health.
4. Logs + Delivery Diagnostics.
5. Backups/Storage.
6. Feature Flags/Updates/Diagnostics.
