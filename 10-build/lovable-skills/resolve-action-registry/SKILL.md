---
name: resolve-action-registry
description: Use when defining or changing a reusable Re:Solve business action that may appear in UI menus, Command Palette, Àríyá, API, MCP, Automations, plugins, or connectors.
---

# Re:Solve Action Registry

Read `03-platform/action-registry.md`, canonical permissions, Approvals, security, API/MCP and the source domain spec.

## Purpose
One business action should not be independently reimplemented for UI, Àríyá, API, MCP and Automations.

## Action contract
Define:
- stable action id and human label;
- domain/target record types;
- required inputs and validation;
- required capability and scope;
- risk class;
- availability/context rules;
- confirmation copy;
- approval/step-up requirement;
- idempotency/concurrency behavior;
- domain side effects/events;
- audit policy;
- API/MCP exposure policy;
- UI placement hints where appropriate;
- offline eligibility;
- success/failure result contract.

## Risk
Distinguish ordinary reads, low-risk writes, sensitive writes and destructive/high-impact actions. Risk classification must drive confirmation/approval/step-up rather than visual styling alone.

## Authorization
Check at execution time using current Principal, capability, scope and target. Discoverability in a menu or by Àríyá is never authorization.

## UI
Use consistent labels and consequence-focused confirmation. Avoid exposing actions that cannot possibly run in the current context unless explaining access/request path is useful.

## AI/automation
Àríyá and Automations invoke registered actions, not hidden provider/database shortcuts. Human confirmation/approval rules remain effective.

## Completion
Verify the action has one canonical execution path, safe retries where applicable, auditable side effects, permission-negative tests and consistent behavior across every exposed surface.