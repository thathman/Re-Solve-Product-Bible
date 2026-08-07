# Command and Action Registry

## Purpose
Re:Solve needs one controlled registry of meaningful actions so the same business capability can be surfaced consistently through UI, command palette, Àríyá, API, MCP, automations and plugins.

The registry prevents six separate implementations of `send invoice`, `create task`, `renew domain`, `approve request`, etc.

## Action definition
An Action should declare:
- stable id
- label
- description
- domain
- target record type(s)
- context requirements
- required capability
- applicable scope
- risk class
- confirmation policy
- approval requirement
- step-up requirement
- input schema
- output/result schema
- idempotency behavior where relevant
- audit requirement
- availability in Admin UI
- availability in Portal
- command-palette availability
- Àríyá availability
- API availability
- MCP availability
- automation availability
- plugin/connector implementation if applicable

## Risk classes

### Read
No mutation. Still permission-scoped.

### Standard Write
Routine reversible/low-impact mutation.

### Sensitive Write
Financial, access, connector, Vault or consequential business mutation; may require explicit confirmation.

### High Impact
Destructive, security-sensitive or externally consequential action. May require step-up and/or approval.

## UI integration
Actions may appear in:
- page headers
- record action menus
- table row actions
- bulk-action bars
- command palette
- quick create
- contextual drawers
- notification/attention items
- Àríyá proposals

The UI must present the same labels and consequences consistently.

## Command palette
The command palette consumes registered actions plus navigation/search. It should prioritize relevant actions by current context, permission and recent use instead of displaying an exhaustive technical catalogue.

## Àríyá
Àríyá may propose/invoke only registered actions. It cannot invent arbitrary database mutations or provider calls.

The assistant must display:
- what action it proposes
- target record
- material consequences
- whether confirmation/approval is required

## API/MCP
Public/action endpoints and MCP tools may map to Action definitions where appropriate. The registry does not mean every UI action is automatically public.

## Automation
Automation actions should reuse Action contracts or explicitly registered automation-only actions, preserving permission/risk semantics.

## Plugins and connectors
Plugins may register namespaced actions.
Connectors may provide provider-backed implementations behind approved domain actions.

Example:
`domain.renew` may use a registrar connector, but the user-facing action remains a Re:Solve domain action.

## Bulk actions
Bulk eligibility is explicit. High-impact actions should not become bulk-capable merely because the table supports selection.

## Acceptance criteria
- action semantics are reusable across interfaces
- authorization happens at execution time, not only when rendering UI
- Àríyá cannot bypass registered action policy
- plugin/connector actions remain permissioned and auditable
- action labels/consequences are consistent across surfaces
