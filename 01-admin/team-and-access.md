# Admin — Team & Access Administration

## Purpose
Give authorized administrators a complete view of who can access Re:Solve, what they can do, which organisations/properties they can reach, and why.

## Navigation
Team & Access
- Staff
- Teams
- Roles
- Permissions
- Invitations
- Client Access
- Sessions
- API/MCP Identities
- Access Review

## Identity model
A person/account may have staff access, client memberships or both. Access is composed from roles, explicit grants, organisation scope, property scope, team membership and temporary grants.

## Staff
Staff record shows identity, status, teams, roles, effective permissions, assigned clients/properties, recent security events, sessions and activity. Deactivation revokes active access according to policy while preserving historical attribution.

## Teams
Teams group staff for responsibility, notifications, approvals, routing and workload. Teams are not automatically security boundaries unless explicitly configured.

## Roles
Roles are named permission bundles. System roles may be protected; custom roles may be created. Role editing shows permission implications and affected users before saving.

## Permissions
Capability-based naming such as clients.read, properties.manage, vault.reveal, billing.refund, connectors.configure, plugins.install. Permissions may also require scope constraints.

## Effective access inspector
For any user, administrators can inspect:
- direct roles
- inherited permissions
- explicit grants/denials
- organisation access
- property access
- temporary access
- why a specific permission is allowed/denied

This explainability is mandatory for debugging authorization.

## Access reviews
Support periodic review of privileged accounts, Vault access, API/MCP credentials, stale users and temporary grants. Reviews can produce revocations/tasks and auditable acknowledgements.

## Invitations
Staff invitations support expiry, resend, cancellation and intended role/team. High-privilege roles may require second approval.

## Sessions/devices
List active sessions with device/browser, approximate location where available, created/last-active time and revoke action. Security policies can revoke all sessions on sensitive changes.

## API/MCP identities
Service accounts and AI clients are visible alongside human identities but clearly distinguished. Show scopes, last used, expiry, owner and revoke/rotate actions.

## Notifications
Privileged role assigned, role changed, account disabled, suspicious session, new API/MCP credential, access review due and sensitive access granted/revoked.

## API / MCP
Administration APIs are high privilege. MCP should default to read-only access inspection; permission mutation requires explicit admin scope and confirmation.

## Lovable build slices
1. Staff/team lists and staff workspace.
2. Roles/permission editor.
3. Effective access inspector.
4. Invitations/sessions/API identities.
5. Access review workflows and mobile polish.