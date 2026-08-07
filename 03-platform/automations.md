# Re:Solve Automation Platform

## Purpose
Automations let Re:Solve react to Domain Events, schedules, verified Connector events and explicit invocations without scattering hidden one-off business logic throughout the product.

Plugins/Connectors may contribute triggers/actions, but execution, Action Registry policy, permissions, retries, Approval, Audit and observability remain centralized.

## Goals
- automate routine operational work visibly;
- prefer deterministic workflows;
- reuse registered Actions rather than duplicate mutations;
- keep failure/retry/debugging understandable;
- support AI-assisted classification/drafting only where controlled;
- extend safely through Plugins/Connectors.

## Core concepts
Workflow, Trigger, Condition, Branch, Registered Action/Automation Action, Delay/Wait, Approval Gate, Run, Step Run, Retry, Failure, Schedule and Context/Variables.

## Triggers
### Domain Events
Examples:
- organisation/client lifecycle changed;
- request created/triaged/completed;
- property.posture_changed;
- property.renewal_due/completed;
- monitoring.outage_confirmed/recovered;
- incident created/updated/resolved;
- project/task/milestone/client-action events;
- proposal/contract events;
- invoice/payment/billing events;
- approval events;
- Vault access/rotation events;
- File/Knowledge events;
- Attention created/resolved;
- data-quality issue created/resolved.

### Time
- fixed/recurring schedule;
- relative to record date;
- Reminder/cadence due;
- inactivity duration;
- SLA/renewal threshold.

### Connector
Only verified/normalized Integration Events become Connector triggers.

### Manual / API / MCP / Àríyá
Allowed only through explicitly registered invocation/Action policy.

### AI-assisted
AI may classify/extract/draft/score a bounded step. Downstream write still uses normal registered Action/permission/Approval.

## Conditions
Inspect approved context such as record fields/status, related records, dates/amounts, Organisation/Property scope, tags/taxonomy, Property Posture, Renewal state, Connector freshness, Attention state and actor context.

Avoid arbitrary unrestricted code in ordinary user-authored workflows.

## Actions
Prefer `03-platform/action-registry.md` definitions for reusable consequential mutations.

Examples:
- create/update supported record;
- assign owner/team;
- create Task/Request/Reminder/Client Action;
- request Approval;
- create Notification;
- create/resolve supported Attention when the domain rule permits;
- send approved email/WhatsApp operational message;
- generate Document Studio draft/render;
- create Secure External Access grant;
- invoke permitted Connector/Plugin Action;
- update lifecycle/status/tag/custom field;
- wait/delay/branch/stop.

Dangerous financial, Vault, production DNS/registrar, access and destructive Actions inherit their confirmation/Approval/step-up requirements and cannot be weakened by Automation configuration.

## Workflow / Run states
Workflow: Draft, Validating, Active, Paused, Disabled, Error, Archived.

Run: Queued, Running, Waiting, Awaiting Approval, Retrying, Succeeded, Partially Succeeded, Failed, Cancelled, Expired.

## Builder UX
Operations -> Automations:
- Workflows
- Recipes/Templates
- Runs
- Scheduled Jobs
- Failures
- Action Catalogue

Use Re:Solve Core UI. A clear vertical builder is preferred for simple flows; React Flow/node canvas may be used only where branching complexity genuinely benefits from it.

Each step displays type, label, input summary, source/target, required capability/risk, failure policy and output variables.

## Validation / testing
Before activation:
- validate schemas/branches;
- inspect missing permissions/Connector/Plugin dependencies;
- detect unsafe recursion/cycles;
- preview registered Actions/consequences;
- test using fictional/sample record;
- test Connector Action safely where supported;
- identify stale/unavailable source assumptions.

## Run-as / authorization
A Workflow has an explicit execution Principal/service identity or tightly defined run-as model.

Creating/editing a Workflow does not grant arbitrary future execution authority.

At execution, Actions recheck relevant capability/scope and current target conditions according to their contract.

A user-triggered Automation must not elevate the invoking User merely because the workflow was authored by an administrator.

## Failure / retry / idempotency
Per step/workflow support stop, retry/backoff, continue/partial, failure branch or human intervention.

External side effects use idempotency keys/Connector semantics where available. Retries must not duplicate invoices, messages, guest links, payments/refunds or other consequential effects.

## Approval gates
Approval captures exact proposed Action/evidence/version. Approval success allows workflow to resume, but downstream Action still verifies current state and may fail safely if context changed.

## Attention
Automation failure requiring human intervention may create Attention.

Automations can react to Attention events or invoke supported domain Actions that resolve source conditions, but should not arbitrarily mark Attention resolved when the underlying condition remains true.

## Notifications / communications
Automation requests delivery through core Notification/Communications platforms. It does not send directly through random SDKs.

## Documents
Document generation may create drafts/renders. Sending Proposal/Contract, executing signatures or accepting commercial terms remains controlled by corresponding Action/Approval policies.

## Monitoring / Renewals
Examples:
- confirmed outage -> create/link Incident;
- stable recovery -> update Incident/resolution workflow;
- Renewal threshold -> assign owner/create Request/notify client;
- stale backup heartbeat -> Technical Attention;
- Maintenance begins -> annotate/suppress eligible alerts.

## Permissions
Canonical examples:
- `automations.read`
- `automations.create`
- `automations.edit`
- `automations.activate`
- `automations.run`
- `automations.runs.read`
- `automations.runs.retry`
- `automations.settings.manage`

Underlying Actions require their own capabilities/service-identity grants.

## Audit / observability
Append-only Audit for Workflow lifecycle/permission/high-impact actions. Operational Run history shows step states, safe inputs/outputs, correlation, retries, provider/source references and errors without leaking secrets.

## API / MCP / Àríyá
APIs expose Workflow state, run history, manual triggers/retry/cancel/templates as permitted.

MCP/Àríyá may inspect/run only specifically allowed workflows/Actions; broad agent scopes do not receive arbitrary Workflow editing/execution by default.

## Plugins / Connectors
Plugins register namespaced triggers/Actions/validators/templates/renderers.
Connectors register verified Event triggers and provider-backed Actions.

All contributions use central Principal/permission, Action, Audit, retry and health contracts.

## PWA/mobile
Mobile supports list/status/run inspection, Approval/human intervention, pause/enable where permitted. Complex builder may be desktop/tablet optimized with explicit mobile read-only state.

## Explicit exclusions
Automation does not introduce HR, employee scheduling, Timesheets/Time Tracking or Client Service Consumption workflows as core product concepts.

## Acceptance criteria
- every Workflow is visible/diagnosable;
- reusable mutations use Action Registry;
- high-impact Action policy cannot be weakened by Automation;
- retries are idempotent where required;
- Approval gates preserve evidence and downstream revalidation;
- Connector events are verified before trigger;
- failures can create actionable Attention;
- Plugin/Connector extensions inherit controls;
- no excluded HR/Timesheet/service-consumption behavior appears.

## Lovable build slices
1. Workflow/Run records + list/detail.
2. simple event/condition/registered-action builder.
3. deterministic execution runtime.
4. schedules/delays/reminders.
5. retry/failure/run inspector + Attention.
6. Approval gates.
7. Plugin/Connector Action contributions.
8. templates + advanced branching/React Flow only if justified.
