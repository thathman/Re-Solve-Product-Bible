# Request Management

## Purpose
A Request is a structured ask that may require triage before it becomes a Task, Project, Support case/Chatwoot conversation, Approval, Opportunity/Proposal, Service activation/order or another authoritative record.

Requests fill the gap between free-form support and formal Project/commercial workflows.

## Request families / examples
- website/content change;
- add a journal/site/service;
- domain/DNS change;
- billing contact/profile change;
- access/user request;
- credential/Vault access request;
- **request a service / commercial change**;
- request a Proposal;
- Project change;
- File/document request;
- maintenance window;
- client operational request;
- plugin-defined request.

## Sources
Requests may originate from:
- Client Portal;
- public/Secure External Form;
- staff entry;
- inbound email/WhatsApp conversion where a connector/workflow supports it;
- Ariya proposal/routing;
- Client Journey;
- plugin;
- API/MCP where permitted.

## Request fields
Potential fields:
- id/reference;
- Request Type/category;
- title/description;
- requester;
- Organisation/Contact;
- Property/Project/Client Service context;
- source/provenance;
- priority;
- state;
- owner/team;
- requested date/deadline;
- Files;
- client-visible state;
- related Support reference;
- entitlement/commercial context;
- triage outcome;
- converted/linked records;
- Activity/Comments;
- Form Submission reference where applicable.

## States
Suggested:
- NEW
- TRIAGE
- NEEDS_INFORMATION
- ACCEPTED
- IN_PROGRESS
- WAITING_ON_CLIENT
- COMPLETED
- DECLINED
- CANCELLED

Request status is not Chatwoot conversation status.

## Triage outcomes
A Request can:
- remain a standalone Request;
- create/link a Task;
- create/link a Project;
- create/link a Change Request;
- create an Approval;
- create/link an Opportunity;
- start a Proposal workflow;
- create/activate/link a Client Service only through the proper commercial/approval path;
- create/open a Support case/Chatwoot conversation when Support is the right channel;
- create a Vault access Request;
- create a Client Journey/onboarding step;
- be declined with reason.

Do not duplicate the converted record; preserve durable source/result links.

## Portal — Request Something
Client Portal should provide a clear **Request Something / Services** entry that prevents clients using Support for ordinary commercial/service requests.

Examples presented in client language:
- New website / redesign;
- New landing page;
- Domain registration/renewal;
- Hosting change/upgrade;
- Additional journal/site;
- Additional service;
- Project change;
- Other request.

The list may be driven by enabled Service Catalogue categories/Request Types without exposing internal Catalogue complexity.

A client flow should:
1. choose what they need;
2. select relevant Property/Project where applicable;
3. answer a short Form/question set if needed;
4. attach Files;
5. understand whether the request is Support, included service work, or likely commercial work;
6. submit;
7. see status/clarification;
8. see linked outcome when client-visible.

## Service Request -> Opportunity -> Proposal
When a Portal Request represents **new paid work / scope**, triage should normally preserve this chain:

`Service Request -> Opportunity -> Discovery/Form if needed -> Proposal`

It must not automatically create an Invoice/Project just because a client clicked a service category.

Potential behavior:
- create/link Opportunity idempotently;
- carry Organisation/Contact/Property/Service interest/source;
- preserve Request answers/Files;
- assign commercial owner;
- use Ariya to summarize requirements;
- recommend Catalogue items/Package/Proposal Template;
- create Proposal draft through a registered Action when policy permits.

Existing-client commercial requests therefore stay distinct from Support cases.

## Entitlement-aware triage
A Request can inspect Client Service/Support Entitlement to help determine:
- included operational Request;
- Support case;
- Change Request;
- billable/new commercial Opportunity;
- client clarification required.

Entitlement informs routing; Re:Solve does not track consumed-hours/credits.

## Forms
Forms can create Requests through explicit routing. Form Submission provenance remains attached to the resulting Request/Opportunity/other record.

## Client Journey
A Request/Client Action may appear as one step in a Journey. Journey completion follows authoritative Request state; the Journey does not mark it complete independently.

## Ariya
Ariya may:
- classify Request intent;
- distinguish Support versus new commercial work using authorised context;
- summarize requirements;
- ask/draft clarification;
- recommend triage outcome;
- propose Opportunity/Proposal creation;
- identify relevant Service Catalogue items;
- Watch overdue/stalled Requests.

Consequential conversions remain registered Actions with normal permission/Approval/idempotency.

## Attention / Notifications / Tasks
Examples:
- new Request assigned;
- Request awaiting triage;
- needs client information;
- overdue/stale Request;
- accepted/declined;
- linked Proposal/Project/outcome ready.

Assigned operational work may project into Tasks. Persistent unresolved Request state may create Attention.

## Bulk Actions
Where safe, staff may bulk assign/tag/archive or send clarification/Form Requests. Commercial conversion is evaluated per Request and should not become a blind mass `create Proposal` action without preview/eligibility.

## Test / routing simulation
Request Types/routing policies can use the shared Dry-Run framework to show likely classification/outcome without creating downstream records.

## API / MCP
Examples:
- `create_request`;
- `get_request`;
- `list_requests`;
- `triage_request`;
- `request_more_information`;
- `convert_request_to_opportunity`.

## Acceptance criteria
- Requests do not duplicate Chatwoot helpdesk;
- existing clients can clearly request additional services without opening Support tickets;
- commercial Service Request routes to Opportunity -> Proposal rather than instant Project/Invoice;
- triage preserves durable source/result links;
- entitlement informs routing without consumption metering;
- Portal Request Types use understandable language;
- Ariya cannot silently convert/bill without Action policy;
- permissions/Property scope are enforced.
