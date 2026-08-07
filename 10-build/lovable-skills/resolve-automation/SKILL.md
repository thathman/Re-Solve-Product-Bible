---
name: resolve-automation
description: Use when designing, implementing, reviewing, or debugging a Re:Solve automation/workflow with triggers, conditions, branches, delays, approvals, connector/plugin actions, retries, or run history.
---

# Re:Solve Automation

Read `03-platform/automations.md`, Action Registry, Approvals, Notifications, connector/plugin contracts, security and the affected domain specs.

## Model
Automation uses explicit Trigger → Conditions/Branches → Actions/Wait/Approval → Result. Do not bury business automation in page components or unmanaged cron jobs.

## Trigger
Declare event/time/manual/connector trigger, source event schema, scope and idempotency expectations.

## Conditions
Use allowed structured record/context fields. Avoid arbitrary user-authored code expressions in ordinary workflows.

## Actions
Prefer registered Actions so UI, Àríyá, API/MCP and Automations share permission/risk behavior. Each action declares inputs, output, required capabilities, side effects, retry/idempotency and failure policy.

## Human gates
Sensitive/high-impact actions may pause on Approval. Preserve request, evidence/version, approver, deadline, decision and continuation link.

## Reliability
Every run and step has observable state. Support retry/backoff, partial failure policy, dead-letter/human intervention and safe cancellation. External side effects must be deduplicated where retried.

## Builder
Prefer clear vertical flow for simple workflows. Use React Flow-style canvas only when branching complexity justifies it. Do not turn the builder into a decorative node playground.

## Testing
Before activation validate dependencies/permissions/configuration, preview actions, and run safely against demo/sample data where possible.

## Security
Workflow configuration does not grant arbitrary execution authority. Execution identity/scopes remain explicit and every sensitive action is audited.

## Completion
Verify failed runs are diagnosable, duplicate events do not duplicate effects, missing connector/plugin dependencies are visible, approvals pause/resume correctly, and mobile provides at least safe run/status/approval operations even if complex editing remains desktop-focused.