# Platform — Approvals

## Purpose
Provide one reusable approval engine for decisions across projects, commercial records, expenses, Vault access, change requests, automations and plugin-defined workflows.

## Approval Request
Core fields:
- id
- object_type / object_id
- request_type
- title / summary
- requested_by
- requested_at
- assigned approver(s)
- approver rule
- due_at
- status
- decision
- decision_comment
- decided_at
- version/evidence reference
- organisation/property/project context
- client-visible flag
- escalation policy

## States
Draft → Pending → Approved / Rejected / Cancelled / Expired. Optional multi-step flows may include In Review, Changes Requested or Escalated.

## Approval rules
Support:
- single approver
- any-of group
- all-of group
- ordered steps
- role-based approver resolution
- client approver designation
- threshold rules
- plugin-defined eligibility

Approver resolution is frozen or versioned at request time where required for auditability.

## UX
Approvals appear in My Work, Notifications, related record workspaces and Portal where client action is required. Decision UI must show exactly what is being approved, version/evidence, consequences and any required acknowledgement.

## Examples
- project deliverable approval
- proposal/estimate approval
- change request approval
- expense approval
- refund approval
- Vault access request
- automation high-risk action
- plugin-defined publishing approval

## Security & audit
Decision authority is checked at action time. Approval records are immutable evidence after decision except for controlled metadata corrections. Re-opening creates a new approval cycle rather than erasing history.

## Notifications
Requested, reminder, due soon, escalated, changes requested, approved, rejected, expired, cancelled.

## Automations
Approval completion can resume paused workflows, create tasks, issue documents, activate services or execute previously gated actions.

## API / MCP
Examples: list_my_approvals, get_approval, approve_request, reject_request, request_changes. Write tools require explicit decision scope and confirmation.

## PWA/mobile
Approving from phone must be first-class. Evidence must be legible before decision. Offline decisions are not committed without confirmed server authorization.

## Lovable build slices
1. Approval record/list/My Work integration.
2. Single approver decision flow.
3. Client Portal approval flow.
4. Multi-step/group rules and escalations.
5. Automation/API/MCP integration.