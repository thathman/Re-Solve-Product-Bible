---
name: resolve-connector
description: Use when designing, implementing, configuring, mapping, syncing, monitoring, or reviewing a Re:Solve connector to an external provider or specialist system such as Chatwoot, Cloudflare, payments, email, OJS, WordPress, WooCommerce, calendars, or signing.
---

# Re:Solve Connector

Read `05-extensions/connectors.md`, `06-connectors/core-connectors.md`, data provenance/sync, Action Registry, security and the provider-specific connector spec.

## Boundary
A Connector integrates an external system. Core business truth must not become provider-shaped. Provider-specific packages may be installed as Plugins that register Connector implementations.

## Instance contract
Define:
- connector type and instance name;
- scope/linked Operating Entity, Organisation and/or Properties;
- authentication method and secure credential reference;
- capability list;
- mappings/external identities;
- source authority and sync direction by field/domain;
- health and auth-expiry state;
- rate limits;
- polling/webhook/event model;
- retry/backoff/idempotency/dead-letter/replay behavior;
- audit/logging;
- disable/uninstall behavior.

## Sync/provenance
For every synchronized field or record declare inbound/outbound/bidirectional/read-only ownership and conflict policy. Preserve source, last sync/freshness and external id separately from canonical Re:Solve identity.

## Webhooks/events
Verify provider authenticity/signature where supported. Normalize events before business domains consume them. Make processing idempotent, observable and replayable.

## Writes
Connector actions use Action Registry risk classes. High-impact writes such as DNS changes, refunds, sending/signing, destructive remote changes or security settings require narrow permissions and confirmation/approval/step-up as specified.

## UI
Instance pages show status, capabilities, mappings, last success/error, event backlog, test connection, reauthorize/rotate, logs and degraded states without exposing secrets.

## Completion
Verify provider outage does not become false business truth, duplicate events do not duplicate side effects, secret material stays out of normal records/logs, mapping conflicts are explainable, and the connector can be disabled without corrupting core data.