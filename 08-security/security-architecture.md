# Re:Solve Security Architecture

## Purpose
Security is a platform property. Admin, Client Portal, Secure External Access, API, MCP, Plugins, Connectors, Automations, Files, Vault, Notifications, Monitoring and Àríyá enforce consistent Principal identity, authorization, isolation, Audit and sensitive-data handling.

## Goals
- strong identity assurance;
- least privilege;
- Organisation/Property/record isolation;
- server-side capability + scope authorization;
- safe confidential-data handling;
- append-only evidence for sensitive actions;
- controlled external access/integrations;
- recoverability and operational visibility;
- portable/self-hosted security posture.

## Identity model
### Principal
General authorization actor:
- Human User;
- Service Account;
- API Client;
- MCP Client;
- Plugin;
- Connector.

### Human User / Contact / Membership
User is authenticated human identity. Contact is business person record. Membership links User to Organisation context/access.

### External Identity Mapping
Provider identity mapping never replaces canonical Re:Solve Principal/User/Contact identity.

Email is not a universal canonical identity key.

## Authentication
Configured policy may support password, magic link, MFA and later OAuth/SSO/passkey-compatible options where appropriate to implementation.

Machine Principals use dedicated credentials—not shared human passwords.

## MFA / step-up
Step-up may be required for:
- account/MFA/security changes;
- Vault reveal/copy/download/export;
- privileged API/MCP credential creation;
- Connector credential rotation;
- production DNS/registrar/security changes;
- high-impact financial Actions;
- role/access administration;
- ownership transfer;
- destructive System/Plugin/Connector Actions.

Step-up has bounded validity and can be invalidated by risk/session changes.

## Sessions/devices
Support active session/device visibility, revoke one/all, last used, safe device/location metadata, inactivity/absolute expiry and suspicious-session policy.

## Authorization
Every protected operation evaluates:
- Principal;
- canonical capability;
- Workspace/Operating Entity/Organisation/Property/record scope;
- ownership/assignment where relevant;
- surface/audience;
- record visibility/classification;
- Connector/Plugin constraints;
- temporary Grant expiry;
- Action Registry risk/confirmation/Approval policy.

UI hiding is convenience only. Deep links, API, MCP and Àríyá always reauthorize server-side.

## Negative authorization testing
Required across:
- cross-Organisation;
- cross-Property/descendant scope;
- staff/internal versus client-visible data;
- Comments/Internal Notes;
- Vault;
- ordinary File downloads/shares;
- commercial/Billing;
- Support references;
- Connector Instances/mappings/events;
- Search/Attention/Notification counts;
- API/MCP/Àríyá tools;
- Secure External Access expiry/revocation;
- Saved Views/shared Reports.

A hidden record must not leak existence/title/count through secondary surfaces.

## Data classification
Initial conceptual classes:
- Public
- Internal
- Client Confidential
- Sensitive
- Secret

Classification informs visibility, logs/redaction, AI/provider eligibility, export, retention, Notification previews, cache policy and guest access.

## Action Registry security
Consequential mutations use registered Actions where applicable.

Actions declare:
- required capability/scope;
- risk class;
- target/context;
- confirmation;
- Approval/step-up;
- idempotency;
- Audit;
- UI/API/MCP/Àríyá availability.

An Action being visible in one interface does not imply it is available to every Principal or interface.

## Secure External Access
Guest access is a narrow grant, not a pseudo-Portal account/general API token.

Requirements:
- strong unguessable token stored/validated securely;
- exact resource/action scope;
- expiry/revocation;
- optional email/OTP verification;
- use/download limits where needed;
- no hidden internal identifiers/data leakage;
- server-side authorization on every request;
- Audit for material view/accept/upload/sign actions;
- no generic Vault secret guest-link behavior.

Expired/revoked links stop immediately.

## Vault / Files boundary
Vault is protected content domain.

Requirements:
- narrow object-level permissions;
- step-up/access requests/temporary Grants;
- reveal/copy/download Audit;
- secure retention/deletion;
- no secret values in generic logs, Notifications, Search, Àríyá, analytics, exports or caches.

Ordinary Files use separate access policy. A protected confidential document must not retain a parallel ordinary File access path.

Signed URLs/streams are short-lived and reauthorized as implementation allows.

## Connector security
- least-privilege provider credentials;
- protected credential references;
- webhook/auth verification;
- idempotency/replay handling;
- TLS;
- rate limiting;
- safe logs;
- rotation/reauthorization;
- explicit sync authority/conflict policy;
- high-impact provider writes behind registered Actions.

A Connector failure cannot be silently interpreted as target/business-record state.

### Cloudflare / DNS / registrar
Production DNS, registrar, auto-renew, TLS/security changes are high-impact. Initial integration should be read-first and writes need specific capabilities, confirmation and possibly step-up/Approval.

## Native Monitoring security
Monitoring targets/configuration can introduce SSRF/network risks.

