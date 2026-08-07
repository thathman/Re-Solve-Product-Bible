# Àríyá — Re:Solve AI

## Purpose
**Àríyá** is Re:Solve's built-in intelligence layer and user-facing AI operator. Àríyá helps users understand records, find information, draft work, detect operational risk, summarize complex situations and execute carefully controlled actions.

Àríyá is separate from Chatwoot Captain. Chatwoot retains its own support AI, support prompts, support Knowledge and support runtime.

Internal technical objects may still use names such as `AIProvider`, `AIProfile`, `AIRun`, `AITool` and `AIConnector`.

See `04-ai/ariya-experience.md` for product identity and interface behavior.

## Product goals
- reduce operational scanning/repetitive writing;
- make dense business information understandable;
- surface important Attention, changes and risks;
- provide natural-language search over permitted Re:Solve data;
- support controlled registered actions without bypassing permissions;
- expose reusable AI capability to Admin and selected Portal experiences;
- remain provider-abstracted;
- show evidence/source/freshness for material business claims.

## Non-goals
- replacing Chatwoot Captain;
- unrestricted autonomous operation;
- arbitrary SQL/database access;
- unrestricted external HTTP/provider access;
- generic Vault secret retrieval;
- exposing data outside caller scope;
- silently sending/accepting/signing consequential commercial documents.

## Provider model
Àríyá consumes an `AIConnector`/provider abstraction. Initial preferred provider may be OpenRouter while the product remains provider-neutral.

Configuration may define default/fast/reasoning/long-context/fallback/embedding models, limits and per-feature routing.

## AI Gateway
All provider requests flow through a Re:Solve AI Gateway responsible for:
- caller Principal;
- feature/context;
- provider/model routing;
- tool/action registry;
- permissions;
- usage/budget;
- redaction/data policy;
- timeout/retry;
- audit metadata;
- safety/guardrails.

Business features do not call provider SDKs directly.

## Surfaces

### Global Àríyá
Accessible through TopBar and Command Palette. It can answer questions and propose/invoke permitted actions.

Examples:
- What needs my attention today?
- Which clients have overdue invoices and active project risk?
- Show properties with renewals in the next 30 days.
- Explain why this Property is degraded.
- Draft a client update for this project.

### Record Àríyá
Available contextually in selected Organisation, Contact, Property, Project, Opportunity, commercial/billing, Request, Incident, Knowledge and document workspaces.

Context is provided by controlled tools/services rather than unrestricted page/database scraping.

### Operational Briefing
Àríyá briefing may prioritize:
- Attention
- My Work
- approvals
- renewals
- Property Posture/incidents
- commercial risk
- overdue receivables
- client actions
- important notifications/deadlines

Every important item links to source evidence.

### Drafting
May draft:
- proposal scope/narrative
- contract/SOW narrative
- project/client updates
- email/WhatsApp message
- report narrative
- internal note
- knowledge article

Drafts remain drafts until deliberately applied/sent/published unless an explicitly approved Automation governs the next action.

### Analysis
Potential analyses include client risk/attention, project slippage, renewal exposure, receivables, Property Posture patterns, opportunity forecast context and data-quality explanation.

The UI distinguishes AI inference from deterministic facts.

## Tool and Action model
Àríyá uses controlled read tools and the shared Command and Action Registry for mutations.

Examples of read tools:
- get_organisation_summary
- search_contacts
- get_property_posture
- get_project_status
- list_attention
- get_invoice_status
- search_knowledge
- get_request

Examples of registered writes:
- create_task
- create_reminder
- draft_client_update
- create_request
- run_allowed_workflow

Connector-backed reads/actions remain behind provider-neutral capability contracts.

## Permissions
Àríyá never expands authority.

Every tool/action performs fresh server-side authorization using caller Principal, capability and scope.

If the caller cannot view/reveal/change something normally, Àríyá cannot reveal/change it.

## Sensitive information
### Vault
Default AI access excludes raw passwords, tokens, keys and confidential value retrieval. Authorized metadata may be searchable when policy allows.

### Files/Documents
Àríyá may process authorized ordinary files/documents. Vault-protected documents follow stricter policy.

### Personal/client data
Send only the minimum provider context required and honor configured provider data-class policy.

## Chatwoot separation
Chatwoot Captain remains responsible for support-answer generation and Chatwoot support Knowledge. Àríyá may query safe provider-neutral support summaries/references when operational context requires it.

## Knowledge retrieval
Àríyá uses Re:Solve Knowledge under caller-aware visibility. Draft/internal content never leaks to client users.

## Sources, provenance and freshness
Material answers should expose source records and freshness where interpretation depends on them. Synced/derived values follow Data Provenance rules.

Àríyá must distinguish:
- current deterministic fact;
- stale/unknown source;
- AI inference;
- suggested action;
- completed registered action.

## AI activity and audit
Track feature, caller, provider/model, duration, usage, tool/action calls, target records, confirmations/approvals and outcome according to retention policy.

Do not retain full sensitive prompts/responses indefinitely solely for debugging.

## Usage and limits
Settings expose provider/model state, usage, cost where available, budgets, rate limits and feature/role limits. Budget/availability issues may produce Attention/Notifications.

## Guardrails
Configurable controls may:
- disable write actions;
- disable selected tools;
- require confirmation for writes;
- require approval/step-up for high-impact actions;
- restrict roles/organisations/properties;
- restrict provider data classes;
- cap request/output size.

## Portal Àríyá
Optional and separately permissioned. It is narrower than staff Àríyá.

Potential uses:
- summarize own project;
- explain own invoice;
- find client-visible Knowledge;
- explain own Property/incident status;
- explain an approval/request/renewal action.

Never expose internal notes, other clients, staff-only risk reasoning, unreleased documents or Vault secrets.

## Notifications and Attention
Àríyá may summarize Attention/Notifications and may propose an AI-derived Attention signal when clearly labeled. Deterministic policy owns notification priority/delivery and authoritative Attention state.

## Automations
AI may be a controlled Automation step for classify, summarize, draft, extract and prioritize. Downstream side effects follow Action Registry/Automation permissions.

## API and MCP
External agents should normally consume underlying Re:Solve tools/actions directly rather than recursively calling Àríyá as an unrestricted proxy.

## Failure states
Handle provider/model unavailable, timeout, budget exceeded, tool denied, stale/unavailable source, context too large and output validation failure without corrupting business records.

Àríyá should explicitly say when it lacks access/evidence rather than fabricate success.

## Acceptance criteria
- Àríyá is the user-facing AI name;
- Chatwoot Captain remains separate;
- provider can be replaced without rewriting domains;
- caller scope is enforced at tool/action execution;
- Vault secrets remain unavailable to generic AI retrieval;
- evidence/freshness and inference are distinguishable;
- writes reuse registered Action policy;
- usage/tool activity is auditable;
- provider failure does not corrupt records.

## Lovable build slices
1. Àríyá visual identity/trigger/panel within Core UI foundation using demo state only.
2. AI settings/provider/model configuration UI.
3. AI Gateway contracts and read-only tool registry.
4. Global Àríyá using read-only demo/real tools.
5. Record summaries and drafting.
6. Operational Briefing from Attention.
7. Action Registry integration + confirmation.
8. usage/audit views.
9. Automation AI steps.
10. optional Portal Àríyá.
