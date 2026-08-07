# Admin — Service Catalogue & Client Services

## Purpose
Model what an Operating Entity sells and continuously delivers, separating reusable Service Catalogue definitions from client-specific Client Service instances.

## Service Catalogue Item
A reusable commercial/operational offering.

Fields may include:
- name/code/category;
- client-facing/internal description;
- pricing model/base price/currency;
- tax defaults;
- available billing cadence;
- setup fee;
- included contractual scope;
- default SLA/Support Entitlement;
- default Project/onboarding template;
- applicable Property Types;
- renewal behavior;
- internal delivery notes;
- status;
- plugin extensions/custom fields.

**Do not define consumption limits, remaining hours/credits or usage meters as a core Service capability.** Contractual scope can still describe what is included in natural/structured terms.

## Client Service
A client-specific service relationship links:
- Operating Entity;
- Organisation;
- Service Catalogue Item;
- one or more Properties;
- Proposal/Estimate/Contract source;
- start/end/renewal dates;
- agreed price/currency;
- Billing Schedule/Subscription where applicable;
- tax/payment terms;
- Support Entitlement;
- service owner/Account Team context;
- lifecycle status;
- related Projects/Requests;
- related Invoices;
- Connector/Plugin configuration references.

## Lifecycle
Suggested:
Draft -> Pending Activation -> Active -> Suspended -> Pending Renewal -> Ended/Cancelled.

Custom states may be controlled, but core semantics remain clear.

## Activation
Activation can orchestrate existing domains via Client Lifecycle/Automations:
- onboarding plan;
- Property association/intake;
- Project creation;
- Requests/Client Actions;
- Billing Schedule;
- Support Entitlement;
- Portal access;
- Chatwoot mapping;
- Monitoring setup;
- Connector provisioning;
- Knowledge/runbook setup.

Do not create a second hidden service-work engine.

## Recurring billing relationship
A Client Service may recur commercially, while Subscription/Billing Schedule describes recurring financial behavior.

`Client Service` and `Subscription` are not synonyms:
- Client Service = service relationship/scope;
- Subscription/Billing Schedule = recurring commercial billing arrangement.

A one-time Client Service may have no Subscription. A recurring Client Service may be manually invoiced without an external provider subscription.

## Renewal
Service renewal uses the shared Renewal/Expiry Obligation and commercial workflow.

Renewal can involve:
- notice windows;
- responsible owner;
- client decision;
- price/scope revision;
- Proposal/Estimate;
- Contract/signature;
- Billing/payment dependency;
- continuation/suspension/end;
- verification/completion.

Property-specific expiry obligations such as Domain/Hosting/Certificate remain linked but separate from Client Service renewal.

## Service packages
Catalogue packages may bundle multiple Service Catalogue Items/pricing lines for commercial convenience while activation still creates clear underlying Client Service relationships as required.

## Client visibility
Portal may show:
- Service name/description;
- status;
- covered Properties;
- Support Entitlement summary;
- start/renewal date;
- related commercial documents;
- Billing status/next action;
- client responsibilities/Requests.

No usage/remaining allowance summary is shown.

## Attention / Notifications
Attention:
- activation blocked;
- renewal approaching with no action;
- client decision/payment required;
- Service suspended/at risk;
- required setup/Connector missing.

Notifications cover material activation/renewal/change/suspension/end events according to policy.

## Automations
Examples:
- Contract executed -> create Pending Activation Client Service;
- Service activated -> create onboarding steps / Support mapping / Monitoring setup;
- renewal window -> create Renewal Obligation/Opportunity;
- Service ended -> begin appropriate offboarding/access review.

## API / MCP / Àríyá
Examples:
- list_service_catalogue
- get_client_services
- get_service_renewals
- create_client_service
- activate_client_service
- change_client_service_status

Commercial mutations use Action Registry, permission and Audit.
Àríyá may explain a Service's scope/status/renewal using authorized contract/catalogue context.

## Product exclusions
Service features must not introduce:
- Client Service Consumption;
- remaining-hours/credits dashboards;
- usage/retainer consumption ledgers;
- Timesheet-derived service usage;
- HR/workforce utilization.

If a future specialist product genuinely needs metered usage, it must be a deliberate plugin/domain decision rather than a hidden core assumption.

## Lovable build slices
1. Service Catalogue list/detail/editor.
2. Client Service workspace.
3. activation/onboarding relationships.
4. Billing/Support/Property relationships.
5. Renewal workflow + Portal exposure.
