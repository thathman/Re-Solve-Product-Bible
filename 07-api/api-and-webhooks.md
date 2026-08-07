# Re:Solve API and Webhooks

## Purpose
Re:Solve exposes useful business capabilities programmatically so external tools, automations, agents and future products do not need to scrape UI or bypass permissions.

The API is first-class. UI, Action Registry, Automations, Plugins, Connectors and MCP should reuse the same domain/service contracts wherever practical.

## Principles
- versioned/documented;
- Principal identity + capability + record scope;
- canonical permission grammar;
- Organisation/Property/client isolation;
- predictable pagination/filtering/sorting/search;
- idempotent writes where appropriate;
- optimistic concurrency/version checks where needed;
- strong Audit for sensitive actions;
- source/provenance/freshness where material;
- consistent safe errors;
- no raw database/provider secret exposure;
- portable/self-hostable implementation.

## Conceptual `/api/v1` resources
Major resources/actions may include:
- operating-entities / brands where authorized;
- organisations / contacts / memberships / access-grants;
- properties / property-relationships / posture / monitors / renewals / incidents;
- projects / tasks / milestones / deliverables / client-actions;
- requests;
- opportunities / services / client-services;
- proposals / estimates / contracts;
- documents / document-templates / secure-external-access administration;
- invoices / payments / receipts / credits / refunds / subscriptions / reconciliation / statements;
- approvals;
- attention;
- notifications / preferences;
- files;
- Vault metadata and dedicated privileged Vault operations;
- knowledge;
- support summaries/references/entitlements;
- comments/activity/following where exposed;
- reminders / booking;
- saved-views;
- forms / submissions;
- custom-field definitions/values where allowed;
- imports / exports / data-quality issues;
- automations / actions;
- plugins / connectors / integration events;
- reports/defined metrics;
- Audit.

There are no Timesheet/Time Entry, HR or Client Service Consumption API resources.

Exact URL naming follows implementation conventions while public contract semantics remain stable.

## OpenAPI / developer reference
Provide machine-readable OpenAPI and human reference covering purpose, auth/capability, scope, request/response schema, errors, pagination, idempotency/concurrency, rate limits, Audit and side effects.

Plugin namespaced API contributions appear in the same documentation system.

## API Principals and credentials
API Client is a non-human Principal.

Credential records include:
- name/owner;
- enabled/expiry;
- scopes/capabilities;
- Operating Entity/Organisation/Property restrictions where applicable;
- created/rotated/last used;
- optional policy such as IP restriction later;
- revoke.

Raw credential shown only at creation/rotation. Stored credentials are hashed/protected as appropriate to credential type.

## Scopes / permissions
Use the same canonical capability vocabulary as the product, e.g.:
- `organisations.read`
- `properties.read`
- `properties.monitoring.manage`
- `projects.manage`
- `requests.read`
- `billing.read`
- `billing.invoices.create`
- `vault.metadata.read`
- `notifications.create`
- `automations.run`
- `connectors.events.replay`

Do not maintain an unrelated colon-separated permission universe.

Machine scope never overrides record-level access restrictions.

## Collection conventions
Consistent support as appropriate for:
- cursor/page pagination;
- typed filters;
- sort;
- search;
- date range;
- relationships;
- status;
- field selection/expansion only when safe.

Avoid unique ad-hoc conventions per domain.

## Data provenance
Resources backed by connector/derived/cache data should expose useful metadata such as source, observed/synced time, freshness and authority where consumers need it.

Stale/unknown cannot be serialized as false zero/healthy state.

## Idempotency
External/retry-prone create or side-effecting Actions accept idempotency keys where appropriate.

Examples:
- create Invoice/Request/Approval;
- create Payment link;
- run Automation;
- send operational communication;
- create Secure External Access grant;
- execute registered Connector-backed Action.

Idempotency key scope/retention/result semantics are documented.

## Concurrency
Sensitive mutable records may use version/ETag/updated-token checks to prevent silent lost updates, especially settings, access, commercial drafts and workflow configuration.

## Action endpoints
Consequential operations should map to Action Registry semantics instead of arbitrary one-off mutation routes.

Action execution performs:
- caller authorization;
- context/target validation;
- risk/confirmation/approval/step-up policy as applicable;
- idempotency;
- domain mutation;
- Event/Activity/Audit emission;
- result schema.

