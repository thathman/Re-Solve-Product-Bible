# Ariya (Àríyá) — Re:Solve Intelligence Fabric

## Purpose
**Ariya (Àríyá)** is Re:Solve's built-in intelligence fabric and user-facing AI operator. It is baked into the OS rather than added as a standalone chatbot/module.

Ariya can understand, correlate, draft, monitor and act across every domain the current Principal is authorised to access while preserving evidence, provenance, permissions and Action/Audit boundaries.

Chatwoot Captain remains a separate system. It does not power Ariya.

## Product goals
- know the authorised Re:Solve state across domains;
- reduce scanning/repetitive writing;
- surface risk/Attention before a user has to ask;
- make dense records and cross-domain relationships understandable;
- monitor Property Health and operational/system conditions;
- triage Communications/inbound email;
- assist Sales, Projects, Support, Billing, Forms and client operations;
- execute controlled registered actions without bypassing permission;
- expose source/evidence/freshness for material claims;
- remain provider-abstracted.

## Operating modes
### Ask
Search/explain authorised Re:Solve truth.

Examples: What is going on with this client? Which invoices are overdue? Why is this Property degraded?

### Draft
Create proposed content/work such as Proposal scope, email, Project update, collection message, Task description, review request or report narrative.

### Act
Invoke a registered authorised action such as create Task/Reminder/Request, route communication, create Support work or run an approved workflow.

### Watch
Continuously observe a condition through Monitoring/Automation/Event primitives and react according to explicit policy.

Examples: domain expiry, repeated outage, unanswered client email, overdue invoice, pending approval, failed job.

### Investigate
Correlate evidence across domains to explain likely cause or relationship while clearly separating deterministic fact from AI inference.

### Recommend
Proactively propose useful next actions with reason/evidence, without fabricating urgency or silently executing consequential work.

## Authority model
Ariya is powerful because it has broad **authorised context**, not because it bypasses controls.

Every tool/action performs fresh server-side authorization using caller Principal, capability and scope. If a user cannot normally see/reveal/change something, Ariya cannot reveal/change it for them.

Risk examples:
- read/explain: normally automatic;
- draft: automatic draft only;
- low/medium registered write: according to policy;
- financial/security/Vault/destructive action: stronger confirmation/Approval/step-up;
- irreversible or legally consequential action: explicit action-specific policy.

## AI Gateway
All provider requests flow through a Re:Solve AI Gateway responsible for caller Principal, context, provider/model routing, tool/action catalogue, authorization, budgets, redaction/data class, timeout/retry, validation, usage and Audit metadata.

Business domains do not call model-provider SDKs directly.

## Context and evidence
Ariya may receive controlled context from Organisation, Contact, Opportunity, Proposal, Contract, Property, Project, Task, Form/Submission, Communication, Support, Billing, File/Knowledge, Report, Automation and System records.

Material answers should expose links/source references, timestamps/freshness and provenance where useful.

Ariya distinguishes:
- deterministic/current fact;
- stale/unknown source;
- connector/provider evidence;
- AI inference;
- recommendation;
- draft;
- proposed action;
- completed registered action.

Never fabricate success.

## Client / CRM / Sales
Ariya may:
- summarize Organisation relationship/history;
- qualify/triage Leads with evidence;
- summarize Communications/Discovery;
- recommend Opportunity next action;
- draft follow-up;
- build Proposal outline from Forms/context;
- suggest Service Catalogue items/packages/Price Book candidates;
- flag unusual pricing/discounts;
- Watch stale Opportunities/expiring Proposals;
- prepare Contract/renewal context.

Sending/accepting/signing/issuing remains controlled.

## Projects and Tasks
Ariya may:
- turn accepted Proposal + questionnaire into a proposed Project plan;
- suggest Project Template, Milestones and Tasks;
- identify blockers/dependencies;
- summarize progress/risks;
- create/reschedule Tasks through policy;
- Watch overdue milestones/client actions;
- draft client updates/reports.

No work timer/timesheet behavior exists.

## Property Health / Monitoring
Ariya consumes native Monitoring/Posture evidence plus authorised Connector signals.

It may:
- explain Health/Posture and source freshness;
- Watch HTTP/SSL/domain/DNS/TCP/heartbeat/backup/application signals;
- correlate repeated incidents/degradation;
- investigate likely causes;
- recommend remediation;
- create/attach Incident, Task or Support work through Automation/Action policy;
- draft incident/client update;
- distinguish monitor/provider failure from confirmed target failure.

Ariya never invents health status without evidence.

