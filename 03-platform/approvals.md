# Platform — Approvals and Approval Policies

## Purpose
Provide one reusable decision engine for Projects, Proposals/Contracts, Billing/Adjustments/Refunds, Expenses, Vault access, Requests/Changes, high-risk Automations/Actions and Plugin-defined workflows.

Approval is evidence that an authorized person/group made a structured decision against an exact target/version. It is not a generic status flag and it does not replace Action Registry.

## Core records
### Approval Policy
Reusable, versioned rule describing when approval is required and how approvers are resolved.

Fields may include:
- id/reference/name;
- domain/use-case;
- Operating Entity/Workspace scope;
- trigger/eligibility conditions;
- ordered or parallel steps;
- approver resolver per step;
- completion rule;
- amount/risk/discount/record thresholds;
- due/escalation defaults;
- step-up requirements;
- client/external eligibility;
- active/published version;
- effective dates;
- owner;
- Audit/version history.

A published Policy Version is immutable for Approval Requests already created from it. Editing creates a new version; pending approvals continue under the frozen version unless explicitly migrated through a controlled action.

### Approval Request
Fields may include:
- id/human reference;
- target type/id/version;
- request type;
- title/summary;
- requested by Principal/User;
- requested at;
- Policy Version or explicit one-off rule;
- resolved approver(s);
- due at;
- state;
- current step(s);
- Organisation/Property/Project context;
- client-visible/external-access policy;
- escalation policy;
- evidence/document snapshot;
- source Action/Automation reference.

### Approval Step
A frozen step in one Approval Request containing:
- sequence/parallel group;
- approver resolver outcome;
- completion rule;
- state;
- due/escalation;
- evidence/version context.

### Approval Decision
Append-only evidence:
- Approval Request/Step;
- decision;
- actor User/Principal;
- comment/reason;
- decided at;
- acknowledged evidence/version;
- metadata/correlation.

## States
Suggested Request states:
- DRAFT
- PENDING
- IN_REVIEW
- CHANGES_REQUESTED
- APPROVED
- REJECTED
- CANCELLED
- EXPIRED
- ESCALATED

Completed decision evidence is never rewritten. Materially changed work requires a new Approval cycle/version.

## Approval methods
### Single approver
One named/resolved approver decides.

### Any one
Any one eligible approver in the step can satisfy it.

Example: Finance Owner **or** Director may approve.

### Everyone / all-of
Every resolved approver must approve before the step passes.

### Sequential
Steps run in order.

Example: Delivery Lead -> Finance -> Director.

### Parallel
Multiple steps/reviewers become active at once.

A parallel group may require `any one`, `all`, or a configured threshold/quorum where the product genuinely needs it.

### Conditional
Policy conditions decide whether approval is required and which path applies.

Examples:
- discount <=10% -> no Approval;
- discount 10–20% -> Sales Owner;
- discount >20% -> Director;
- Expense <=50,000 NGN -> Project Owner;
- larger Expense -> Project Owner + Finance;
- standard Contract terms -> no internal Approval;
- nonstandard terms -> Legal/Director policy where configured.

Conditions are typed and domain-owned; do not create arbitrary unsafe expressions.

## Approver resolvers
May support:
- named User;
- Team;
- role/capability;
- Account Team responsibility;
- record owner;
- Operating Entity responsibility;
- client-designated approver;
- any-of/all-of group;
- plugin-defined resolver through approved contract.

Resolution is frozen/explainable for each Request while decision authority is still revalidated at decision time.

## Action Registry relationship
An Approval may gate a registered Action.

Example:
1. user requests high-value Refund;
2. Action policy requires Approval;
3. Approval Request records exact amount/Invoice/evidence;
4. Policy resolves approvers;
5. required decisions complete;
6. Action rechecks current permission/context/idempotency/provider state;
7. downstream execution is attempted;
8. Approval does not falsely claim provider execution succeeded.

