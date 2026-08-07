# Re:Solve MCP Platform

## Purpose
Re:Solve exposes a first-class Model Context Protocol surface so approved AI/agent clients such as Claude/Cowork, ChatGPT, OpenClaw/Hermes, Codex and future systems can inspect and perform controlled Re:Solve operations without scraping UI or receiving unrestricted database/provider access.

## Principles
- curated tools/resources, never arbitrary SQL;
- MCP Client is a scoped Principal;
- capability + record-level authorization;
- Organisation/Property isolation;
- read/write/high-impact distinction;
- shared Action Registry for consequential writes;
- source/provenance/freshness in outputs when material;
- minimal structured output;
- Audit every invocation;
- no generic Vault/provider-secret retrieval;
- portable/self-hostable transport.

## MCP administration
Settings > API & MCP > MCP should include:
- enable/disable;
- transport/endpoint configuration;
- Clients/credentials;
- canonical capabilities/scopes;
- allowed tool categories/tools;
- Organisation/Property restrictions;
- read/write policy;
- confirmation/Approval policy;
- rate/usage limits;
- last used/health;
- Audit;
- revoke/rotate.

## Tool categories
Possible categories:
- Clients / CRM
- Properties / Monitoring / Renewals
- Projects
- Requests
- Sales / Documents
- Billing
- Support Context
- Attention / My Work
- Knowledge
- Notifications
- Files
- Automations / Actions
- Reports
- System / Connector Health
- Plugin tools

No HR, Timesheet/Time Entry or Client Service Consumption tools exist.

## Example read tools
- `search_organisations`
- `get_organisation`
- `get_client_health`
- `search_contacts`
- `get_property`
- `get_property_posture`
- `list_expiring_properties`
- `list_active_incidents`
- `get_monitor_history`
- `search_projects`
- `get_project`
- `list_project_blockers`
- `get_request`
- `list_requests`
- `get_proposal_status`
- `get_contract_status`
- `get_invoice`
- `list_overdue_invoices`
- `get_client_balance`
- `get_attention_summary`
- `get_my_work`
- `search_knowledge`
- `list_notifications`
- `search_files`
- `get_support_summary`
- `get_connector_health`
- `run_defined_report`

## Example write tools
Only when explicitly registered/scoped:
- `create_task`
- `update_task`
- `create_request`
- `create_reminder`
- `acknowledge_attention`
- `snooze_attention`
- `draft_project_update`
- `create_client_action`
- `request_vault_access`
- `run_allowed_workflow`

High-impact financial/security/connector/document actions may be confirmation/Approval-gated or unavailable to MCP entirely.

## Action Registry relationship
MCP write tools should map to registered Re:Solve Actions where practical.

The Action definition provides:
- target/context requirements;
- canonical capability;
- risk class;
- confirmation/Approval/step-up rules;
- idempotency;
- Audit;
- output contract.

MCP exposure is explicit per Action. An Action available in UI does not automatically become an MCP tool.

## Risk classes
- read;
- standard write;
- sensitive write;
- high-impact/destructive.

High-impact tools require narrow capability and may require human confirmation/Approval outside the agent flow.

## Data output / provenance
Tool outputs should be structured, concise and minimized.

When material include:
- stable id/human reference;
- source record type;
- status;
- source/provider;
- observed/synced time;
- freshness;
- deep-link/reference;
- deterministic versus derived status.

Agents should not receive an enormous full-record payload when only three fields answer the tool's purpose.

## Vault boundary
Default MCP Vault exposure is safe metadata only under narrow capability.

Possible safe tools:
- search_vault_metadata
- list_credentials_due_for_rotation
- request_vault_access

Generic secret reveal/export is unavailable by default. Never provide bulk secrets. If a future deployment deliberately enables a narrow reveal operation, it must be a dedicated high-trust Action with human confirmation/step-up and Audit—not `get_all_credentials`.

## Files / Documents
MCP may access authorized File metadata/content through controlled resources. Protected Vault documents follow Vault restrictions.

Document Studio tools may draft/generate metadata or proposal content, but sending/accepting/signing/executing a commercial/legal document is never a broad default write tool.

## Support boundary
Tools access Re:Solve provider-neutral Support summaries/references/Incidents under permission. They do not provide unrestricted Chatwoot message archives and do not call Chatwoot Captain as Re:Solve AI.

## Property / Monitoring boundary
Tools expose Re:Solve Property Posture/evidence rather than pretending one monitoring provider is authoritative.

Cloudflare/Uptime Kuma/provider source may appear in provenance, but a connector outage is distinguishable from confirmed Property outage.

## Àríyá relationship
Àríyá and external MCP Clients may use overlapping underlying domain tools, but Àríyá is a Re:Solve product experience and MCP is an external-agent protocol surface.

Do not require external agents to proxy through Àríyá, and do not let Àríyá recursively invoke an unrestricted external MCP identity.

## Tool execution contract
Each tool declares:
- stable name/description;
- input/output schema;
- required canonical capability;
- record scope behavior;
- risk class;
- confirmation/Approval requirement;
- idempotency where needed;
- Audit/redaction;
- rate/usage class;
- provenance/freshness behavior;
- plugin/source ownership.

Authorization rechecks at execution time.

## MCP Client credentials
Record:
- label/client name;
- protected credential hash/reference;
- capabilities;
- status/expiry;
- last used;
- allowed tools/categories;
- Organisation/Property restrictions;
- read/write setting;
- rate/usage limits.

## Audit
Append-only invocation evidence includes Client Principal, tool, timestamp, safe input summary, target records, result state, duration, correlation id and confirmation/Approval reference.

Never store raw Vault/provider secrets merely for Audit.

## API relationship
MCP tools should reuse the same domain services/Action contracts as UI/API wherever practical, while providing AI-friendly schemas and additional restrictions.

MCP has no separate authorization universe.

## Plugins
Plugins may register namespaced MCP tools/resources through core registry and declare permission/risk/provenance. Plugin tools cannot expose unrestricted storage/SQL/provider APIs.

## Abuse / limits
Support per-Client rate limits, action limits, payload/output bounds and disabling/revoking a Client quickly. Repeated denied/high-risk attempts may create Security Audit/Attention according to policy.

## Acceptance criteria
- MCP Clients are revocable/scoped Principals;
- read/write/high-impact tools are explicit;
- cross-Organisation/Property denial is server-side;
- every invocation is auditable;
- writes reuse Action Registry where applicable;
- outputs expose freshness/source when material;
- Vault/provider secrets are not generic tools;
- Chatwoot/monitoring ownership boundaries hold;
- plugin tools inherit platform controls;
- no HR/Timesheet/Client Service Consumption tools exist.

## Lovable build slices
1. MCP Client/credential administration.
2. tool registry + read-only Organisation/Property/Project/Attention tools.
3. invocation Audit/diagnostics.
4. scoped standard writes through Action Registry.
5. confirmation/Approval/high-impact policy.
6. plugin tool registration + Reports/Search resources.
7. client connection documentation/testing.
