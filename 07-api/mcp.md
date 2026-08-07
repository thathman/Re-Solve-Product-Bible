# Re:Solve MCP Platform

## Purpose

Re:Solve exposes a first-class Model Context Protocol surface so approved AI clients such as Claude, ChatGPT, OpenClaw/Hermes, Codex, and future agents can safely inspect and act on Re:Solve data without scraping the UI or receiving unrestricted database access.

## Principles

- curated tools, not arbitrary SQL
- least privilege
- read/write separation
- caller identity and scopes
- organisation/property isolation
- audit every tool call
- redaction of secrets and sensitive fields
- confirmation/approval for dangerous actions
- portable/self-hostable transport

## MCP administration

Settings > API & MCP > MCP includes:
- enable/disable
- transport/endpoints
- client credentials
- scopes
- tools
- allowed organisations/properties where applicable
- rate limits
- last used
- audit
- revoke/rotate

## Tool registry

Tool categories:
- CRM
- Properties
- Projects
- Sales
- Billing
- Support context
- Knowledge
- Notifications
- Files
- Automations
- System health
- plugin tools

Examples:
- search_organisations
- get_organisation
- search_contacts
- get_property
- get_property_health
- list_expiring_properties
- search_projects
- get_project
- create_task
- update_task
- get_invoice
- list_overdue_invoices
- search_knowledge
- get_notifications
- get_support_summary
- run_allowed_workflow

## Risk classes

- read-only
- low-risk write
- sensitive write
- destructive/high-risk

Sensitive/destructive tools may require explicit confirmation, additional scopes, step-up approval, or be unavailable to MCP entirely.

## Vault boundary

MCP does not receive unrestricted Vault secret contents. Vault metadata may be available under narrow scope. Secret reveal/export requires explicit product policy and should default to unavailable.

## Support boundary

MCP may access Re:Solve support context and connector-backed summaries where permitted, but does not become an alternate Chatwoot AI engine and does not receive unrestricted Chatwoot conversation data by default.

## Tool execution

Each tool declares:
- name
- description
- input schema
- output schema
- required scopes
- risk class
- confirmation requirement
- audit policy
- redaction policy
- rate-limit class

## Client credentials

Each AI client record includes:
- label/client name
- credential hash/reference
- scopes
- status
- expiration
- last used
- allowed tools/categories
- optional organisation/property restrictions

## Audit

Record:
- client
- tool
- timestamp
- safe input summary
- target records
- result status
- duration
- correlation ID
- confirmation/approval reference
- safe error

Never persist secret values merely for audit convenience.

## API relationship

MCP tools should call shared domain services/commands also used by the API/UI where practical. MCP is a curated AI interface, not a separate business-logic stack.

## Plugin relationship

Plugins can register namespaced MCP tools through the MCP registry. Plugin tools inherit core scopes, risk classification, audit, and health rules.

## Acceptance criteria

- clients can be issued/revoked scoped credentials
- read/write tools are clearly distinguished
- cross-scope/organisation/property access is denied server-side
- every tool call is auditable
- dangerous actions cannot execute through broad default scopes
- Vault secrets and provider credentials are not exposed by generic tools
- plugin tools inherit platform controls

## Lovable build slices

1. MCP client/credential management
2. tool registry + read-only core tools
3. audit viewer
4. scoped write tools
5. confirmation/approval model
6. plugin tool registration
7. client connection documentation and diagnostics