API availability must be explicitly declared by the Action; UI availability does not automatically expose an API action.

## Errors
Standard safe envelope:
- stable code;
- message;
- field errors;
- request/correlation id;
- remediation hints where safe;
- retryability metadata where useful.

Never leak secrets, stack traces, SQL or provider credentials.

## Rate limits
May vary by API Client, route/action risk, workload and provider capacity. Expose retry/limit metadata where practical.

## Outbound Webhooks
Subscription:
- name;
- endpoint;
- selected Event catalogue;
- protected secret reference;
- status;
- creator;
- scope/filter where supported;
- last success/failure;
- failure count.

Delivery payload includes stable Event id/type/version, occurred_at, permitted data, source ids/references and correlation id.

Requests are signed. Delivery history stores safe metadata, response status/timing/attempt and redacted failure details.

States: queued, sending, delivered, retrying, failed/dead-letter/paused.

Repeated failure can pause delivery and create Platform Attention/Notification.

## Event catalogue
Examples:
- organisation.created
- client.lifecycle_changed
- property.posture_changed
- property.renewal_due
- monitoring.outage_confirmed
- incident.created/resolved
- request.created/triaged/completed
- project.completed
- proposal.accepted
- contract.executed
- invoice.issued/paid
- payment.verified
- approval.completed
- vault.access_granted/revoked
- attention.created/resolved
- connector.health_changed

Plugins add namespaced Events.

## Inbound webhooks
Provider callbacks belong to Connector Integration Event runtime with verification, idempotency, normalization, retry/dead-letter and provenance.

Generic inbound Automation webhooks are explicit trigger endpoints with authentication/rate limits, not an escape hatch around Connector contracts.

## Secure External Access
Public guest actions use dedicated narrow grant/session endpoints with expiry/revocation and target-specific authorization. The guest token is not a general API credential.

## Vault API
Default public/machine surface is metadata-first.

Secret reveal/protected download is a dedicated privileged operation, disabled for broad API Clients by default and subject to narrower capability, object grant, step-up/confirmation policy and Audit.

Generic list/search/export never returns raw Vault secrets.

## Search / Reports
API exposes curated permission-aware Search and defined report/metric datasets. No unrestricted SQL/query endpoint.

## MCP relationship
MCP uses the same domain/action authorization but exposes a curated AI-friendly tool/resource surface with additional risk controls. It is not an alternate permission universe.

## Àríyá relationship
Àríyá uses internal controlled tools/actions rather than becoming an unrestricted proxy over public API. Both rely on the same domain authorization.

## Plugins
Plugin API resources/actions are namespaced/registered and inherit Principal auth, capabilities, record scope, rate limits, Audit, Action Registry and docs conventions.

## PWA / first-party app
First-party internal endpoints may be optimized for UI composition while public API remains stable/documented. Provider-specific SDK calls should not leak throughout browser UI.

## Admin settings
Settings > API & MCP should cover API Clients/tokens, scopes, Webhooks, delivery logs, docs, usage/limits and Audit.

## Audit
At minimum token create/rotate/revoke, scope/access changes, Webhook configuration, sensitive Actions, Secure External grants and high-risk API failures.

## Acceptance criteria
- meaningful business operations have programmatic equivalents where appropriate;
- API Client is a scoped Principal;
- canonical capabilities match UI/MCP concepts;
- cross-Organisation/Property denial is server-side;
- retries/idempotency cannot duplicate consequential records;
- source/freshness is truthful;
- outbound Webhooks signed/retryable/observable;
- provider inbound events use Connector runtime;
- Vault/hidden data is not exposed generically;
- Plugin endpoints cannot bypass core controls;
- OpenAPI remains current;
- no HR/Timesheet/Client Service Consumption resources exist.

## Lovable build slices
1. API Client/credential records + admin UI.
2. common Principal/scope enforcement + canonical error/idempotency patterns.
3. first read APIs for Organisations/Properties/Projects/Requests.
4. registered write Actions + concurrency/idempotency.
5. OpenAPI/reference.
6. outbound Webhook subscriptions/delivery runtime.
7. logs/retry/dead-letter/Audit.
8. plugin registry + expanded domain resources over time.
