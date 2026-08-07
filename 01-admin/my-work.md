# My Work

## Purpose
My Work is the staff User's personal execution center. It consolidates assigned/owned actionable work from source records without creating shadow records or requiring module hopping.

It is distinct from Notifications and from the broader Attention Engine:
- Notification = awareness/delivery;
- Attention = unresolved condition;
- My Work = current user's responsibility/action projection.

## Primary inputs
My Work may project permitted items from:
- Tasks / recurring Task occurrences;
- Approvals;
- Requests;
- Client Actions;
- Reminders;
- Mentions;
- Renewal/Expiry Obligations;
- onboarding/offboarding steps;
- commercial follow-up/cadences;
- Incidents assigned to the user;
- Data Quality issues assigned for review;
- plugin-provided work providers.

No Timesheet, Time Entry, employee utilization or HR work items exist.

## Core principles
- personal accountability first;
- every item links to an authoritative source record;
- completing work updates the source record through registered Actions;
- projections are deduplicated/grouped when one source appears in several contexts;
- waiting versus actionable versus overdue is explicit;
- inaccessible source data never leaks through title/count/context;
- My Work can consume Attention but does not replace it.

## Main views

### Focus
Small, ranked set of highest-priority actionable items. Strong mobile/default workflow.

### Today
Due/scheduled today:
- Tasks;
- Reminders;
- Approvals;
- Requests/follow-ups;
- Renewal actions;
- meetings/bookings/calendar commitments.

### Overdue
Always prominent when non-empty. Show source type, title, Organisation/Property/Project context, due age, priority, owner/source and next action.

### Upcoming
Configurable horizon such as next 7 days.

### Waiting
Cannot proceed because another person/system/dependency is outstanding.

Examples:
- waiting on client approval/file/credential;
- waiting on payment;
- waiting on external Connector/provider;
- waiting on teammate decision.

Waiting is not overdue unless its explicit waiting deadline/threshold is exceeded.

### Approvals
Current User's pending decisions.

### Requests
Assigned Requests, clarification needed and triage work.

### Renewals
Renewal/Expiry Obligations for which the current User is responsible.

### Mentions
Meaningful direct Mentions from shared Collaboration.

### Reminders
Personal/system Reminders, including snoozed items reaching their time.

### Recently Completed
Short optional confirmation/reopen history where source workflow permits.

## Presentation modes
- Focus
- List
- Calendar/Agenda
- Group by source/Organisation/Property

Saved Views may persist filters/presentation without expanding root navigation.

## Filters
Type, due state, priority, Organisation, Property, Project, Team, source domain, waiting/actionable, created/requested by and Saved View.

## Normalized projection contract
A projection may include:
- source type/id/reference;
- work type;
- assigned Principal/User/Team;
- title/summary;
- due/start time;
- priority;
- actionable/waiting state;
- Organisation/Property/Project context;
- Attention link where relevant;
- primary Action id/capability;
- deep link;
- source freshness/provenance when relevant;
- created/updated.

Do not copy sensitive source bodies merely to render a work item.

## Actions
Depending on source and permission:
- complete;
- start;
- acknowledge;
- snooze Reminder;
- reschedule;
- reassign;
- comment/reply;
- request clarification;
- approve/reject/request changes;
- open Renewal action;
- open source.

Every mutation routes to the source record/Action Registry and rechecks authorization.

## Calendar / Agenda
May aggregate:
- Task due dates;
- meetings/bookings;
- Milestones;
- Reminders;
- Renewal dates;
- Maintenance windows;
- scheduled commercial/client follow-ups.

External calendar items show provider/source and read-only/editable authority clearly.

No employee shift/leave/attendance scheduling.

## Attention relationship
If an Attention Item is personally assigned/relevant, My Work can project it or its source action. Resolution follows the underlying source condition.

Example: `Domain renewal due` remains Attention until renewed/closed, even if the User opened or snoozed its My Work projection.

## Notifications
Assignments, due/overdue, reassignments, direct Mentions, Approval, dependency resolution and Reminder events may create Notifications according to policy. My Work itself is not an inbox.

## Àríyá
Àríyá may:
- summarize today's work;
- explain why an item is prioritized;
- help draft a response/update;
- propose reschedule/reassignment/registered action.

It uses current source permission and evidence.

## API / MCP
Expose personal/team permitted work projection, complete/action endpoints via source Actions, Reminder creation, filters/Saved Views and agenda.

MCP candidates:
- get_my_work
- get_overdue_work
- get_today_schedule
- get_my_renewals
- get_my_requests
- complete_task
- reschedule_task
- create_reminder

## Responsive/PWA
Mobile Focus is a primary experience. Use touch-friendly rows/cards and contextual sheets, not dense desktop tables.

Safe cached work can display with stale timestamp. Offline mutation is queued only when the specific Action is replay-safe/idempotent; otherwise show online requirement.

## Accessibility
Keyboard-operable items/actions, semantic priority/status, screen-reader announcements and accessible list alternative for Calendar.

## Plugins
Plugins may register work providers only when they map to the normalized projection and provide secure source links/Actions.

## Acceptance criteria
- User sees personally actionable work across domains;
- source records remain authoritative;
- Waiting/Overdue/Actionable are distinct;
- Requests/Renewals/Reminders integrate without duplicate shadow data;
- hidden source data cannot leak;
- mobile Focus is excellent;
- no Timesheet/HR/Client Service Consumption work appears.

## Lovable build slices
1. Focus + Today + Overdue with fictional projections.
2. Upcoming + Waiting.
3. Approvals + Requests + Renewals + Mentions + Reminders.
4. filters/Saved Views.
5. Agenda/Calendar integration.
6. Attention/Àríyá summary integration.
7. mobile/PWA/offline-safe behavior.
