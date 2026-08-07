---
name: resolve-mcp
description: Use when adding, changing, documenting, or reviewing Re:Solve MCP tools/resources, MCP clients, scopes, AI-agent access, confirmations, redaction, or tool audit behavior.
---

# Re:Solve MCP

Read `07-api/mcp.md`, Action Registry, API contracts, canonical permissions, Àríyá boundaries, Vault rules and security architecture.

## Principle
MCP exposes curated business tools/resources, never arbitrary SQL, filesystem, provider SDK or unrestricted database access.

## Tool contract
Every tool declares:
- stable name and user/agent-oriented description;
- input/output schema;
- read-only / low-risk write / sensitive write / destructive-high-risk class;
- required scopes/capabilities;
- organisation/property/object authorization;
- confirmation, approval or step-up requirement;
- redaction policy;
- audit policy;
- rate-limit class;
- idempotency/side-effect behavior;
- deep-link/source references where useful.

## Reuse
Call shared Re:Solve domain services/registered Actions rather than building an alternate business-logic stack.

## Vault
Generic MCP tools do not reveal Vault secrets. Metadata may be exposed under narrow scope. Secret reveal remains disabled by default and bulk secret access is prohibited.

## Support
Do not turn MCP into a second Chatwoot/Captain runtime. Expose only authorized Re:Solve support context and connector-backed summaries explicitly designed for MCP.

## Client identities
MCP clients have separate credentials, owner, status, expiration, scopes, allowed tool categories and optional organisation/property restrictions. Human UI sessions are not reused as broad MCP credentials.

## Audit
Record client, tool, safe input summary, target records, result, duration, correlation id and confirmation/approval reference without logging secret values.

## Completion
Verify denied scopes and cross-client access fail server-side, dangerous tools cannot run under broad default scopes, schema descriptions are agent-readable, tool errors are safe, and every tool call is auditable.