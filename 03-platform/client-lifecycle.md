# Client Lifecycle

## Purpose
Client Lifecycle is the cross-domain operating flow that turns a commercial relationship into an active, supportable client and eventually closes/transfers that relationship safely.

It orchestrates existing records rather than creating a second copy of them.

## Lifecycle stages
Suggested lifecycle vocabulary:
- Prospect
- Qualified
- Commercial Review
- Won / Preparing Onboarding
- Onboarding
- Active
- At Risk
- Paused/Suspended where applicable
- Offboarding
- Former/Archived

Organisation lifecycle state remains configurable, but transitions should have clear operational consequences.

## Onboarding
A client onboarding plan may coordinate:
- Organisation/profile completion
- Contacts and roles
- Account Team assignment
- accepted proposal/contract
- service activation
- billing profile/payment terms
- initial invoice/deposit where required
- properties to manage
- domain/hosting/platform inventory
- credential/Vault requests
- connector setup/mappings
- portal invitations/access
- Chatwoot support mapping
- support entitlement
- monitoring setup
- project creation/template
- required files/content
- client approvals/actions
- knowledge/runbook creation
- communications preferences
- handoff to steady-state operations

## Onboarding plan
Use a reusable Plan/Checklist concept backed by Tasks, Client Actions, Requests and Approvals rather than an isolated onboarding task engine.

An onboarding template may declare required steps by service/property type.

## Onboarding status
Show:
- overall stage
- blockers
- client actions
- internal actions
- access/credential readiness
- property readiness
- billing readiness
- support readiness
- monitoring readiness
- next milestone
- responsible account owner

The Attention Engine surfaces blocked/stale onboarding.

## Account Team
An Organisation may have named operational responsibilities such as:
- Account Owner
- Delivery/Project Owner
- Technical Owner
- Finance Owner
- Support/Relationship Owner

These are assignment responsibilities, not HR job records.

## Relationship reviews
Active clients may have periodic account-review records capturing:
- current services
- project state
- property posture
- support/incidents
- renewals
- receivables
- risks
- opportunities
- decisions/actions

A review can generate Tasks, Requests, Opportunities or Knowledge updates.

## Offboarding
Offboarding must be explicit and safe.

Potential checklist:
- confirm effective end date
- close/cancel future service billing
- settle/credit outstanding invoices as approved
- complete/close projects
- export/hand over client files
- transfer credentials/domains/hosting where contractually required
- review/revoke Vault access and temporary shares
- revoke portal memberships/access
- disconnect or remap connectors
- stop/transfer monitoring
- close/transfer Chatwoot support mappings
- archive relevant properties/services
- provide final documents/statements
- preserve required audit/commercial history
- apply retention/deletion policies

Offboarding must not automatically delete history.

## Handover
Support structured handover packages using Document Studio, Files, Secure External Access and Vault where needed.

## Reassignment
When a responsible staff user becomes unavailable/deactivated, lifecycle ownership must be reassignable without HR functionality.

## Notifications and Attention
Examples:
- onboarding blocked
- client action overdue
- required credential missing
- support/monitoring not configured before go-live
- offboarding action overdue
- access still active after offboarding date

## Automations
Examples:
- proposal accepted -> create onboarding plan
- service activated -> request required property information
- onboarding complete -> mark Organisation Active
- offboarding started -> create access review

Automations may create steps but cannot bypass permission/approval requirements.

## Portal
Client Portal should present only relevant onboarding/offboarding actions, uploads, approvals and status. Do not show internal transition complexity.

## API/MCP/Àríyá
Expose lifecycle summary and allowed actions. Àríyá may summarize blockers and draft client follow-up, but must not automatically revoke/transfer critical assets without controlled actions.

## Acceptance criteria
- onboarding connects commercial, property, access, support and billing work coherently
- no duplicate shadow records replace native domain objects
- offboarding revokes/handovers access deliberately
- operational history is retained according to policy
- client and internal views expose different appropriate detail
- no HR or timesheet dependency is introduced
