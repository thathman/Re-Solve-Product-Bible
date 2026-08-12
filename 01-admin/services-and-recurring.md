# Admin — Service Catalogue & Client Services

## Purpose
Model what an Operating Entity sells and continuously delivers, separating reusable Catalogue definitions from client-specific Services and Recurring Arrangements.

## Service Catalogue Item
A reusable commercial/operational product or service offering.

Fields may include:
- name/code/category;
- client-facing/internal description;
- pricing basis;
- base price/currency;
- quantity unit where applicable;
- duration unit/default duration where applicable;
- tax defaults;
- setup fee;
- recurring/renewal eligibility;
- included contractual scope;
- default SLA/Support Entitlement;
- default Project/onboarding template;
- applicable Property Types;
- renewal behavior;
- internal delivery notes;
- status;
- plugin extensions/custom fields.

## Pricing basis
Canonical bases:
- `flat` — one fixed amount;
- `quantity` — quantity × unit price;
- `duration` — duration × rate.

Duration units support at least day, week, month, quarter and year.

Examples:
- logo design: flat;
- five social graphics: quantity × unit price;
- hosting for 12 months: 12 × monthly rate;
- domain for 2 years: 2 × yearly rate.

A duration-priced line is a measurement/pricing choice and **does not automatically create recurrence**.

Manual custom lines remain allowed in Proposals/Invoices where policy permits.

## Price Books / Rate Cards
Reusable price books can define:
- Operating Entity/Brand scope;
- Catalogue item;
- effective dates;
- currency;
- flat/quantity/duration rate;
- client class or specific Organisation override;
- active state.

Historical accepted Proposal prices remain immutable when a Rate Card later changes.

## Service Packages / Options
Packages may bundle Catalogue items for Proposal convenience and may be presented as mutually exclusive options or selectable add-ons. Activation still creates clear underlying Client Service relationships where needed.

## Client Service
A client-specific service relationship links:
- Operating Entity;
- Organisation;
- Catalogue Item/package source;
- one or more Properties;
- Proposal/Contract source;
- start/end/renewal dates;
- agreed price/currency/pricing basis snapshot;
- Billing Schedule where applicable;
- Support Entitlement;
- owner/Account Team context;
- lifecycle status;
- Projects/Requests/Invoices;
- Connector/Plugin references.

Suggested lifecycle: Draft -> Pending Activation -> Active -> Suspended -> Pending Renewal -> Ended/Cancelled.

## Recurring Arrangement
A first-class recurring commercial/operational arrangement such as hosting, maintenance or retainer.

It may define:
- Organisation/Operating Entity;
- linked Client Services/Catalogue lines;
- Properties;
- Contract/accepted Proposal;
- frequency;
- start/end;
- next billing/renewal date;
- billing mode: auto-create draft, auto-issue only if explicitly configured, or manual;
- payment terms;
- pause/cancel rules;
- renewal behavior;
- status.

A Recurring Arrangement is not synonymous with an external payment-provider subscription. Provider subscription is only a billing integration mapping.

## Activation
Activation can orchestrate existing domains via Automations/Action Registry:
- Portal invitation/onboarding pack;
- Property association/intake;
- Project creation from template;
- Tasks/Requests/Client Actions;
- Billing Schedule;
- Support Entitlement;
- Chatwoot/Ariya mapping;
- Monitoring setup;
- Connector provisioning;
- Knowledge/runbook setup.

Do not create a second hidden service-work engine.

## Renewal
Service/Recurring Arrangement renewal can involve notice windows, owner, client decision, price/scope revision, Proposal, Contract/signature, Billing/payment dependency, continuation/suspension/end and verification.

Property-specific Domain/Hosting/Certificate expiry obligations remain linked but separate.

## Project Templates
Catalogue items/packages may reference a default Project Template so accepted work can instantiate repeatable Milestones, Tasks, Approvals and client-visible defaults without hardcoding delivery into Sales.

## Portal
Portal may show service name/description, status, covered Properties, support entitlement, start/renewal date, related signed commercial documents, Billing state and client responsibilities. No usage/remaining allowance display exists.

## Ariya
Ariya may explain Service scope/status/renewal, recommend Catalogue/Package choices from authorised discovery context, surface pricing anomalies, Watch renewals and create controlled Tasks/Proposals through registered actions.

## Product exclusions
Do not define consumption limits, remaining hours/credits, usage meters, Timesheet-derived usage, work timers or HR/workforce utilization.

## Acceptance criteria
- pricing basis is explicit and supports duration;
- duration does not imply recurrence;
- Price Books/packages preserve accepted historical prices;
- Client Service and Recurring Arrangement are distinct;
- external provider subscription is only a Connector/Billing mapping;
- activation reuses shared domains;
- no consumption/time/HR feature is introduced.

## Build slices
1. Catalogue list/detail/editor + pricing basis.
2. Price Books/Rate Cards + packages/options.
3. Client Service workspace.
4. Recurring Arrangement lifecycle/Billing relationship.
5. activation/onboarding/Project Template relationships.
6. Renewal + Portal exposure.
