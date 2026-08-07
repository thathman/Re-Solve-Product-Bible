# Secure Vault

## Purpose
Secure Vault is Re:Solve's controlled workspace for confidential information and protected documents/files. It is not merely a password manager and it is not ordinary File storage.

## Protected item types
Examples:
- credential;
- API key/token;
- SSH key/certificate;
- recovery code;
- secure note/instruction;
- confidential Proposal/Contract document;
- signed agreement;
- legal/private/financial document;
- protected evidence/attachment.

## Domain identity
A protected confidential document is a **Vault Item**, not simultaneously an ordinary File record with a second access route.

Vault and Files may share provider-neutral storage infrastructure, but authorization/domain identity stay separate.

If ordinary content is promoted into Vault, ordinary File links/shares/search/download access must be removed or invalidated while provenance to the originating business record is retained.

## Core records
Vault Item, Vault Version, Vault Share, Vault Access Grant, Vault Access Request, Vault Access Event, Vault Rotation Record, Vault Category and Vault Policy.

Access Event can classify reveal, copy, download, share, revoke, failed access, export and other sensitive operations.

## Principles
- least privilege;
- object-level authorization plus Organisation/Property/Project scope;
- encrypted storage/transport according to implementation security model;
- masked metadata-first lists;
- no secret values in generic Search/Notifications/Activity/API/MCP/Àríyá;
- every sensitive reveal/copy/download/share/revoke is append-only audited;
- temporary access expires automatically;
- client and staff access policies are independently enforceable;
- protected documents link to authoritative business records without duplicating their commercial state.

## Main workspace
Views:
- My Access
- Authorized Items
- Credentials
- Confidential Documents
- Shared With Clients
- Access Requests
- Expiring / Rotation Due
- Audit

Lists show safe metadata only: name/type, Organisation/Property/Project, owner, access level, last access, expiry/rotation and status.

## Item workspace
Sections:
- Overview metadata;
- protected content action;
- Access;
- Versions;
- Linked Records;
- Rotation/Expiry;
- Activity/Audit summary.

Reveal/copy/download is never automatic when opening the record.

## Step-up authentication
Policy can require recent stronger authentication for actions such as:
- reveal/copy high-sensitivity secret;
- protected download/export;
- change privileged Access Grant;
- create high-risk share;
- rotate sensitive connector credential;
- delete/purge protected item.

Step-up validity is bounded and security-event aware.

## Access Grants / Sharing
A Grant/Share defines:
- recipient Principal/User or approved client scope;
- specific Item;
- allowed operations;
- start/expiry;
- re-share permission;
- approval requirement;
- reason/purpose where required;
- grantor;
- revoke state.

Following an Organisation/Property or having ordinary File access does not grant Vault access.

## Access Requests
Users may request specific access with reason and duration. Approval routes through shared Approval policy/item owner. Denied/expired/revoked state remains auditable.

Attention may remain open while a request awaits decision.

## Credentials
Metadata may include username/account label, URL, environment, owner, linked Property/system, rotation due/last rotated and optional external-vault reference.

Secret material is stored separately from ordinary metadata and masked by default.

## Confidential documents
Commercial/legal source records such as Proposal/Contract remain outside Vault as first-class business records.

A protected rendered/final document may be represented by a Vault Item linked to:
- Document Studio Final Snapshot;
- Contract/Proposal;
- Organisation/Property/Project;
- retention/access policy.

No parallel ordinary File download route should remain for the protected content.

## Rotation / expiry
Credential lifecycle may include:
- rotation owner;
- due/reminder policy;
- last rotated;
- evidence/reference;
- linked Connector/Property;
- manual/automated rotation state.

Plugins/Connectors may assist rotation through registered high-risk Actions. Core supports safe manual lifecycle without requiring an external vault product.

## External Vault Connector
OpenBao or another external secrets system can optionally strengthen/host secret material behind a `VaultConnector`. Re:Solve product behavior must not depend on one external secrets provider.

## Permissions
Canonical examples:
- `vault.metadata.read`
- `vault.items.create`
- `vault.items.manage`
- `vault.secret.reveal`
- `vault.secret.copy`
- `vault.file.download`
- `vault.items.share`
- `vault.access.request`
- `vault.access.approve`
- `vault.access.manage`
- `vault.audit.read`
- `vault.policy.manage`
- `vault.items.delete`

All are further constrained by object/scope grants.

## Attention / Notifications
Attention:
- access request awaiting decision;
- rotation overdue;
- Item expiring;
- temporary Grant nearing expiry when action required;
- suspicious/repeated access failure requiring review.

Notifications may cover request outcome, share/revoke/expiry, rotation and security policy events. Do not include raw protected values in any channel.

## Automations
Examples:
- rotation due -> Attention/notify owner;
- temporary Grant expiry -> revoke;
- Membership/Property access removed -> reevaluate inherited Vault access;
- offboarding -> access-review workflow;
- Contract executed -> protect final signed document if policy requires;
- Property archived -> review linked Vault Items.

## Search / AI / MCP
Generic Search returns only safe metadata when the caller has metadata permission.

Default MCP exposure is metadata-only:
- search_vault_metadata
- list_credentials_due_for_rotation
- request_vault_access

Direct secret reveal through MCP/Àríyá is disabled by default. If a future deployment deliberately enables a narrow high-trust flow, it requires explicit policy, human confirmation/step-up and full Audit. Bulk secret retrieval is never normalized.

Àríyá may explain that an Item exists/needs rotation when metadata is authorized, but should not ingest raw secrets into ordinary conversation history.

## API
Ordinary endpoints are metadata-first.

Protected retrieval uses dedicated privileged operations with:
- fresh authorization;
- step-up where configured;
- minimal response lifetime;
- no caching;
- append-only Audit;
- short-lived download URL/secure streaming for protected files.

## PWA/mobile
Metadata/access request/Approval and individual protected action can work on mobile when policy allows.

Protected content is never offline cached. Screenshot prevention cannot be guaranteed and must not be claimed as a security control.

## Data export / privacy
Generic client/admin exports exclude Vault secret values. Any protected export is an explicit high-risk Vault action and follows retention/access policy.

## Acceptance criteria
- ordinary File access cannot bypass Vault;
- lists/search never reveal secret value;
- reveal/copy/download/share/revoke are auditable;
- expired/revoked Grants stop access immediately;
- Membership/scope removal revokes inherited access as designed;
- offline caches/Notifications/Àríyá/MCP cannot leak protected content;
- optional external Vault providers remain replaceable;
- protected commercial documents retain business-record provenance.

## Lovable build slices
1. metadata list/item workspace + permission model.
2. credential reveal/copy + step-up/Audit.
3. confidential document flow + File promotion boundary.
4. Shares/Access Requests/Approvals.
5. rotation/expiry/Attention.
6. client-authorized Vault Portal experience.
7. optional external VaultConnector support.
