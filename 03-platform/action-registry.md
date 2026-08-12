# Command and Action Registry

## Purpose
Re:Solve needs one controlled registry of meaningful actions so the same business capability can be surfaced consistently through UI, Search/Command, Ariya, API, MCP, Automations and Plugins.

The registry prevents multiple inconsistent implementations of `send invoice`, `create task`, `renew domain`, `approve request`, `archive organisation`, etc.

## Action definition
An Action declares:
- stable id;
- label/description;
- domain;
- target record type(s);
- context requirements;
- required capability/scope;
- risk class;
- confirmation policy;
- Approval requirement/Policy;
- step-up requirement;
- input schema;
- output/result schema;
- idempotency behavior;
- Audit requirement;
- availability by Admin/Portal/Command/Ariya/API/MCP/Automation;
- plugin/connector implementation where applicable;
- **bulk eligibility and limits**;
- **preview/dry-run capability**;
- **dependency/impact requirement** for destructive/high-impact actions;
- client-visible consequence text where applicable.

## Risk classes
### Read
No mutation; still permission-scoped.

### Standard Write
Routine reversible/low-impact mutation.

### Sensitive Write
Financial, access, Connector, Vault or consequential business mutation; normally explicit confirmation.

### High Impact
Destructive, security-sensitive, externally consequential or broad/bulk mutation. May require step-up, Approval, mandatory impact preview and/or dry run.

## UI integration
Actions may appear in page headers, record menus, table rows, **bulk-action bars**, Search/Command, Quick Create, contextual drawers, Tasks, Notifications/Attention and Ariya proposals.

Labels, consequences and policy should remain consistent across interfaces.

## Command/Search
The command surface consumes registered Actions plus navigation/search. It prioritizes context, permission and recent/relevant use rather than showing an exhaustive technical catalogue.

## Ariya
Ariya may propose/invoke only registered Actions. It cannot invent arbitrary database/provider mutations.

Before consequential execution Ariya shows:
- proposed Action;
- target/matched records;
- material consequence;
- risk/confirmation/Approval requirement;
- dependency/impact summary where required;
- dry-run result where available/required.

## API / MCP
Public Action endpoints and MCP tools may map to registry definitions where appropriate. Registration does not automatically make an Action public or agent-accessible.

## Automation
Automation Actions reuse the same contracts or explicitly registered automation-only Actions, preserving permission/risk/idempotency semantics.

## Plugins and Connectors
Plugins may register namespaced Actions. Connectors may provide provider-backed implementations behind approved domain Actions.

Example: `properties.domain.renew` can use a registrar Connector while the user-facing Action remains Re:Solve-owned.

## Bulk Actions
Bulk capability is **explicit per Action**.

An Action that works on one record does not automatically become bulk-capable because a table supports selection.

A bulk-capable Action declares:
- allowed target type(s);
- maximum/default batch size;
- per-record authorization behavior;
- eligibility/precondition evaluation;
- all-or-nothing versus partial-success semantics;
- idempotency strategy;
- required preview/dry run;
- confirmation summary;
- Approval threshold if any;
- notification/external side-effect policy;
- Audit/result reporting.

### Bulk preview
Before execution, show:
- selected/matched count;
- eligible count;
- denied/skipped count + reasons;
- records with warnings/dependencies;
- expected mutations/external sends;
- Approval/step-up requirements;
- whether execution is atomic or partial.

High-impact bulk Actions require mandatory preview and may be disallowed entirely.

Examples of reasonable bulk Actions:
- assign owner/team;
- add/remove tags;
- archive eligible records;
- send Form Request;
- create renewal Tasks;
- add to Cadence;
- export permitted records;
- create Review Requests.

Examples that should not become casual bulk Actions:
- mark Invoices paid;
- reveal Vault secrets;
- delete/rotate credentials;
- issue/refund money broadly;
- approve/sign legal records on behalf of clients.

## Dependency / Impact Inspector
Destructive/high-impact Actions can declare a dependency-inspection requirement.

Before actions such as Archive/Delete/Disable/Disconnect/Replace, Re:Solve evaluates direct and meaningful dependent records/capabilities and returns blockers, warnings and available alternatives.

Examples:
- Organisation archive/delete -> active Projects, Properties, Portal Memberships, unpaid Invoices, Contracts, Services;
- Staff deactivation -> assigned Tasks/Projects/Approvals/Renewals/signatory defaults/Automations;
- Service Catalogue item archive -> active Client Services/Proposal defaults/Recurring Arrangements;
- Template archive -> active/default/dependent usage;
- Connector disable -> Properties/Automations/Payments/Monitoring/email using it;
- Property archive -> Support/Projects/Renewals/Monitoring/Services.

Impact inspection is permission-aware and must not leak hidden records through counts/details to unauthorized callers.

The result can classify:
- hard blocker;
- warning;
- reassignment required;
- safe archival alternative;
- cascade explicitly allowed by domain policy;
- no material dependency.

## Preview / Test / Dry Run
Actions may register a no-side-effect preview/dry-run implementation through the shared Test/Simulation framework.

The dry run returns eligibility, proposed changes, dependencies, calculations, external calls that would occur and skipped/blocked reasons without executing the Action.

A dry run never masquerades as completion.

## Confirmation and review
Confirmation UI for high-impact Actions should summarize the real effect, not merely ask `Are you sure?`.

For bulk/destructive Actions include target count, dependency impact, irreversible consequences, expected notifications/external operations and recovery path where applicable.

## Audit and result
Every consequential Action produces an outcome record/Audit correlation with:
- actor/interface;
- target(s);
- Action/version;
- input summary;
- confirmation/Approval evidence;
- execution result;
- partial-success/failure details;
- external correlation/provider reference where relevant.

## Acceptance criteria
- Action semantics are reusable across interfaces;
- authorization happens at execution time;
- Ariya cannot bypass registry policy;
- Plugins/Connectors remain permissioned/auditable;
- bulk eligibility is explicit and permission-aware;
- high-impact bulk Actions expose preview/impact first;
- Dependency Inspector blocks unsafe destructive work without leaking hidden data;
- dry run has no business side effects;
- action labels/consequences remain consistent across surfaces.
