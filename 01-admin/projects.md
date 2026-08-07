# Projects

## Purpose
Projects is Re:Solve's delivery operating system. It converts sold work, retainers, internal initiatives and client Requests into visible accountable execution without becoming a generic task manager.

## Goals
- show what is being delivered, by whom, for whom and against what commitment;
- make blockers, approvals, dependencies, deadlines and Client Actions obvious;
- preserve a clean client-safe view;
- connect work to Organisations, Contacts, Properties, Services, commercial records, Billing, Requests, Files, Vault Items, Support context and outcomes;
- support repeatable delivery through templates and recurring work;
- expose project cost/commercial context without Timesheets.

## Non-goals
- replace specialist engineering issue trackers;
- duplicate Chatwoot conversations;
- become a personal notes app;
- implement Timesheets/Time Tracking;
- implement employee utilization/HR performance management.

## Core records
Project, Project Member, Task, Recurring Task Definition, Task Group, Milestone, Deliverable, Client Action, Dependency, Risk, Issue, Change Request, Expense Reference, Approval Request, Project Update, Project Template and Project Activity.

## Project lifecycle
Draft -> Planned -> Active -> On Hold -> At Risk -> Completed -> Archived.

Cancelled is terminal and preserves history. Reopening requires permission/audit reason.

## Record workspace
Project 360 contains:
- Overview
- Work
- Milestones
- Deliverables
- Client Actions
- Requests / Changes
- Risks & Issues
- Cost & Commercial
- Files
- Collaboration / Activity
- Automations
- Settings

Plugins may add approved tabs/widgets.

## Overview
Show:
- status and explainable health;
- client and Property context;
- owner/team;
- start, target and forecast completion;
- next milestone;
- blockers;
- approvals waiting;
- Client Actions waiting;
- open Requests/Changes;
- budget/cost/commercial summary when permitted;
- linked Service/Contract;
- latest internal/client-visible update.

Health must show reasons rather than an unexplained score.

## Work
Tasks may support title, description, assignee, collaborators, status, priority, due date, estimate/effort note, group, milestone, client visibility, dependencies, tags, checklist, Files, Collaboration, recurrence, automation metadata and related records.

**Tasks do not record time logged or Timesheet entries.**

Suggested statuses: Backlog, Ready, In Progress, Blocked, Review, Waiting on Client, Done, Cancelled. Templates may configure statuses.

Views:
- List
- Board
- Timeline where useful
- My Work
- client-visible work where enabled

Saved Views, filters, bulk actions, keyboard behavior and responsive alternatives use shared platform/Core UI contracts.

## Recurring work
Recurring Task Definitions create ordinary Task occurrences. Each occurrence remains independently inspectable/completable and follows the shared recurrence rules.

## Milestones
Meaningful delivery commitments with target date, owner, success criteria, tasks/deliverables, dependencies, client visibility, status and evidence.

## Deliverables
Supports versions/files/links, owner, due date, review state, approval requirement, client comments, Change Request linkage and final acceptance.

States: Draft -> Internal Review -> Ready for Client -> Client Review -> Approved / Changes Requested -> Final.

## Client Actions
First-class client dependencies such as content, access, approval, payment, decision, file, credential or meeting.

Fields may include request, owner Contact, due date, Project, Property, priority, state, reminders, evidence and completion note.

## Requests and Change Requests
A Request may be linked/converted into project work. Change Requests preserve modifications to agreed scope/timing/cost without rewriting the original commitment.

Approved changes may create/modify commercial records through controlled actions.

## Risks and Issues
Risk: description, likelihood, impact, owner, mitigation, trigger, review date, status.

Issue: description, severity, owner, root cause, resolution and related Project/Property/Incident context.

## Cost and commercial context
Where permitted show:
- project budget/approved value;
- approved expenses/costs;
- invoiced amount;
- paid amount;
- outstanding amount;
- approved Change Request value;
- simple margin/cost context only when inputs are meaningful.

Do not infer labor cost from Timesheets because Re:Solve does not have them.

## Project updates
Internal or client-visible status updates summarize progress, completed work, next steps, blockers/client actions and revised dates.

Àríyá may draft updates; user/approved workflow remains responsible for publishing/sending.

## Collaboration
Use shared Comments/Mentions/Following. Internal Notes remain hidden from Portal.

## Attention
Examples:
- milestone at risk;
- blocked task overdue;
- Client Action overdue;
- approval waiting;
- Request/change waiting;
- project health at risk.

## Permissions
Capabilities may include projects.read/create/manage/archive, projects.members.manage, tasks.manage, deliverables.manage, client_actions.manage, risks.manage, changes.manage, financials.read, client_updates.publish and project_settings.manage.

No `time.manage` capability exists.

## Notifications
Assignment, due/overdue, blocked, milestone risk, deliverable/approval, Client Action, Change Request, project risk and completion. Do not notify every task edit.

## Automations
Examples:
- accepted proposal -> create Project from template;
- milestone approaching with blockers -> Attention/notify owner;
- recurring task due -> generate Task occurrence;
- client action overdue -> Portal + configured channel;
- deliverable approved -> advance workflow;
- project completed -> handover/closure plan.

## API/MCP/Àríyá
Expose projects, tasks, milestones, deliverables, Client Actions, risks, Changes and updates with normal authorization/pagination/audit.

No Timesheet/Time Entry endpoints/tools are part of the Project API.

Candidate MCP tools include search_projects, get_project, get_project_health, list_project_blockers, list_client_actions, create_task, update_task, draft_project_update and list_due_milestones.

## PWA/mobile
Phone prioritizes My Work, summary, task updates, comments, Client Actions, approvals, Files and status changes. Complex planning views can reduce gracefully. Financial/destructive actions require connectivity where policy requires it.

## Acceptance criteria
- health is explainable;
- client cannot see internal-only work/comments/files;
- task completion cannot bypass required approval;
- cross-scope access is denied server-side;
- overdue Client Actions feed Portal/Attention/Notifications;
- sensitive status/permission/change events are audited;
- no Timesheet/Time Tracking behavior appears.

## Lovable build slices
1. Projects list + create/edit + Project 360 overview.
2. Tasks list/board + assignment/status/recurrence.
3. Milestones + Deliverables.
4. Client Actions + Portal exposure.
5. Requests/Risks/Issues/Change Requests.
6. Cost/commercial context + updates + advanced automations.