This distinction applies to Refunds, Credit/Adjustment actions, production DNS/hosting changes, Vault access, Contract activation, destructive operations and high-risk Automations.

## Policy examples
Reusable policies may gate:
- high Proposal discount;
- nonstandard Proposal/Contract terms;
- unusual deposit/payment schedule;
- Credit Note/write-off/Refund;
- Expense threshold;
- Project Change Request;
- production release/maintenance;
- client Deliverable approval;
- Vault access/reveal/grant;
- Connector/DNS/hosting action;
- bulk high-risk operation;
- Automation enablement/change.

## UX
Approval appears in Tasks, Attention, Notifications, source workspaces, Portal and Secure External Access where permitted.

Decision UI must show:
- exactly what is being approved;
- current target/version/snapshot;
- financial/operational consequence;
- changed terms/value;
- requester/context;
- current step and other required steps;
- deadline/escalation;
- required acknowledgement/confirmation.

Never ask a user to approve a generic title without underlying evidence.

## Client / Secure External approvals
Portal approval uses client-safe evidence and exact Organisation/Property/Project scope.

Selected non-Portal recipients may use narrow expiring Secure External Access where the Approval Policy explicitly permits it.

Knowing a hidden URL never makes a person an eligible approver.

## Changes requested / resubmission
When a reviewer requests changes, the source record may be revised. A new exact version/snapshot is then resubmitted through a new or explicitly restarted Approval cycle according to policy. Old decision evidence remains intact.

## Automation
Approval can pause/resume Automation, gate Actions, create Tasks/Requests, allow publication/issue, activate a Service/Project step or request revised evidence.

Automation never fabricates a human Approval Decision.

## Test / simulation
Approval Policies integrate with the shared Test/Dry-Run framework.

A simulation should show:
- whether Policy matches;
- resolved steps/approvers;
- sequential/parallel activation;
- thresholds/conditions;
- downstream Action that would be gated;
- missing resolver/permission configuration.

No real Approval Request/Decision is created in a dry run unless the operator explicitly chooses a dedicated test record.

## Template Center
Reusable Approval Policy templates/recipes may be discoverable from Template Center only where it improves administration; the Approval domain remains authoritative.

## Ariya
Ariya may:
- summarize evidence/consequence;
- explain why Approval is required;
- explain remaining approval path;
- draft decision comments;
- recommend a Policy based on authorised context;
- simulate Policy routing.

Ariya cannot decide on behalf of a human unless the workflow explicitly defines a non-human deterministic gate rather than a human Approval.

## Permissions / security
Decision authority is rechecked at decision time: Principal, capability, scope, eligibility, Step/Version, expiry and step-up.

Policy create/edit/publish is separately permissioned and audited.

## API / MCP
Potential tools: `list_my_approvals`, `get_approval`, `get_approval_policy`, `simulate_approval_policy`, `approve_request`, `reject_request`, `request_changes`.

High-impact decision tools may be disabled for MCP by policy.

## PWA/mobile/accessibility
Phone Approval is first-class. Evidence, amount, version and consequence are readable before decision controls. Offline decisions do not commit without current server authorization.

Actions are textual and keyboard/focus accessible; meaning never depends on red/green color alone.

## Acceptance criteria
- Approval Policy is reusable and versioned;
- single/any-one/everyone/sequential/parallel/conditional methods are explicit;
- pending Requests remain bound to the exact Policy/evidence version;
- decisions are append-only;
- downstream Action success remains distinct from Approval;
- client/external Approval is securely scoped;
- eligibility is rechecked at decision time;
- dry run can explain Policy routing without side effects;
- Ariya cannot bypass human decision authority;
- mobile decision experience is clear.

## Build slices
1. Approval Request/Decision model + Tasks/Attention.
2. Approval Policy/version model + single/any/all.
3. sequential/parallel/conditional routing.
4. Project/client/Secure External Approval.
5. Action Registry/Automation/Billing/Commercial integration.
6. simulation/escalation/API/MCP/Ariya polish.
