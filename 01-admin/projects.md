# Projects

## Purpose
Projects is Re:Solve's delivery operating system. It converts sold work, retainers, internal initiatives, and client requests into visible, accountable execution without becoming a generic task manager.

## Goals
- show what is being delivered, by whom, for whom, against what commitment
- make blockers, approvals, dependencies, deadlines, and client actions obvious
- preserve a clean client-safe view without exposing internal notes or sensitive data
- connect work to organisations, contacts, properties, services, commercial records, billing, files, vault items, support context, and outcomes
- support repeatable delivery through templates without forcing every project into the same shape

## Non-goals
- replace specialist engineering issue trackers for deep software development
- duplicate Chatwoot conversations
- become a personal notes app

## Core records
Project, Project Member, Task, Task Group, Milestone, Deliverable, Client Action, Dependency, Risk, Issue, Change Request, Time Entry, Expense Reference, Approval Request, Project Update, Project Template, Project Activity.

## Project types
Configurable. Initial examples: Website Build, Website Redesign, OJS Setup, OJS Upgrade, Journal Launch, Migration, Maintenance, Consulting, Incident Recovery, Internal Initiative, Retainer Workstream.

## Project lifecycle
Draft → Planned → Active → On Hold → At Risk → Completed → Archived.

Cancelled is terminal and must preserve history. Reopening requires permission and an audit reason.

## Record workspace
The Project 360 workspace contains:
- Overview
- Work
- Milestones
- Deliverables
- Client Actions
- Risks & Issues
- Changes
- Time & Cost
- Files
- Activity
- Automations
- Settings

Plugins may add approved tabs and widgets.

## Overview
Show only meaningful operational information:
- project status and health
- client and property context
- owner and delivery team
- start, target, and forecast completion
- next milestone
- current blockers
- approvals waiting
- client actions waiting
- budget/time consumption when permitted
- linked service/contract
- latest internal update and latest client-visible update

Health must be explainable. No unexplained red/yellow/green score.

## Work
Tasks support title, description, assignee, collaborators, status, priority, due date, estimate, time logged, task group, milestone, client visibility, dependencies, tags, checklist, attachments, comments, recurrence, automation metadata, and related records.

Suggested statuses: Backlog, Ready, In Progress, Blocked, Review, Waiting on Client, Done, Cancelled. Statuses are configurable by project template.

Views:
- List
- Board
- Timeline
- My Work filtered view
- Client-visible work view where enabled

Saved views, filters, bulk actions, keyboard navigation, and quick-edit are required.

## Milestones
Milestones represent meaningful delivery commitments, not arbitrary task buckets. Each can contain target date, owner, success criteria, linked tasks/deliverables, dependencies, client visibility, status, and completion evidence.

## Deliverables
A deliverable is a client-relevant output. It supports versions, files/links, owner, due date, review state, approval requirement, client comments, change request linkage, and final acceptance.

States: Draft → Internal Review → Ready for Client → Client Review → Approved / Changes Requested → Final.

## Client Actions
A first-class record for things Re:Solve needs from the client: content, access, approval, payment, decision, file, account, credentials, meeting, or other dependency.

Fields: request, owner contact, due date, project, property, priority, status, reminders, evidence, visibility, completion note.

States: Draft, Requested, Viewed, In Progress, Completed, Overdue, Waived.

Client Actions surface prominently in portal Home and project views.

## Risks and issues
Risk fields: description, likelihood, impact, owner, mitigation, trigger, review date, status.
Issue fields: description, severity, owner, root cause, resolution, related task/milestone/property/support incident.

## Change requests
Support scope changes without silently rewriting original commitments.

Fields: requested by, reason, scope impact, schedule impact, cost impact, affected deliverables, approval state, commercial linkage.

Approved changes can create proposal/estimate/invoice items or modify project baseline according to permission.

## Updates
Project Updates can be internal or client-visible. A client-visible update should summarize progress, completed work, next steps, blockers requiring client action, and revised dates where applicable.

AI may draft updates but a human remains responsible for sending unless explicitly configured otherwise.

## Permissions
Capabilities include projects.read, projects.create, projects.manage, projects.delete, projects.members.manage, tasks.manage, deliverables.manage, client_actions.manage, risks.manage, changes.manage, time.manage, financials.read, client_updates.publish, project_settings.manage.

Client permissions are separate and can be scoped to specific projects/properties.

## Notifications
Meaningful events include assignment, due soon, overdue, blocked, milestone risk, deliverable ready, approval requested/decided, client action requested/overdue, change request decision, status change, project at risk, and completion.

Do not notify on every task edit. Group and deduplicate related events.

## Automations
Examples:
- project created from accepted proposal
- template creates default work structure
- milestone approaching with incomplete blockers → notify owner
- task blocked for N days → escalate
- client action overdue → portal + email/WhatsApp according to policy
- deliverable approved → advance milestone
- project completed → trigger handover/closure checklist

## API
Expose CRUD and query APIs for projects, tasks, milestones, deliverables, client actions, risks, changes, updates, and time entries with filtering, pagination, scopes, audit, and idempotency for externally-created records.

## MCP
Candidate tools: search_projects, get_project, get_project_health, list_project_blockers, list_client_actions, create_task, update_task, draft_project_update, create_client_action, list_due_milestones. Write tools require explicit scopes; destructive operations are excluded by default.

## PWA/mobile
Phone experience prioritizes My Work, project summary, task updates, comments, client actions, approvals, file capture/upload, and status changes. Complex planning views may gracefully reduce to list/timeline summaries. Offline draft capture is allowed for comments/checklists where conflict-safe; financial or destructive actions require connectivity.

## Empty/error states
Every view must define loading, skeleton, empty, filtered-empty, partial data, permission denied, connector unavailable, offline, stale data, and failed mutation states.

## Acceptance criteria
- project health always shows reasons
- client cannot see internal-only tasks/comments/files
- completing a task never bypasses required deliverable approval
- cross-organisation and cross-property access is denied server-side
- overdue client actions surface in portal and configured notification channels
- all sensitive status/permission/change events are audited

## Lovable build slices
1. Projects list + create/edit + Project 360 overview
2. Tasks list/board + assignment/status flows
3. Milestones + deliverables
4. Client Actions + portal exposure
5. Risks/issues/change requests
6. time/cost + updates + advanced automations
