# Request Management

## Purpose
A Request is a structured ask that may require triage before it becomes a Task, Project, Support Conversation, Approval, Service Order or another record.

Requests fill the gap between free-form support and formal project/commercial workflows.

## Examples
- update website content
- add a journal
- request domain/DNS change
- change billing contact
- request a new user/access grant
- request credential access
- request a quote
- request additional service
- request a project change
- request file/document
- request maintenance window

## Sources
Requests may originate from:
- Client Portal
- public/secure form
- staff entry
- email/WhatsApp conversion where a connector/workflow supports it
- Àríyá proposal
- plugin
- API

## Request fields
- id/reference
- type/category
- title
- description
- requester
- organisation/property/project/service context
- source
- priority
- state
- owner/team
- requested date/deadline
- attachments
- client-visible status
- related support reference
- related commercial entitlement
- triage outcome
- converted/linked records
- activity/comments

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

Request status is not the same as a Chatwoot conversation status.

## Triage outcomes
A Request can:
- remain a standalone request
- create/link a Task
- create/link a Project
- create/link a Change Request
- create an Approval
- create/link an Opportunity/Estimate
- create/open a Chatwoot support conversation where support is the appropriate channel
- create a Vault access request
- create an onboarding/offboarding step
- be declined with reason

Do not duplicate the converted record; preserve traceability.

## Forms
Forms may create Requests using a routing rule and mapped fields.

## Client Portal
Portal Request experience should be simple:
- choose understandable request type
- provide context/property
- explain what happens next
- attach files
- submit
- see status
- respond to clarification
- view linked outcome when client-visible

## Entitlement awareness
A Request may consult Client Service/Support Entitlement to inform triage, but Re:Solve does not maintain Client Service Consumption balances.

## Notifications and Attention
- new request assigned
- needs client information
- request overdue
- request accepted/declined
- linked outcome ready

## Collaboration
Requests use the shared comments/mentions/follow model, with explicit internal/client-visible communication boundaries.

## API/MCP/Àríyá
Examples:
- create_request
- get_request
- list_requests
- triage_request
- request_more_information

Àríyá may help classify/draft/triage, but consequential conversions remain registered actions.

## Acceptance criteria
- Requests do not duplicate Chatwoot helpdesk
- triage preserves a durable link to resulting records
- client-facing request types use understandable language
- entitlement can inform routing without service-consumption metering
- permissions and property scope are enforced
