---
name: resolve-vault
description: Use when building or reviewing Re:Solve Secure Vault items, credential reveal/copy, confidential file download, access requests, temporary shares, rotation, step-up authentication, or Vault-related API/MCP/AI behavior.
---

# Re:Solve Secure Vault

Read `01-admin/secure-vault.md`, Files, Secure External Access, Security Architecture, PWA and canonical permissions.

## Boundary
Vault is the protected confidential domain. Files is ordinary document storage. A protected confidential document must not retain a second ordinary File access path.

## Default behavior
Lists/search show metadata only. Secret values and protected file contents require an explicit privileged action. No bulk secret exposure.

## Access
Evaluate capability + organisation/property/project/object grant + share policy + expiry + step-up requirement at access time. Temporary grants expire automatically.

## Sensitive actions
Reveal, copy, download, share, revoke, approve access and rotate are separate auditable actions. Use dedicated confirmation/step-up where policy requires it.

## UI
Mask by default. Reveal only after deliberate user action. Show owner, scope, access level, expiry/rotation, last access and request/share state without exposing content. Mobile sensitive views must avoid accidental persistence.

## Storage/cache/logs
Never put secret values in generic search indexes, analytics, logs, notification bodies, error messages, offline caches or generic Àríyá/MCP context. Use short-lived authorized download/reveal responses.

## AI/MCP
Metadata may be exposed under narrow scope. Generic AI/MCP cannot reveal secrets. Confidential document processing requires explicit policy and caller authorization.

## Lifecycle
Support versioning, rotation due, share expiry, access request/approval/denial, revocation and retention/secure deletion policy with durable audit.

## Completion
Test unauthorized metadata/content access, expired grant, cross-organisation/property denial, step-up failure, revocation after an open page, offline behavior and complete reveal/download/share audit.