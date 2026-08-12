# Projects

## Purpose
Projects is Re:Solve's delivery operating system. It converts sold work, recurring service work, internal initiatives and client Requests into visible accountable execution without becoming a generic task manager.

## Goals
- show what is being delivered, by whom, for whom and against what commitment;
- make blockers, Approvals, dependencies, deadlines and Client Actions obvious;
- preserve a clean client-safe view;
- connect work to Organisations, Contacts, Properties, Services, Proposals/Contracts, Billing, Requests, Files, Vault Items, Support and outcomes;
- support repeatable delivery through Project Templates and recurring work;
- expose Project Financial Plan/commercial health without Timesheets.

## Non-goals
- replace specialist engineering issue trackers;
- duplicate Chatwoot conversations;
- become a personal notes app;
- implement Timesheets/Time Tracking/work timers;
- implement employee utilization/HR performance management;
- become a statutory accounting ledger.

## Core records
Project, Project Member, Task, Recurring Task Definition, Task Group, Milestone, Deliverable, Client Action, Dependency, Risk, Issue, Change Request, Expense Reference, Approval Request, Project Update, Project Template, Project Financial Plan reference/context and Project Activity.

## Project lifecycle
Draft -> Planned -> Active -> On Hold -> At Risk -> Completed -> Archived.

Cancelled is terminal and preserves history. Reopening requires permission/Audit reason.

## Record workspace
Project 360 contains:
- Overview;
- Tasks / Work;
- Milestones;
- Deliverables;
- Client Actions;
- Requests / Changes;
- Risks & Issues;
- Financials / Cost & Commercial;
- Properties;
- Forms;
- Files;
- Communications / Collaboration / Activity;
- Automations;
- Settings.

Plugins may add approved tabs/widgets.

## Overview
Show:
- status and explainable health;
- client and Property context;
- owner/team;
- start, target and forecast completion;
- next Milestone;
- blockers;
- Approvals waiting;
- Client Actions waiting;
- open Requests/Changes;
- approved value/Billing/cost summary when permitted;
- linked Service/Contract/Proposal;
- latest internal/client-visible update.

Health shows reasons rather than an unexplained score.

## Tasks / Work
Tasks may support title, description, assignee, collaborators, status, priority, due date, estimate/effort note, group, Milestone, client visibility, dependencies, tags, checklist, Files, Collaboration, recurrence, Automation metadata and related records.

**Tasks do not record time logged or Timesheet entries.**

Suggested statuses: Backlog, Ready, In Progress, Blocked, Review, Waiting on Client, Done, Cancelled. Templates may configure statuses where semantics remain clear.

Views:
- List;
- Board;
- Timeline where useful;
- Assigned to me / Focus / Today through canonical Tasks views;
- client-visible work where enabled.

Saved Views, filters, permission-aware Bulk Actions, keyboard behavior and responsive alternatives use shared platform/Core UI contracts.

## Project Templates
Project Templates define reusable delivery blueprints for Milestones, Tasks, Approvals, dependencies, client-visible defaults, default durations, Forms/File Requests and Automation hooks.

Templates register in Template Center. A Project instantiated from Template Version v2 keeps that source/version reference after v3 is published.

Proposal/Service acceptance may instantiate a Project Template idempotently.

## Recurring work
Recurring Task Definitions create ordinary Task occurrences. Each occurrence remains independently inspectable/completable and follows shared recurrence rules.

## Milestones
Meaningful delivery commitments with target date, owner, success criteria, Tasks/Deliverables, dependencies, client visibility, status and evidence.

## Deliverables
Supports versions/Files/links, owner, due date, review state, Approval requirement, client comments, Change Request linkage and final acceptance.

States: Draft -> Internal Review -> Ready for Client -> Client Review -> Approved / Changes Requested -> Final.

## Client Actions
First-class client dependencies such as content, access, approval, payment, decision, File, credential or meeting.

Fields may include request, owner Contact, due date, Project, Property, priority, state, reminders, evidence and completion note.

Client Actions may be surfaced inside a Client Journey/Onboarding Pack without duplicating the underlying record.

