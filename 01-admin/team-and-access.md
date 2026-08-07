# Admin — People, Principals and Access Administration

## Purpose
Give authorized administrators a complete, explainable view of who/what can access Re:Solve, which capabilities/scopes apply and why.

This is identity/access administration, **not HR**.

## Navigation
People & Access:
- Human Users / Staff Access
- Teams
- Roles
- Permissions
- Invitations
- Client Access
- Sessions / Devices
- API / MCP / Service Principals
- Access Reviews

## Principal model
Principal types:
- Human User;
- Service Account;
- API Client;
- MCP Client;
- Plugin;
- Connector.

A Human User may have staff access, client Memberships or both. One person should not need duplicate auth identities merely because they participate in multiple Organisations/contexts.

## Human User access workspace
Show access-oriented information:
- identity/profile reference;
- enabled/suspended state;
- staff access status;
- Teams;
- Roles;
- effective capabilities;
- Operating Entity scope;
- Organisation/Property/Project grants;
- temporary Grants;
- sessions/devices;
- recent relevant Security/Audit events;
- owned operational responsibilities requiring reassignment before deactivation.

Do not add employee number, payroll, leave, attendance, performance review, recruitment or Timesheet fields.

## Teams
Teams group Users for operational ownership, assignments, Notification targeting, Approvals, routing and access defaults.

Teams are not HR departments and are not automatically security boundaries unless configured.

Do not add utilization/workload/attendance analytics as a Team feature.

## Account Team distinction
Client Organisation `Account Team` assignments such as Account Owner/Technical Owner/Finance Owner are business-responsibility relationships and may reference Users/Teams.

They do not replace Teams/Roles and do not create HR reporting.

## Roles
Named canonical capability bundles. System templates may be protected; authorized admins can clone/customize roles.

Role editor shows:
- capabilities grouped by domain;
- high-risk capabilities;
- affected Principals/Users;
- inherited/direct behavior;
- diff/review before save.

## Permission grammar
Use `domain.action` or `domain.resource.action`.

Examples:
- `organisations.read`
- `properties.access.manage`
- `vault.secret.reveal`
- `billing.refunds.approve`
- `connectors.configure`
- `plugins.install`
- `mcp.clients.manage`

Do not create alternate naming grammar in this UI.

## Effective Access Inspector
For a Principal/User and optionally a target record, show:
- direct Roles;
- canonical capabilities;
- inherited/default Grants;
- Operating Entity/Organisation/Property scope;
- descendant inheritance;
- temporary Grants/expiry;
- source/grantor;
- explicit restrictions where supported;
- final allow/deny reason;
- step-up/Approval requirements that still apply.

Explainability is mandatory for authorization debugging.

## Invitations
Staff/client Invitations are separate workflows with expiry, resend, revoke, intended context/role/scope and duplicate-existing-User handling.

High-privilege staff Invitations may require Approval.

## Client Access
Administrators can inspect/assist with:
- Memberships;
- client role;
- Property scope;
- Portal state;
- billing/approver/designations;
- Vault authorization summary;
- Invitation state.

Client admins may manage their own permitted subset through Portal.

## Sessions / Devices
List active sessions with safe device/browser, approximate location when available/appropriate, created/last-active and revoke Actions. Sensitive security changes can invalidate sessions according to policy.

## Machine / extension Principals
API Clients, MCP Clients, Service Accounts, Plugins and Connectors must be visibly distinct from humans.

Show appropriate:
- owner/purpose;
- capabilities/scopes;
- credential expiry/last use;
- status;
- health where relevant;
- rotate/revoke/disable;
- Audit.

## Reassignment before deactivation
Before disabling a Human User, identify operational ownership requiring deliberate handover, such as:
- client Account Team responsibilities;
- Projects/Requests;
- pending Approvals;
- Renewal Obligations;
- Vault Item ownership/Approval responsibility;
- Connector/Automation stewardship;
- scheduled relationship reviews.

This is operational orphan prevention, not an HR offboarding system.

## Access Reviews
Periodic/reason-based reviews for:
- privileged Users;
- stale/suspended access;
- temporary Grants;
- Vault access;
- client Memberships;
- API/MCP credentials;
- Plugin/Connector permissions;
- unexpected broad access.

Outcomes may revoke/reassign/create Task/Attention with append-only Audit evidence.

## Attention / Notifications
Examples:
- privileged access review due;
- temporary Grant expiring with decision required;
- high-risk Role assigned;
- stale privileged credential;
- deactivation blocked by orphaned responsibility;
- suspicious session.

Notification delivers awareness; Attention persists until the source condition resolves.

## Security
Role/access changes are server-authorized, audited and may require confirmation/step-up/Approval.

Hidden Organisation/Property records must not appear in selectors/access previews to unauthorized administrators.

## API / MCP / Àríyá
Administration APIs are high privilege.

MCP defaults toward read-only access inspection. Access mutation requires narrow canonical capability, Action Registry and confirmation/Approval where applicable.

Àríyá may explain effective access/reassignment needs for authorized admins but cannot silently grant privilege.

## Responsive/PWA
Access inspection works on phone/tablet with drill-down cards/sheets rather than an impossible full-width matrix. Complex Role editing can optimize for larger screens while remaining readable on mobile.

## Product exclusions
People & Access must never drift into:
- HR employee records;
- payroll;
- recruitment;
- leave/attendance;
- employee reviews;
- Timesheets/Time Tracking;
- workload/utilization performance management.

## Acceptance criteria
- every acting identity is represented as a Principal;
- Human User is distinct from Contact;
- effective access is explainable;
- permission naming is canonical;
- deactivation identifies orphaned operational responsibilities;
- machine/plugin/connector Principals are distinguishable;
- client access is scope-aware;
- no HR/Timesheet/workforce-management feature is introduced.

## Lovable build slices
1. Human User/Team lists and access workspace.
2. Roles/capability editor.
3. Effective Access Inspector.
4. Invitations/Sessions/Client Access.
5. API/MCP/Service Principals.
6. Access Reviews/reassignment + mobile polish.
