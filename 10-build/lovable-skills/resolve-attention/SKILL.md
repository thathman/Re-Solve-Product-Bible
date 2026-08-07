---
name: resolve-attention
description: Use when defining, generating, displaying, resolving, snoozing, prioritizing, or aggregating Re:Solve Attention Items for Dashboard, My Work, Portal Home, Àríyá briefings, renewals, incidents, finance, approvals, or system operations.
---

# Re:Solve Attention Engine

Read `03-platform/attention-engine.md`, Notifications, Dashboard/My Work/Portal Home and the source domain spec.

## Core distinction
Attention is an unresolved condition that matters now. Notification is awareness/delivery of an event. Do not use unread notification state as the source of truth for whether a business condition is still unresolved.

## Attention contract
Define:
- attention type/key;
- source record(s);
- organisation/property/project context;
- reason/evidence;
- priority/severity;
- owner/assignee or recipient resolution;
- detected/started/due timestamps;
- recommended/registered action;
- resolve condition;
- snooze/reopen behavior;
- dedup/grouping behavior;
- client visibility;
- source/freshness where derived;
- Àríyá summarization eligibility.

## Lifecycle
Attention should resolve because the underlying condition is fixed, waived, expired or explicitly resolved under policy—not merely because a user clicked read.

## Noise control
Deduplicate repeated provider signals. Prefer one explainable item with changing evidence over many near-identical alerts. Escalate only when policy says the condition became more urgent.

## UI
Use canonical `AttentionItem` across Dashboard/My Work/Portal surfaces with clear reason, context, age/due state and next action. Priority must not rely on color alone.

## Permissions
Attention projections must not leak inaccessible records through titles, counts or summaries. Portal gets client-safe language and evidence only.

## Completion
Verify creation, dedupe, snooze, underlying-condition resolution, reopen/escalation, permission filtering and Notification relationship.