## Requests and Change Requests
A Request may be linked/converted into Project work. Change Requests preserve modifications to agreed scope/timing/cost without rewriting the original commitment.

Approved Change Requests may create/modify Proposal/Billing/Financial Plan context through controlled Actions.

## Risks and Issues
Risk: description, likelihood, impact, owner, mitigation, trigger, review date, status.

Issue: description, severity, owner, root cause, resolution and related Project/Property/Incident context.

## Project Financial Plan / Cost & Commercial
The detailed contract lives in [Project Financial Plan and Commercial Health](project-financials.md).

Where permitted, Project shows authoritative/derived:
- original accepted Proposal/Contract value;
- approved Change Request additions/reductions;
- current approved value;
- linked Invoice totals;
- paid/outstanding/remaining-to-invoice;
- approved explicit external/operational cost budget;
- actual Project-linked Expenses/costs;
- expected/current gross margin only where inputs/currency basis are valid.

Do not infer labor cost from Timesheets because Re:Solve has none. Unlike currencies are not silently aggregated.

## Project updates
Internal or client-visible status updates summarize progress, completed work, next steps, blockers/client actions and revised dates.

Ariya may draft updates; user/approved workflow remains responsible for publishing/sending.

## Collaboration / Communications
Use shared Comments/Mentions/Following and record-linked Communications. Internal Notes/cost/margin remain hidden from Portal.

## Attention
Examples:
- Milestone at risk;
- blocked Task overdue;
- Client Action overdue;
- Approval waiting;
- Request/Change waiting;
- Project health at risk;
- approved work not invoiced;
- explicit costs exceed approved cost budget where policy enables it.

## Permissions
Capabilities may include projects.read/create/manage/archive, projects.members.manage, tasks.manage, deliverables.manage, client_actions.manage, risks.manage, changes.manage, project_financials.read/manage, client_updates.publish and project_settings.manage.

No time-tracking capability exists.

## Notifications
Assignment, due/overdue, blocked, Milestone risk, Deliverable/Approval, Client Action, Change Request, Project risk and completion. Do not notify every Task edit.

## Automations
Examples:
- accepted Proposal -> instantiate Project from Template;
- Milestone approaching with blockers -> Attention/notify owner;
- recurring Task due -> generate occurrence;
- client action overdue -> Portal + configured channel;
- Deliverable approved -> advance workflow;
- approved Change Request -> update Project financial/commercial flow;
- Project completed -> create handover/review Client Journey.

## API / MCP / Ariya
Expose Projects, Tasks, Milestones, Deliverables, Client Actions, Risks, Changes, updates and permitted financial summary with normal authorization/pagination/Audit.

Candidate tools: `search_projects`, `get_project`, `get_project_health`, `get_project_financial_summary`, `list_project_blockers`, `list_client_actions`, `create_task`, `update_task`, `draft_project_update`, `list_due_milestones`.

No Timesheet/Time Entry tools exist.

## PWA/mobile
Phone prioritizes Tasks, summary, Task updates, comments, Client Actions, Approvals, Files and status changes. Complex planning/financial detail can reduce gracefully. Sensitive financial/destructive actions require connectivity/strong confirmation where policy requires it.

## Acceptance criteria
- health is explainable;
- client cannot see internal-only work/comments/files/cost/margin;
- Task completion cannot bypass required Approval;
- cross-scope access is denied server-side;
- overdue Client Actions feed Portal/Attention/Notifications;
- Project Templates preserve version/provenance;
- Project financial state links to authoritative Sales/Billing/Expense truth;
- unlike currencies do not produce false margin;
- sensitive status/permission/change events are audited;
- no Timesheet/Time Tracking/work-timer behavior appears.

## Build slices
1. Projects list + create/edit + Project 360 overview.
2. Tasks list/board + assignment/status/recurrence.
3. Milestones + Deliverables.
4. Client Actions + Portal/Client Journey exposure.
5. Requests/Risks/Issues/Change Requests.
6. Project Templates + Template Center integration.
7. Financial Plan/Billing/Expense context.
8. updates/advanced Automations/Ariya/mobile polish.
