# Attention Engine

## Purpose
The Attention Engine is Re:Solve's shared model for conditions that still require awareness or action now.

A Notification says something happened. An Attention Item says something still needs attention.

## Why it exists
Without a shared attention model, Dashboard, My Work, Portal Home, Àríyá briefings, digests and domain pages would each recreate their own overdue/risk queries.

The Attention Engine provides one explainable contract across domains.

## Core record
An Attention Item should conceptually include:
- id
- type
- title
- concise reason
- priority
- state
- audience/principal
- organisation
- property
- project/service/commercial context
- related record
- owner/assignee where applicable
- source rule/event
- source evidence
- created at
- detected at
- due/threshold time
- snoozed until
- resolved at
- resolution reason
- primary action
- deep link
- grouping/dedup key
- client-safe variant where applicable
- provenance/freshness metadata

## States
- OPEN
- ACKNOWLEDGED
- SNOOZED
- RESOLVED
- DISMISSED where policy permits
- STALE/UNKNOWN when evidence cannot be refreshed

## Priority
Use the canonical Notification priority vocabulary where possible:
- informational
- normal
- important
- urgent
- critical

Priority determines presentation and escalation, not authorization.

## Attention sources
Examples:
- task overdue
- approval waiting
- client action overdue
- invoice overdue
- renewal approaching
- domain/hosting/SSL expiry
- property degraded
- backup stale
- active incident
- connector authentication broken
- dead-letter accumulation
- Vault access request
- credential rotation due
- knowledge review overdue
- client onboarding blocked
- proposal expiring
- contract signature waiting
- data-quality issue
- automation failure

Plugins may register namespaced Attention providers through approved contracts.

## Resolution
Attention should resolve because the underlying condition is no longer true, not merely because a notification was read.

Examples:
- invoice paid -> overdue attention resolves
- domain renewed -> renewal attention resolves
- connector reauthenticated -> connector attention resolves
- approval completed -> approval attention resolves

Manual acknowledgement may suppress presentation without falsely resolving the underlying business condition.

## Aggregation
Attention items may group into higher-level summaries:
- Organisation attention
- Property posture attention
- Project risk
- Finance attention
- Platform attention

A group must remain explainable down to source items.

## Dashboard and My Work
Dashboard emphasizes business-wide/role-relevant attention.
My Work emphasizes items the current user/team is responsible for.

Do not duplicate source records; link back to them.

## Portal
Portal Home may show client-safe Attention items such as:
- approve deliverable
- pay invoice
- upload requested file
- domain renewal decision
- active incident
- contract awaiting signature

Internal risk reasoning must not leak to client users.

## Àríyá
Àríyá may summarize, rank and explain permitted Attention items, but deterministic source rules remain visible. AI inference may create a proposed Attention signal only when clearly labeled as AI-derived and governed by policy.

## Notifications
Attention state changes can create Notifications according to policy. Notifications do not own the Attention lifecycle.

## Automations
Attention events may trigger automations such as escalation, assignment, reminder, approval or incident creation.

## API/MCP
Expose permission-filtered operations such as:
- list_attention
- get_attention_item
- acknowledge_attention
- snooze_attention
- get_attention_summary

MCP/AI must not reveal hidden source evidence.

## Acceptance criteria
- attention remains linked to authoritative source conditions
- reading a notification does not falsely resolve attention
- cross-organisation/property filtering is enforced
- Dashboard/My Work/Portal can consume the same engine without duplicating domain data
- grouped attention remains explainable
- AI-derived signals are distinguishable from deterministic facts
