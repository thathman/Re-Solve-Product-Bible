# Data Provenance, Authority and Synchronization

## Purpose
Re:Solve combines native records, connector data, imports, cached summaries, monitoring observations, derived metrics and AI output. Users and systems need to understand where material information came from and which system is authoritative.

## Provenance dimensions
Where material, data should be able to answer:
- source type
- source/provider
- connector instance/import/run
- external identifier
- captured/synced at
- source observed/updated at
- last verified
- authority/ownership mode
- editable here or read-only
- freshness state
- derived or authoritative
- confidence/quality where applicable

## Source types
Examples:
- native user entry
- native automation
- connector sync
- integration event
- import
- monitoring probe
- calculated/derived
- AI-derived
- migrated legacy data

## Authority modes
Each mapped field/resource relationship should declare one of:
- Re:Solve authoritative
- external system authoritative
- bidirectional with explicit conflict policy
- append/event-only
- derived/cache only
- manual reconciliation

Never assume bidirectional synchronization simply because both systems contain the same field.

## Sync contract
A Connector mapping should declare:
- objects involved
- external identifiers
- supported direction
- trigger model: event, scheduled, on-demand, manual
- create/update/delete semantics
- authoritative fields
- conflict policy
- transformation/mapping rules
- stale threshold
- retry/idempotency behavior
- deletion/archive behavior

## Conflict handling
Supported strategies may include:
- external wins
- Re:Solve wins
- newest-wins only where safe and explicitly approved
- field-level ownership
- manual review
- reject conflicting update

High-impact fields such as billing status, payment truth, permissions, Vault data and executed documents should not use casual newest-wins conflict rules.

## Freshness
Canonical freshness states may include:
- current
- aging
- stale
- unknown
- sync failed
- disconnected

UI uses FreshnessIndicator only when freshness materially affects interpretation.

## Payment truth
Verified provider events/records establish payment truth according to Billing policy. Browser return/success pages are not authoritative.

## Chatwoot truth
Chatwoot remains authoritative for support conversation/message state. Re:Solve stores provider-neutral references and derived summaries.

## Monitoring truth
Monitoring observations are time-bound evidence. Property Posture is a Re:Solve derived state whose reasons/source freshness remain visible.

## AI output
AI-generated values are derived unless a human/approved workflow deliberately applies them to an authoritative record. The original AI suggestion remains distinguishable in activity/audit where required.

## Imports
Imported data retains import batch provenance and validation history.

## UI
Synced/read-only fields should communicate their source where it affects editability. Do not clutter every field with provider labels if provenance is irrelevant to ordinary work.

## API/MCP
APIs should expose provenance/freshness metadata for resources where consumers need it. Agents must not present stale derived data as current fact.

## Acceptance criteria
- every connector declares sync ownership/direction
- provider data cannot silently overwrite authoritative Re:Solve fields without policy
- stale data is distinguishable from confirmed zero/healthy state
- AI-derived values are identifiable
- imports and migrations preserve source history
- conflict resolution is auditable where consequential