## Communications and inbound email
Ariya may inspect authorised inbound email metadata/content/attachments according to data policy and classify sender, Organisation, intent, urgency, Property/Project, Support relationship, commercial/Billing context and requested action.

High-confidence classification may auto-route only under explicit policy. Uncertain messages go to Inbox Triage with explanation.

Examples:
- client outage email -> create/attach Support work;
- hosting renewal quote -> Opportunity/Proposal follow-up;
- Project answer -> Project context;
- proof-of-transfer email -> reconciliation triage, **never automatic Payment verification from text alone**.

Ariya may identify client communications waiting too long for a response and create Attention/Task according to policy.

## Support and Portal live chat
Canonical flow:
`Client Portal -> Ariya -> Chatwoot -> Ariya -> Client`.

Ariya first uses client-authorised Re:Solve context to answer/route. When human intervention is needed, it hands off through Chatwoot and preserves Support mapping/context. Human response returns through the same client experience.

Ariya is not Chatwoot Captain and Re:Solve does not build a competing agent chat console.

## Billing
Ariya may explain Invoice balance/Adjustments, summarize receivables, draft reminders, identify overdue accounts, recommend reconciliation matches and route payment evidence for review.

It can never invent a Payment, mark one verified from ordinary text, silently add a fee, or bypass Approval/financial Action rules.

## Forms
Ariya may summarize questionnaire/survey responses, extract requirements/deadlines, propose Tasks/Milestones/Services, compare authorised responses and draft personalised Review Requests.

## Documents
Ariya may draft narrative, explain/review permitted document revisions and flag missing fields/signatures. It cannot silently issue/sign/send/accept a legal/commercial/financial document.

## Reviews and client success
Ariya may identify eligible completed engagements, recommend when a Review Request is appropriate and draft personalised requests. It never fabricates that an external review was posted.

## System operations / setup
Ariya may explain setup/system readiness, failed jobs, Connector health, delivery failure, backup/Monitoring Worker status and operational Attention. It cannot bypass installer lock or execute destructive maintenance from unrestricted language.

## Vault / sensitive information
Default AI access excludes raw passwords, tokens and keys. Authorized metadata may be searchable. Where a future tool needs a secret, prefer a capability/secret handle that lets the operation use the protected value without injecting/revealing it to the generic model context.

## Knowledge / Files
Ariya may process authorised ordinary Files/Documents/Knowledge. Vault-protected content follows stricter policy and never becomes generic search/index context by accident.

## Global presence
Ariya is available through global Search/Command/assistant entry, Home briefing and contextual record actions/panel. It does not require users to navigate to a dedicated Ariya module.

Final interaction placement/visual treatment is governed by the Admin/Portal experience redesign; no assistant UI may obscure primary product work.

## Portal Ariya
Portal Ariya is narrower and always bound to active Membership + selected Organisation/record scope.

It may:
- explain own Project/Invoice/Property Health;
- find client-visible Knowledge;
- explain action required;
- upload/link a File through an authorised File Request;
- create a Support Request;
- continue/live-chat through Chatwoot handoff.

It never exposes internal notes, margins, risk reasoning, hidden Properties, other clients, staff-only Knowledge, audit detail or Vault values.

## Usage / Audit
Track provider/model, feature, caller, duration, usage, read tools/actions, target records, confirmations/Approvals and outcome according to retention/privacy policy. Do not retain full sensitive prompts indefinitely just for debugging.

## Failure states
Handle provider/model unavailable, timeout, budget limit, tool denied, stale source, context too large, validation failure and Connector/source unavailable without corrupting records. Ariya explicitly says when evidence/access is insufficient.

## Acceptance criteria
- Ariya is embedded intelligence across the OS, not a bolt-on module;
- modes Ask/Draft/Act/Watch/Investigate/Recommend are supported conceptually;
- caller permissions are enforced at tool/action execution;
- Property Health monitoring/explanation is evidence-based;
- inbound email can be intelligently routed without fabricating business truth;
- Portal live chat uses Ariya -> Chatwoot -> Ariya;
- high-risk writes reuse Action/Approval/step-up policy;
- Vault secrets are not exposed to generic model context;
- source/freshness/inference are distinguishable;
- provider failure does not corrupt records.

## Build slices
1. provider-neutral AI Gateway + read tool contracts.
2. global/contextual Ariya + sources/evidence.
3. Ask/Draft across Clients/Projects/Sales/Billing.
4. Tasks/Attention operational briefing + Recommend.
5. Property Health Watch/Investigate integration.
6. Communications/email triage.
7. Action Registry integration + confirmation/Approval.
8. Portal Ariya + Chatwoot handoff.
9. Automation AI steps/Watch policies.
10. usage/audit/degraded-state polish.
