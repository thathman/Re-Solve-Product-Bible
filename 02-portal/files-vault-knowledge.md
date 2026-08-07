# Client Portal — Files, Secure Vault, and Knowledge

## Purpose
Provide three clearly separated information experiences: normal shared files, confidential Vault items, and reusable client-facing operational knowledge.

## Files
Files is for ordinary project, billing, property and organisation documents.

Capabilities:
- browse by recent, project, property, category and folder/collection
- search by filename/title/tags
- preview supported formats
- download when permitted
- upload where a workflow allows it
- see version, owner/source, related record and updated time
- distinguish client-uploaded and staff-shared content

Client uploads must enter a defined workflow and may trigger notifications/tasks. Malware scanning and allowed-type/size policies apply.

## Secure Vault
Vault is visually and behaviorally distinct from Files. It contains credentials, secrets and confidential files explicitly shared with the current user.

Capabilities may include:
- list permitted items
- request access
- reveal/copy a secret
- download confidential file
- acknowledge receipt
- view access expiry
- revoke own temporary share where appropriate

Step-up authentication may be required. Every reveal, copy, download, grant and revocation is auditable. Offline caching of secret values is prohibited.

## Knowledge
Knowledge gives clients reusable guidance scoped to their organisation, property, service or role.

Capabilities:
- browse spaces/categories
- search
- open article
- related articles
- recently updated
- suggested guidance based on property/service context

Re:Solve Knowledge is separate from Chatwoot support Knowledge. Support FAQ/agent knowledge remains a Chatwoot concern where used.

## AI
Optional Portal AI retrieval may search only content the caller can already read. Vault values are excluded from generic retrieval. Confidential files require explicit policy before AI processing.

## Notifications
Examples: file shared, new file version, client upload processed, Vault access granted/expiring/revoked, knowledge article materially updated when subscription rules apply.

## API / MCP
Separate scopes for files, Vault metadata, Vault reveal and knowledge. Generic MCP search must never leak Vault values.

## Mobile/PWA
Files and Knowledge may support safe offline reading under retention policy. Vault secrets never persist in offline caches. Preview and upload interactions must work from mobile file pickers/camera where allowed.

## Lovable build slices
1. Files library and contextual record files.
2. Knowledge browse/search/article.
3. Vault list and permission states.
4. Vault step-up/reveal/access flows.
5. Mobile/offline security and polish.