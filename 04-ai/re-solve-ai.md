# Re:Solve AI

## Purpose

Re:Solve AI is the built-in intelligence layer for operating Re:Solve itself. It helps staff understand records, find information, draft work, detect operational risk, summarize complex situations, and execute carefully permissioned actions.

Re:Solve AI is separate from Chatwoot Captain. Chatwoot retains its own support AI, support prompts, support knowledge, and support runtime.

## Product goals

- reduce operational scanning and repetitive writing
- make dense business information easier to understand
- surface important changes and risks proactively
- provide natural-language search over permitted Re:Solve data
- support controlled actions without bypassing user permissions
- expose reusable AI capabilities to Admin and selected Portal experiences
- remain provider-abstracted

## Non-goals

- replacing Chatwoot Captain
- unrestricted autonomous operation
- arbitrary SQL or raw database access
- reading Vault secrets by default
- exposing data the caller cannot access through normal Re:Solve permissions

## Provider model

Re:Solve AI consumes an `AIConnector`/provider abstraction. Initial preferred provider may be OpenRouter, while the product remains provider-neutral.

Configuration may define:
- default model
- fast model
- reasoning model
- long-context model
- fallback model
- embeddings model where needed
- provider limits
- per-feature model routing

## AI surfaces

### Global Assistant

Accessible from the Admin shell through a command/assistant surface. It can answer questions and invoke permitted tools.

Examples:
- What needs my attention today?
- Which clients have overdue invoices and open projects?
- Show properties with renewals in the next 30 days.
- Summarize Kampala University's current work.
- Draft a client update for this project.

### Record Assistant

Available in selected record workspaces:
- Organisation
- Contact
- Property
- Project
- Opportunity
- Invoice/Commercial records
- Knowledge

It receives record context through controlled tools rather than unrestricted page scraping.

### Daily Briefing

A generated operational briefing prioritizing:
- urgent work
- overdue commitments
- approvals
- property health
- commercial risk
- client actions
- important notifications
- upcoming deadlines

Every briefing item should link to source evidence.

### Summaries

Generate concise summaries of:
- organisation relationship history
- project status
- project activity
- property health
- commercial history
- notification cluster
- document/knowledge content where permitted

### Drafting

Examples:
- project update
- proposal text
- follow-up email
- internal note
- report narrative
- client-facing explanation
- knowledge article draft

AI drafts remain drafts until user submits/sends unless an explicitly approved automation says otherwise.

### Analysis

Potential analyses:
- client attention/risk signals
- project slippage
- overdue dependencies
- workload concentration
- renewal exposure
- receivables summary
- property-health patterns

The UI must distinguish AI inference from deterministic system facts.

## AI Gateway

All AI requests flow through a Re:Solve AI Gateway responsible for:
- caller identity
- feature context
- model routing
- tool registry
- permissions
- usage tracking
- redaction
- timeout/retry policy
- audit metadata
- safety/guardrails

Business features should not call provider SDKs directly.

## Tool model

AI tools are controlled business capabilities.

Examples:
- get_organisation_summary
- search_contacts
- get_property_status
- get_project_status
- list_overdue_tasks
- get_invoice_status
- search_knowledge
- create_task
- draft_client_update
- run_allowed_workflow

Connector-backed tools may include:
- get_ojs_submission_status
- get_store_order_status
- get_monitor_status

Tools inherit caller permissions and record scoping.

## Permission model

AI never expands a user's authority.

If a user cannot view an invoice normally, AI cannot reveal it.
If a user cannot reveal Vault contents, AI cannot reveal them.
If a user cannot modify a project, AI cannot modify it.

Tool execution performs server-side authorization at execution time.

## Sensitive information

### Vault

Default AI access:
- no secret values
- no password/key reveal
- optionally searchable non-sensitive metadata under permission

### Files

AI can process files only where user visibility and file policy permit. Sensitive Vault documents follow stricter policy.

### Personal/client data

Prompts/tools should send the minimum data required for the task. Provider requests must avoid irrelevant PII.

## Chatwoot separation

Chatwoot owns:
- Captain
- support-answer generation
- support knowledge retrieval
- customer-support AI workflows

Re:Solve AI may query safe support summaries through the Chatwoot connector if a Re:Solve workflow needs operational context, but must not become a proxy Captain implementation.

## Knowledge retrieval

Re:Solve AI uses Re:Solve Knowledge with caller-aware visibility.

Knowledge scopes may include:
- internal
- organisation-specific
- property-specific
- portal-visible
- plugin-contributed

Retrieval must preserve visibility at query time and result time.

## AI activity and audit

Track:
- feature
- user/service identity
- model/provider
- start/end
- tokens/usage where available
- tool calls
- target records
- success/failure
- confirmation/approval references

Avoid storing full sensitive prompts/responses indefinitely merely for debugging. Retention and redaction are configurable.

## Usage and limits

Settings should expose:
- provider status
- model status
- usage by period
- usage by feature
- cost where provider returns it
- budget thresholds
- rate limits
- per-role/feature limits

Budget alerts use Notifications.

## AI settings

Sections:
- Provider
- Models
- Feature Routing
- Tools
- Knowledge
- Guardrails
- Usage & Budgets
- Retention
- Audit

## Guardrails

Configurable policies:
- disable write tools globally
- disable specific tools
- require confirmation for writes
- require approval for sensitive actions
- restrict AI to selected roles
- restrict provider data classes
- cap output/input size
- disable AI for selected organisations/properties

## Portal AI

Portal-facing AI is optional and separately permissioned. It must be narrower than staff AI and restricted to client-visible records/knowledge.

Potential uses:
- summarize own project
- explain own invoice
- find client-visible documentation
- understand property status

It must not expose internal notes, staff-only health reasoning, other clients, unreleased documents, or Vault secrets.

## Notifications

AI can generate notification summaries/digests, but deterministic event priority and mandatory delivery rules remain controlled by the Notification Platform.

AI may identify a risk and propose a notification, but the product should visibly mark AI-derived alerts where appropriate.

## Automations

AI can be used as an automation step for:
- classify
- summarize
- draft
- extract structured fields
- prioritize

Any downstream side effect follows normal automation permissions and confirmation rules.

## API and MCP

AI capabilities may be exposed through API/MCP as controlled operations, but external AI clients should generally consume underlying Re:Solve tools directly rather than recursively calling the Re:Solve assistant.

## Failure states

Handle:
- provider unavailable
- model unavailable
- timeout
- budget exceeded
- tool denied
- context too large
- source unavailable
- output validation failure

UI should preserve the user's work and show recovery options.

## Acceptance criteria

- Re:Solve AI and Chatwoot AI remain architecturally separate
- AI provider can be replaced without rewriting business domains
- AI cannot access records beyond caller permission
- every write tool performs fresh authorization
- Vault secrets are unavailable to generic AI retrieval
- AI outputs distinguish inference from system fact where material
- tool calls are auditable
- provider failure does not corrupt business records
- usage/budget visibility exists

## Lovable build slices

1. AI settings/provider/model configuration UI with demo provider state
2. AI Gateway contracts and read-only tool registry
3. Global assistant UI using demo/read-only tools
4. Record summaries and drafting
5. Daily Briefing
6. tool permissions + confirmation
7. usage/audit views
8. automation AI steps
9. optional Portal AI