Controls should include:
- validated target schemes/types;
- policy on private/internal network targets;
- DNS rebinding/redirect considerations;
- timeout/size limits;
- protected auth headers/credentials;
- probe authentication;
- rate/concurrency controls;
- signed/authenticated Monitoring Worker result submission;
- no secret echo in evidence/errors.

Monitoring Workers/Probes are scoped Service Account Principals and cannot receive broad application DB access by default.

## Plugins
Plugins declare canonical permissions, Actions, data/migrations, Connector registrations and extension slots.

Protections:
- namespaced data/routes;
- no arbitrary secret access;
- migration validation/recovery;
- kill switch;
- Core UI/navigation governance;
- health/Audit;
- no assumption of omnipotent DB access.

## API
API Client credentials are scoped/expiring/revocable/rate-limited/auditable. Validation, idempotency/concurrency and record authorization are consistent. No raw DB/provider endpoints.

## MCP
Curated tools/resources; per-Client capability/scope; Action Registry for writes; Audit each call; output minimization; no arbitrary SQL/filesystem/provider access; Vault reveal unavailable by default.

## Àríyá
Àríyá inherits caller Principal permissions/scope and configured data policy.

Rules:
- minimum context sent to provider;
- source/freshness visible;
- inference distinguishable from fact;
- no generic Vault secret retrieval;
- registered Actions only for writes;
- confirmations/Approvals respected;
- Portal context cannot access internal records;
- provider failure cannot fabricate success.

## Notifications / communications
Sensitive content is minimized in push/email/WhatsApp previews. Deep-link to authenticated surfaces for detail.

Destinations/recipient eligibility follow privacy/communication policy. Mandatory security notices follow policy even when optional notifications are disabled.

## Privacy / retention / data rights
Privacy workflows support verified data access/correction/deletion/anonymization requests according to policy while respecting legal/operational holds and required financial/Audit retention.

Connector deletion propagation is only claimed when provider evidence confirms it.

## Audit
Audit Event is **append-only** accountability evidence.

Do not mutate a historical Audit Event to `correct` it. A correction/annotation creates subsequent evidence.

Audit high-value actions including:
- auth/security/session;
- role/permission/grants;
- Vault access/share/reveal/download;
- API/MCP credentials/actions;
- Secure External grants/material outcomes;
- Connector credentials/configuration/replay;
- Plugin lifecycle/permission/migration;
- financial/commercial acceptance/actions;
- production monitoring/DNS changes;
- sensitive exports/import merges;
- destructive archive/purge;
- Automation high-impact actions.

## Logging
Redact/exclude passwords, keys, auth/session tokens, private keys, Vault content, protected guest tokens and unnecessary sensitive webhook/provider payloads.

Use correlation IDs/structured safe metadata instead of dumping confidential content.

## Common web protections
Address XSS, CSRF where relevant, injection, IDOR, mass assignment, upload issues, path traversal, SSRF, unsafe URL fetch/redirect, brute force/rate abuse, replay and dependency vulnerabilities.

## Uploads
Validate type/size/content mismatch, authorization/destination, scan policy and processing state server-side. Secure guest uploads are destination-constrained.

## Destructive/high-impact operations
Require explicit capability, named target/consequence, contextual confirmation, Audit and archive/recovery where practical. Step-up/Approval when risk warrants.

## Security events / Attention / Notifications
Potential events:
- new/suspicious session;
- MFA/security change;
- privileged API/MCP credential;
- Connector auth expiry;
- repeated Vault access failure/reveal;
- privileged role/grant change;
- Secure External abuse/replay;
- Monitoring Worker anomaly;
- backup/security-control failure.

Persistent actionable conditions may create Security Attention; Notifications deliver awareness.

## Security settings
Settings > Security & Privacy:
- Authentication
- MFA / Step-up
- Sessions / Devices
- Password/SSO policy
- Roles/Permissions link
- API/MCP security
- Rate limits / abuse
- Security Events
- Secure External Access policy
- privacy/consent/data rights
- retention/holds
- export/purge/anonymization policy.

## Backup / recovery
Include documented backups, encryption where appropriate, restore testing, credential recovery/rotation, Audit preservation and disaster-recovery responsibilities.

## Acceptance criteria
- Principal/capability/scope authorization is server-side;
- negative cross-scope tests exist;
- hidden records cannot leak via secondary surfaces;
- Vault/File boundary is enforced;
- API/MCP/Connector/Plugin credentials are protected/revocable;
- provider events verified/idempotent;
- Secure External grants expire/revoke safely;
- Monitoring avoids SSRF/secret leakage and Probe identity is scoped;
- Àríyá cannot elevate caller access;
- sensitive actions produce append-only Audit;
- production rejects known insecure defaults;
- no HR/Timesheet/Client Service Consumption security model is introduced.

## Lovable build slices
1. Principal/capability/scope framework + negative tests.
2. session/security settings + step-up baseline.
3. append-only Audit coverage.
4. Vault/File/Secure External access policies.
5. API/MCP credential security.
6. Connector/Plugin/Action Registry security.
7. upload/download/monitor-target hardening.
8. Security Event/Attention/Notification center.
