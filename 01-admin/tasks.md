# Admin — Tasks

## Purpose
Tasks is the staff User's execution center. It consolidates actionable work from authoritative source records without creating shadow business truth or forcing constant module hopping.

The former product name `My Work` is deprecated. The canonical destination and product term is **Tasks**.

Tasks is distinct from Notifications and Attention:
- Notification = awareness/delivery;
- Attention = unresolved condition;
- Task/work projection = actionable responsibility for a person/team.

## Primary inputs
Tasks may contain/project permitted items from:
- native Tasks and recurring Task occurrences;
- Approvals;
- Requests;
- Client Actions;
- Reminders;
- Mentions;
- Renewal/Expiry Obligations;
- onboarding/offboarding steps;
- commercial follow-up/cadences;
- Incidents/Property Health work;
- Data Quality review;
- Ariya-created/proposed Tasks when policy permits;
- plugin-provided work providers.

No Timesheet, Time Entry, work timer, employee utilization or HR work items exist.

## Core principles
- personal/team accountability first;
- every projection links to an authoritative source record;
- completing work updates the source through its registered Action;
- deduplicate/group one underlying source that appears in several contexts;
- actionable, waiting, overdue and blocked are explicit;
- hidden source data never leaks through counts/titles/context;
- Tasks can consume Attention but does not replace it.

## Main views
### Focus / Assigned to me
Small ranked set of highest-priority actionable items. Strong mobile/default workflow.

### Today
Due/scheduled today, including Tasks, Reminders, Approvals, Requests/follow-ups, renewals and Calendar commitments.

### Overdue
Prominent when non-empty. Show source, Organisation/Property/Project context, due age, priority and next action.

### Upcoming
Configurable future horizon.

### Waiting on client / dependency
Explicit non-actionable state with dependency/deadline context.

### Approvals / Requests / Renewals / Mentions / Reminders
Saved/system views over the same work projection rather than separate root modules.

### Property Health
Assigned remediation/incident/renewal work sourced from Monitoring/Posture/Incidents.

### Ariya-created
Work Ariya created through an approved policy/Action, with source evidence and reason.

### Recently completed
Short confirmation/history where the source workflow permits it.

## Presentation
Focus, list, calendar/agenda and group-by Organisation/Property/Project/source. Saved Views persist filters/columns/presentation.

## Normalized projection contract
A projection may include source type/id/reference, work type, assigned Principal/User/Team, title, due/start time, priority, actionable/waiting state, Organisation/Property/Project context, Attention link, primary Action id, deep link, freshness/provenance and timestamps.

Do not copy sensitive source bodies merely to render a Task projection.

## Actions
Depending on source/permission: complete, start, acknowledge, snooze, reschedule, reassign, comment/reply, request clarification, approve/reject/request changes, open renewal/remediation, or open source.

Every mutation routes to the authoritative source/Action Registry with fresh authorization.

## Calendar relationship
Tasks/Agenda may aggregate Task dates, meetings/bookings, Milestones, Reminders, Renewals, Maintenance and commercial follow-ups. No employee shift/leave/attendance scheduling.

## Ariya
Ariya may summarize work, explain prioritization, identify blockers, draft responses, recommend next actions, create a Task when authorised and Watch conditions that should create future work.

Important suggestions link to evidence. Ariya cannot invent completion or bypass assignment/Action policy.

## API / MCP
Examples: `get_my_tasks`, `get_overdue_tasks`, `get_today_schedule`, `get_my_renewals`, `complete_task`, `reschedule_task`, `create_task`, `create_reminder`.

## Responsive/PWA
Mobile Focus is a primary experience. Use touch-friendly rows/cards/sheets rather than forcing dense desktop tables. Private task data follows the explicit PWA privacy/cache policy.

## Acceptance criteria
- staff can see personally actionable work across domains;
- source records remain authoritative;
- Waiting/Overdue/Actionable are distinct;
- hidden source data cannot leak;
- Saved Views reduce navigation sprawl;
- Ariya-created work preserves evidence/provenance;
- mobile Focus is excellent;
- no HR/Timesheet/work-timer/consumption work appears.

## Build slices
1. Focus/Today/Overdue.
2. Upcoming/Waiting + filters/Saved Views.
3. Approval/Request/Renewal/Property Health projections.
4. Calendar/Agenda integration.
5. Ariya/Attention integration.
6. mobile/PWA/accessibility polish.
