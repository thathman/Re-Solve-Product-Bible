# Re:Solve Security Architecture

## Purpose

Security is a platform property, not a feature added after implementation. Every Re:Solve surface—Admin, Client Portal, API, MCP, plugins, connectors, automations, files, Vault, notifications, and AI—must enforce consistent identity, authorization, isolation, audit, and secret-handling rules.

## Security goals

- strong identity assurance
- least privilege
- organisation and property isolation
- explicit permission checks server-side
- safe handling of confidential data
- auditable sensitive actions
- secure external integrations
- recoverability and operational visibility
- portable/self-hosted security posture

## Identity

Canonical identity concepts:
- User
- Person/Contact
- Membership
- Role
- Permission Grant
- Service Identity
- API Client
- MCP Client
- External Identity Mapping

Email is not the canonical identity key.

## Authentication

Support according to configured policy:
- password
- magic link
- MFA
- OAuth/SSO later where needed
- service/API credentials

Security settings must allow administrators to control allowed methods without weakening minimum safe defaults.

## MFA

Support step-up/MFA for:
- account security changes
- Vault reveal/download where configured
- API token creation
- sensitive connector credential changes
- high-risk financial actions
- role/permission administration

## Sessions

Session controls:
- list active sessions/devices
- revoke one/all
- last used
- location/device metadata when safely available
- absolute/session inactivity expiry
- suspicious session notification policy

## Authorization

Use capability-based permissions rather than route-only role checks.

Authorization inputs may include:
- actor
- permission
- organisation scope
- property scope
- record ownership/assignment
- client/staff surface
- record visibility
- connector/plugin constraints

UI hiding is convenience only. Server-side authorization is mandatory.

## Isolation

Negative authorization tests are required for:
- cross-organisation access
- cross-property access
- internal vs portal-visible data
- Vault access
- connector instances
- support context
- file downloads
- API/MCP tools

A user belonging to multiple organisations must resolve scope explicitly and never inherit unrelated access accidentally.

## Sensitive data classification

At minimum:
- Public
- Internal
- Client Confidential
- Sensitive
- Secret

Policies determine:
- visibility
- logging/redaction
- AI eligibility
- export eligibility
- retention
- notification content

## Secure Vault

Vault is the primary controlled-sharing surface for secrets and sensitive confidential files.

Requirements:
- encryption at rest using approved implementation
- narrow permissions
- step-up support
- access requests
- temporary grants
- reveal/download audit
- revocation
- secure deletion/retention policy
- no secret values in generic logs, notifications, AI prompts, analytics, or search indexes

## Files

Normal files use permissioned storage. Sensitive content should be explicitly moved/routed to Vault based on policy rather than relying on ordinary file visibility.

Signed download URLs or equivalent access should be short-lived and scoped where implementation supports them.

## Connectors

Connector security requirements:
- credentials stored through approved secret mechanism/reference
- signature/auth verification for webhooks
- idempotency
- replay protection where provider protocol supports it
- TLS
- rate limiting
- masked logs
- credential rotation
- connector-specific least privilege

## Plugins

Plugins declare permissions and dependencies.

Minimum protections:
- named permissions
- namespaced data/routes
- no casual arbitrary secret access
- migration validation
- lifecycle kill switch
- health and audit

Full OS-process sandboxing is not a v1 requirement, but plugins must not be treated as omnipotent by default.

## API

API security:
- scoped credentials
- expiration/revocation
- rate limiting
- audit
- idempotency where relevant
- standard validation
- consistent authorization
- no raw database endpoints

## MCP

MCP security:
- curated tool registry
- per-client scopes
- risk classes
- confirmations/approvals
- audit each call
- Vault secret reveal unavailable by default
- no arbitrary SQL/filesystem/provider access

## AI

AI inherits caller permissions and data classification.

Rules:
- minimize provider payloads
- no generic Vault secret access
- no hidden permission expansion
- mark inference where materially different from deterministic fact
- configurable retention/redaction
- write actions use normal authorization

## Notifications

Notification content must respect classification.

Examples:
- do not put passwords or private contract contents in push/WhatsApp previews
- use deep links to authenticated surfaces for sensitive detail
- mandatory security events cannot be muted where policy requires delivery

## Audit

Audit high-value actions such as:
- authentication/security changes
- role/permission changes
- Vault reveal/share/download
- API/MCP credentials
- connector credentials/configuration
- plugin lifecycle
- financial changes
- destructive deletes
- sensitive exports
- automation actions

Audit records should be append-oriented and protected from ordinary user modification.

## Logging

Logs must exclude or redact:
- passwords
- API keys
- auth tokens
- session tokens
- private keys
- Vault secret content
- full sensitive webhook payloads where unnecessary

Use correlation/request IDs to debug without dumping confidential data.

## Validation and common web protections

Implementation must address:
- XSS
- CSRF where applicable
- injection
- insecure direct object reference
- mass assignment
- upload validation
- path traversal
- SSRF in connector/url workflows
- brute force
- rate abuse
- unsafe redirects
- dependency vulnerabilities

## File uploads

Validate:
- type
- size
- extension/content mismatch
- permission
- destination classification
- malware scanning capability where deployed

Uploads are never trusted solely by client-side validation.

## Destructive actions

High-impact actions require:
- explicit permission
- contextual confirmation
- clear object names/consequences
- audit
- recoverability/archive where practical

Avoid unnecessary hard deletes.

## Security events and notifications

Potential events:
- new sign-in/device
- MFA changed
- password changed
- API/MCP token created/revoked
- suspicious repeated failure
- connector auth expired
- Vault access granted/revealed
- privileged role changed

Delivery priority depends on event severity and policy.

## Security Admin area

Settings > Security includes:
- Authentication
- MFA
- Password Policy
- Sessions
- Roles/Permissions link
- API/MCP credential security
- Rate Limits
- Security Events
- Data/Retention policies where appropriate

## Backup and recovery

Security architecture includes recovery:
- documented backups
- encrypted backups where appropriate
- restore testing
- credential restoration/rotation procedure
- audit preservation

## Acceptance criteria

- authorization is server-side and capability/scoped
- cross-organisation/property negative tests exist
- Vault secrets do not appear in logs/AI/notifications/search
- API/MCP credentials are revocable and auditable
- connector webhooks are verified and idempotent
- sensitive actions produce audit records
- session/security controls are user/admin visible as appropriate
- uploads and downloads enforce permission at request time
- production configuration rejects known insecure defaults

## Lovable build slices

1. permission/scoping framework + negative tests
2. session/security settings UI
3. audit coverage for sensitive actions
4. Vault step-up/access policy
5. API/MCP credential security
6. connector/plugin security checks
7. upload/download hardening
8. security event center and notifications
