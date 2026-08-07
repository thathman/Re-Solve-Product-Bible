# Client Portal — Projects

## Purpose
Provide clients a trustworthy, calm view of delivery progress, decisions, deliverables and responsibilities without exposing internal execution noise.

## Primary flows
- browse active/completed projects
- understand status, progress and next milestone
- review deliverables
- complete client actions
- approve/reject where permitted
- review change requests and key decisions
- access shared files and updates

## Project list
Show project name, linked property/service, status, progress, next milestone, due date, client action count, latest update and health indicator. Filters: active, waiting on client, at risk, completed, property, service, owner.

## Project workspace
Sections:
- Overview
- Timeline/Milestones
- Deliverables
- Client Actions
- Approvals
- Change Requests
- Files
- Updates
- Activity

Overview includes project objective, scope summary, status, progress, key dates, current phase, next event, visible blockers, client responsibilities and account/project contacts.

## Client actions
Client actions are first-class records with owner, due date, instructions, evidence/attachment, completion state and related project/milestone. They feed Portal Home, Notifications and My Work for staff.

## Deliverables and approvals
Deliverables may be previewed/downloaded where supported. Approval flows record decision, actor, timestamp, optional comment and version being approved. Revisions create new versions rather than mutating approved evidence.

## Change requests
Show request, reason, impact summary, price/time impact where client-visible, decision state and resulting scope changes.

## Visibility
Internal notes, staff tasks, private risk commentary, private costs and internal-only files are never exposed merely because they belong to the same project.

## Notifications
Examples: client action assigned/due, deliverable ready, approval requested, milestone reached, update posted, change request needs decision, project completed.

## API / MCP
Client API is permission-filtered. MCP examples: list_my_projects, get_my_project, list_my_project_actions, get_deliverable_status, submit_project_action. Write tools require explicit scope and audit.

## Mobile/PWA
Timeline and tables collapse into cards/steppers. Approval and action flows must work comfortably from a phone. Cached project summaries may be read offline; mutating actions require connectivity unless a safely queued workflow is explicitly implemented.

## Lovable build slices
1. Project list and workspace overview.
2. Milestones/timeline and updates.
3. Client actions.
4. Deliverables/approvals.
5. Change requests/files/activity and mobile polish.