# Re:Solve Automation Platform

## Purpose

Automations let Re:Solve react to business events, time, connector events, and explicit user actions without embedding one-off rules throughout the product.

The automation engine is a shared platform primitive. Plugins and connectors may contribute triggers/actions, but execution, permissions, retries, audit, and observability remain centralized.

## Goals

- make routine operational work configurable
- keep automation logic visible and auditable
- support deterministic actions first, AI-assisted actions where explicitly allowed
- prevent hidden background logic from becoming impossible to debug
- let plugins/connectors extend the engine safely

## Core concepts

- Workflow
- Trigger
- Condition
- Branch
- Action
- Delay/Wait
- Approval Step
- Run
- Step Run
- Retry
- Failure
- Schedule
- Variable/Context

## Trigger classes

### Record events
- organisation.created/updated
- contact.created/updated
- property.created/health_changed
- project.created/status_changed/completed
- task.created/assigned/due/overdue/completed
- invoice.created/sent/due/overdue/paid
- payment.confirmed/failed/refunded
- approval.requested/completed
- vault.access_requested/granted/revoked/revealed
- file.uploaded/shared

### Time
- fixed schedule
- recurring schedule
- relative to record date
- inactivity duration
- SLA threshold

### Connector
Only verified normalized connector events may trigger workflows.

### Manual
- button/action from UI
- API request
- MCP tool where permitted

### AI
AI may propose or classify an automation input, but any write/action still follows normal permission and workflow controls.

## Condition system

Conditions can inspect allowed workflow context such as:
- record fields
- related record fields
- status
- dates
- amount ranges
- organisation/property membership
- tags
- health state
- connector state
- actor role

Avoid arbitrary code expressions in normal user-authored workflows.

## Actions

Core actions may include:
- create/update record
- assign owner
- create task
- create reminder
- request approval
- create notification
- send email
- send WhatsApp operational message
- call permitted connector action
- run plugin action
- generate document
- create portal action item
- set status/tag/field
- wait/delay
- branch
- stop workflow

Potentially dangerous actions must declare confirmation/approval requirements.

## Workflow states

- draft
- validating
- active
- paused
- disabled
- error
- archived

## Run states

- queued
- running
- waiting
- awaiting_approval
- retrying
- succeeded
- partially_succeeded
- failed
- cancelled
- expired

## Builder experience

Admin > Automations should include:
- Workflows
- Templates
- Runs
- Scheduled Jobs
- Failures

Workflow builder should show a clear vertical or node-based flow without becoming visually gimmicky.

Each step displays:
- type
- label
- input summary
- permission requirements
- failure policy
- output variables

## Testing

Before activation users should be able to:
- validate workflow
- inspect missing permissions/configuration
- run against demo/sample record
- preview resulting actions
- test individual connector/action where safe

## Failure policy

Per action/workflow:
- stop immediately
- retry
- continue and mark partial failure
- route to failure branch
- request human intervention

Retries use central job runtime.

## Idempotency

Automations triggered by external events or retries must minimize duplicate side effects.

Actions that create external side effects should support idempotency keys where available.

## Human approvals

Workflows may pause for approval. Approval records must preserve:
- requested action
- requester/workflow
- approver
- deadline
- decision
- comment
- resulting run continuation

## Notifications

Automation notifications are generated through the Notification Platform. Workflow authors choose from permitted notification actions rather than implementing delivery directly.

## Permissions

Examples:
- automations.read
- automations.create
- automations.edit
- automations.activate
- automations.run
- automations.view_runs
- automations.retry

A workflow may execute only actions permitted by its service identity/configuration. User permissions to create a workflow do not automatically grant arbitrary execution rights.

## Audit

Audit:
- workflow created/edited
- activated/paused
- permission changed
- manual run
- retry/cancel
- destructive action
- approval step

Run history remains operationally searchable.

## API

Expose:
- workflow listing/detail
- enable/disable where permitted
- run history
- manual trigger
- retry/cancel
- templates

## MCP

MCP may:
- list permitted workflows
- inspect workflow status
- run explicitly AI-allowed workflows
- inspect runs

Do not expose arbitrary workflow creation/editing to broad AI scopes by default.

## Plugins/connectors

Plugins can register triggers, actions, validators, templates, and step renderers.
Connectors can register verified event triggers and permitted action capabilities.

All contributions use central runtime, logs, permissions, and health.

## PWA/mobile

Mobile supports:
- workflow list/status
- run inspection
- pause/enable where permitted
- approval/action on failed runs

Complex visual editing may use an optimized desktop/tablet builder with an explicit mobile read-only state rather than a broken canvas.

## Acceptance criteria

- workflow has observable trigger, conditions, steps, and outputs
- validation catches missing connector/plugin/configuration dependencies
- failed runs are diagnosable and retryable
- duplicate external events do not create duplicate business side effects when idempotency applies
- approvals pause/resume correctly
- every action passes permission/audit policies
- plugin/connector actions run through central runtime

## Lovable build slices

1. workflow/run data model + list/detail
2. simple trigger-condition-action builder
3. execution engine for core deterministic actions
4. schedules/delays
5. retries/failures/run inspector
6. approvals
7. plugin/connector action registry
8. templates and advanced branching
