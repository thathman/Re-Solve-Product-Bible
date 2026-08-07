# Platform — Approvals

## Purpose
Provide one reusable decision engine for Projects, commercial documents, Expenses, Vault access, Requests/Changes, high-risk Automations/Actions and Plugin-defined workflows.

Approval is evidence that an authorized person/group made a structured decision. It is not a generic status flag and it is not a replacement for Action Registry.

## Core records
### Approval Request
Fields may include:
- id/human reference;
- target type/id/version;
- request type;
- title/summary;
- requested by Principal/User;
- requested at;
- assigned approver(s)/rule;
- due at;
- state;
- current step;
- Organisation/Property/Project context;
- client-visible/external-access policy;
- escalation policy;
- evidence/document snapshot;
- source Action/Automation reference where applicable.

### Approval Decision
Append-only decision evidence:
- Approval Request/step;
- decision;
- actor User/Principal;
- comment/reason;
- decided at;
- acknowledged evidence/version;
- metadata/correlation.

## States
Suggested:
- DRAFT
- PENDING
- IN_REVIEW where useful
- CHANGES_REQUESTED
- APPROVED
- REJECTED
- CANCELLED
- EXPIRED
- ESCALATED

A completed decision is not rewritten. Reopening materially changed work creates a new cycle/version rather than erasing prior evidence.

## Approver rules
May support:
- single named approver;
- role/capability resolution;
- client-designated approver;
- any-of group;
- all-of group;
- ordered multi-step;
- amount/risk threshold;
- contextual rule;
- Plugin-defined resolver through approved contract.

Approver resolution/effective rule should be versioned/frozen enough to explain who could decide at that time.

## Action Registry relationship
An Approval may gate a registered Action.

Example:
1. user requests high-value refund Action;
2. Action policy requires Approval;
3. Approval Request records target/amount/evidence;
4. authorized approver approves;
5. Action may then execute only after rechecking current permission/context/idempotency/provider state;
6. Approval itself does not prove the downstream provider Action succeeded.

This distinction is important for refunds, DNS changes, Vault access, Contract activation and other consequential workflows.

## UX
Approval surfaces appear in:
- My Work;
- Attention;
- Notifications;
- source record workspace;
- Client Portal;
- Secure External Access when an authorized external recipient needs one narrow decision.

Decision UI must show:
- exactly what is being approved;
- current version/snapshot/evidence;
- consequences;
- any changed terms/value;
- requester/context;
- deadline;
- required acknowledgement/confirmation.

Do not ask a user to approve a generic title without the underlying evidence.

## Examples
- Project Deliverable;
- production release/maintenance window;
- Proposal/Estimate internal approval;
- Change Request;
- Expense/billable Expense;
- Refund/Credit;
- payment schedule/discount exception;
- Vault access;
- high-risk Connector Action such as production DNS change;
- high-risk Automation;
- Plugin-defined publishing/release decision.

## Client approvals
Portal approval uses client-safe evidence only and respects Organisation/Property/Project scope.

A client can never become eligible simply because a hidden Approval URL is known.

## Secure External Access
Where the recipient is not a Portal User, selected approval/document workflows may use a narrow expiring Secure External grant with recipient verification according to risk.

This is appropriate only when the Approval type/policy explicitly allows external guest decision.

## Version/evidence integrity
Approval records should reference the exact evidence/version being approved.

For Document Studio/commercial documents, accepted/approved/executed content should reference immutable or versioned snapshots so later edits do not retroactively change the decision target.

## Attention
A pending Approval can create Attention for assigned approvers and optionally requester/escalation owner.

Approval Attention resolves when the current approval cycle reaches a terminal outcome or is no longer actionable.

## Notifications
Requested, due soon, reminder, escalated, changes requested, approved, rejected, expired and cancelled according to policy.

Reading a Notification does not decide/resolve an Approval.

## Automations
Approval can:
- pause/resume Automation;
- gate registered Action;
- create follow-up Task/Request;
- publish/issue a document;
- activate a Service/Project step;
- request new evidence/version after Changes Requested.

Automation never fabricates a human Approval Decision.

## Collaboration
Approval may support bounded comments/clarification through shared Collaboration where policy allows. Internal Notes remain hidden from client/external approvers.

## Permissions / security
Decision authority is checked at decision time, including current Principal/User, capability, scope, approver eligibility, step/version and expiry.

High-risk decisions may require step-up.

Audit includes request, assignment/rule changes, decision, cancellation, escalation and downstream gated Action reference.

## API / MCP / Àríyá
Potential API/MCP tools:
- list_my_approvals
- get_approval
- approve_request
- reject_request
- request_changes

Write operations require explicit decision capability and confirmation. MCP exposure of high-impact Approval decisions may be disabled by policy.

Àríyá may summarize the evidence/consequence or draft a decision comment, but cannot decide on behalf of a human unless an explicitly non-human approval policy exists for that workflow.

## PWA/mobile
Phone approval is first-class. Evidence/amount/version/consequence must be readable before the decision controls.

Offline decisions are not committed without current server authorization; drafts/comments may only queue if safely designed.

## Accessibility
Approve/Reject/Request Changes are explicit textual Actions with keyboard/focus/error handling. Destructive/reject actions cannot depend on red/green color alone.

## Acceptance criteria
- decisions reference exact target/version/evidence;
- completed decision evidence is not rewritten;
- Action-gated Approval and downstream Action success remain distinct;
- client/external Approval is securely scoped;
- current eligibility is rechecked server-side;
- Attention/Notification lifecycles are distinct;
- high-impact Automation/MCP cannot bypass Approval policy;
- mobile decision experience is clear.

## Lovable build slices
1. Approval model/list/My Work/Attention integration.
2. single-approver decision flow.
3. Project/client Portal Approval.
4. Secure External document Approval where needed.
5. multi-step/group/escalation.
6. Action Registry/Automation/API/MCP integration.
