# Secure Vault

## Purpose
Secure Vault is Re:Solve's controlled workspace for confidential information and sensitive files. It is not merely a password manager and it is not general file storage.

## Vault item types
- credential
- API key / token
- SSH key / certificate
- recovery code / secure note
- confidential document
- proposal file
- contract file
- financial/private record
- access instruction
- other sensitive attachment

## Core records
Vault Item, Vault Version, Vault Share, Vault Access Grant, Vault Access Request, Vault Reveal Event, Vault Download Event, Vault Rotation Record, Vault Category, Vault Policy.

## Principles
- least privilege
- explicit scope to organisation/property/project where applicable
- encrypted storage and secure transport
- sensitive values are never exposed in normal lists/search results
- every reveal/download/share/revoke event is auditable
- client and staff permissions are separate
- confidential documents remain linked to their source business record when one exists

## Vault workspace
Views:
- My Access
- All Authorized Items
- Credentials
- Confidential Files
- Shared With Clients
- Access Requests
- Expiring/Rotation Due
- Audit

Lists show metadata only: name, type, organisation/property, owner, access level, last accessed, expiry/rotation, status.

## Item workspace
Sections:
- overview metadata
- secret/file content action
- access
- versions
- linked records
- rotation/expiry
- activity/audit

Reveal/download requires explicit user action. Optional step-up authentication can be required by policy or item sensitivity.

## Sharing
A share defines recipient/user/group, scope, access capability, expiration, whether re-sharing is allowed, whether download/copy/reveal is permitted, and optional approval requirement.

Temporary access must expire automatically.

## Access requests
User can request access with reason and duration. Approval flow routes to item owner/policy approver. Denied and expired requests remain auditable.

## Credentials
Credential fields may include username, password/secret, URL, notes, environment, owner, rotation due, last rotated, external vault reference, property/system context.

Secret values must be masked by default and never included in generic API/MCP search results.

## Confidential documents
Sensitive files use the same access-policy model as secrets. Proposal/contract records may link to Vault-protected versions while their commercial metadata remains outside Vault.

## Rotation
Support due date, reminder schedule, rotation owner, last rotation, evidence, linked connector/system. Future plugins may automate rotation, but core must support manual lifecycle safely.

## Permissions
vault.metadata.read, vault.create, vault.manage, vault.reveal, vault.copy, vault.download, vault.share, vault.access.request, vault.access.approve, vault.audit.read, vault.policy.manage.

Permissions are subject to object-level grants and organisation/property scope.

## Notifications
access requested, access approved/denied, share created/revoked/expiring, credential rotation due/overdue, item expiring, suspicious access event, high-sensitivity reveal if policy requires owner notification.

## Automations
- rotation due → notify owner
- temporary grant expires → revoke automatically
- staff/client access removed → revoke related vault grants
- property archived → review linked vault items
- contract executed → secure final signed copy if configured

## API
API defaults to metadata. Secret retrieval uses dedicated privileged endpoints with step-up/authorization checks, minimal response lifetime, audit, and no caching. File downloads use short-lived authorized URLs or equivalent secure streaming.

## MCP
Default MCP exposure is metadata-only. Candidate tools: search_vault_metadata, list_credentials_due_for_rotation, request_vault_access. Direct secret reveal should be disabled by default and only possible through an explicit high-trust configuration with human confirmation; never expose bulk secrets.

## PWA/mobile
Metadata, access requests, approval, and individual reveal/download may be mobile-capable. Sensitive content must never be cached for offline use. Screenshots cannot be reliably prevented across platforms, so policy should not claim otherwise.

## Acceptance criteria
- unauthorized list/search reveals no secret content
- reveal/download/share is audited
- expired grants stop access immediately
- removal from organisation/property scope removes inherited access
- sensitive content is excluded from offline caches and normal notification bodies
- generic AI/MCP search cannot leak secrets

## Lovable build slices
1. metadata lists + item workspace + permissions
2. credential reveal/copy flow with audit
3. confidential file flow
4. shares + access requests/approvals
5. rotation/expiry policies
6. advanced external-vault connector support
