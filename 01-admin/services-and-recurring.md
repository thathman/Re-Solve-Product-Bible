# Admin — Service Catalogue & Recurring Services

## Purpose
Model what Re:Solve sells and continuously delivers, separating reusable service definitions from client-specific service instances.

## Service Catalogue
A Service defines a reusable commercial/operational offering.

Fields may include:
- name
- code
- category
- description
- billing model
- base price/currency
- tax defaults
- billing cadence options
- setup fee
- included scope
- limits/allowances
- default SLA/support entitlement
- default project template
- default property types
- renewal behavior
- client-visible description
- internal delivery notes
- status

Service definitions may be extended by plugins.

## Client Service / Recurring Service
A client-specific instance links:
- organisation
- service
- one or more properties
- contract/proposal source
- start/end dates
- billing cadence
- agreed price/currency
- tax treatment
- quantity/plan
- renewal date
- auto-renew/manual-renew state
- support entitlement
- service owner
- delivery status
- related invoices/projects
- connector/plugin configuration

## Lifecycle
Draft → Pending Activation → Active → Suspended → Pending Renewal → Ended/Cancelled, with controlled custom states where necessary.

Activation may create a project, property tasks, connector provisioning, billing schedule, support entitlement and onboarding actions through automations.

## Renewal
Renewal workflows support advance notice windows, price/scope change, client approval, proposal/estimate generation, invoice generation, contract/signature requirements and service continuation/termination.

## Usage / allowance
Some services may track usage or retainer consumption. Usage dimensions must be defined by the service/plugin; Re:Solve should not assume hours are the only unit.

## Notifications
Activation, upcoming renewal, renewal action required, payment dependency, suspension risk, service change and cancellation.

## API / MCP
Examples: list_services, get_client_services, get_service_renewals, create_service_instance, change_service_status. Commercial write tools require strong scopes and audit.

## Portal
Clients can see only client-visible service terms, current status, linked properties, renewal dates, permitted usage summaries and required actions.

## Lovable build slices
1. Service catalogue list/detail/editor.
2. Client service instance workspace.
3. Activation workflow links.
4. Renewal flow.
5. Usage/allowance extensions and Portal exposure.