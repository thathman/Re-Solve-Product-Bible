# My Work

## Purpose

My Work is the staff member's personal execution center. It consolidates assigned tasks, reminders, approvals, mentions, client actions, scheduled follow-ups, calendar commitments, and other personally actionable items into one coherent queue.

It must reduce context switching. Users should not need to visit Projects, CRM, Billing, Approvals, and Notifications separately just to understand what they personally owe.

## Primary users

All authenticated staff users with assigned work.

## Core principles

- Personal accountability first.
- Every item has a source record.
- One work item should not be duplicated across multiple categories unless explicitly grouped.
- Due state and urgency must be explainable.
- Completing work from My Work must update the source record, not create a shadow status.
- Notifications may bring a user to My Work, but My Work is not a notification inbox.

## Main sections

### Today

Includes:
- due today
- scheduled today
- reminders due today
- approvals due today
- follow-ups due today

### Overdue

Always visible when non-empty.

Each item displays:
- item type
- title
- related organisation
- related property/project
- due date/time
- overdue duration
- priority
- owner
- source
- next action

### Upcoming

Default horizon configurable, e.g. 7 days.

### Waiting

Items where the user cannot proceed because another actor or dependency is outstanding.

Examples:
- waiting for client approval
- waiting for payment
- waiting for credential
- waiting for teammate

Waiting items should not look overdue unless an explicit wait deadline has passed.

### Approvals

Approvals requiring the current user's decision.

### Mentions & Requests

Includes meaningful @mentions and direct requests for action, not every conversational mention.

### Reminders

User-created and system-created reminders.

### Recently Completed

Short, optional retrospective view to confirm completion and allow quick reopen where permitted.

## Views

Users can switch between:
- Focus
- List
- Calendar
- Grouped by source

Focus mode shows a small number of highest-priority actionable items.

## Filters

- type
- due state
- priority
- client
- property
- project
- team
- source module
- waiting/actionable
- created by

Saved views supported.

## Item actions

Depending on type and permission:
- complete
- start
- snooze reminder
- reschedule
- reassign
- comment
- request clarification
- approve/reject
- open source

Destructive or materially consequential actions require confirmation where appropriate.

## Work item model

My Work should be an aggregation contract rather than one universal table replacing source records.

A normalized work projection should support:
- source_type
- source_id
- work_type
- assigned_user/team
- title
- due_at
- priority
- state
- organisation_id
- property_id
- project_id
- action capability
- deep link
- created_at
- updated_at

## Calendar interaction

Calendar view may include:
- task due dates
- meetings
- milestones
- scheduled follow-ups
- reminders
- maintenance windows

External calendar data may be connected, but Re:Solve must identify which items are editable in Re:Solve and which are external/read-only.

## Notifications

Relevant events:
- item assigned
- due soon
- overdue
- reassigned
- comment/request directed to user
- approval requested
- waiting dependency resolved

Users may configure delivery rules except for mandatory critical/security items.

## API

Expose:
- list my work
- list team work with permission
- complete supported work
- reschedule
- reassign
- create reminder
- saved views

## MCP candidates

- get_my_work
- get_overdue_work
- get_today_schedule
- complete_task
- reschedule_task
- create_reminder

Write operations need scoped permission and source-level authorization.

## Responsive/PWA

Mobile is a primary use case. The Focus view should be especially strong on mobile.

Offline:
- safely cached work list can display stale
- completion may be queued only for explicitly offline-safe actions
- conflicting updates require resolution when reconnecting

## Accessibility

- keyboard-completable work items
- screen-reader state announcements
- priority not conveyed by color alone
- calendar has accessible list alternative

## Extension slots

Plugins may contribute work providers if they map to the normalized work contract and supply source links/actions.

## Acceptance criteria

- User can see all personally actionable work across modules in one place.
- Completing an item updates its source record.
- Waiting items are distinguishable from overdue actionable work.
- No inaccessible source data leaks through work projections.
- Mobile Focus view is fully usable without desktop tables.
- Duplicate projections are grouped or deduplicated.

## Demo data

Include tasks, a project approval, a client follow-up, an overdue milestone action, a waiting credential request, a reminder, and recently completed work across at least three organisations.

## Lovable build slices

1. Focus + Today + Overdue with demo projections.
2. Upcoming + Waiting.
3. Approvals + Mentions + Reminders.
4. Filters/saved views.
5. Calendar view.
6. Mobile/PWA and offline behavior.
