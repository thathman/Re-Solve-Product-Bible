# Client Portal — Organisation and Account

## Purpose
Let authorized client Users manage permitted Organisation profile, memberships/access, communication/privacy preferences and personal account/security without exposing staff/platform administration.

## Navigation
Keep Portal navigation simple. `Organisation` may contain:
- Profile
- Team & Access
- Invitations
- Billing / Approver designations
- Communication Preferences

Personal `Account` is reached through the global Avatar/AccountMenu rather than adding another heavy root destination.

## Organisation Profile
Editable fields are deployment/policy controlled and may include approved:
- display/legal name;
- business/contact information;
- address;
- billing/profile details;
- public/client metadata;
- custom fields explicitly client-editable.

Operating Entity/Brand identity is staff configuration and not client-editable.

## Team & Access
Authorized Organisation Owner/Admin can understand:
- who has Portal access;
- role template;
- Property scope;
- Project/Approver/Billing designations;
- Vault authorization summary;
- status/last sign-in where policy permits;
- pending Invitations;
- access expiry/temporary grants where relevant.

The client access UI should answer common questions plainly:
- Who can see this Property?
- Who can approve this work?
- Who receives Billing?
- Who can manage other client users?
- Who has protected Vault access?

Do not expose internal staff Roles or platform permissions irrelevant to client administration.

## Invitations
Lifecycle:
- Draft/created
- Sent
- Accepted
- Expired
- Revoked

Support resend, expiry, cancellation and duplicate/existing Membership detection.

Invitation accepts into one human User identity; do not create duplicate user identities for each Organisation.

## Client Roles
Default role templates may include:
- Organisation Owner
- Organisation Admin
- Billing Contact
- Project Collaborator
- Approver
- Property Manager
- Vault User
- Read-only Member

Roles are bundles over canonical client-safe capabilities. Actual access also depends on Property/record scope.

## Property Access
Client admins with authority can grant/revoke permitted Property access, including descendant behavior where allowed by policy.

Hidden Properties/children cannot leak through selectors/counts.

High-sensitivity capabilities such as Vault access require explicit assignment and clear warnings; ordinary Property access does not imply Vault access.

## Designations
A client Contact/User may be designated for operational responsibility such as:
- Billing Contact;
- Project Approver;
- Technical/Property Contact;
- escalation Contact.

These are relationship/access responsibilities, not HR roles.

## Organisation communication preferences
Where client admins are allowed, manage Organisation-level operational communication defaults such as:
- billing destinations;
- renewal notices;
- maintenance/incident contacts;
- support/escalation contacts;
- approved WhatsApp/email destinations.

Individual User preferences and mandatory security/billing rules still apply.

Marketing/newsletter consent remains separate from required service/operational communication.

## Personal Account
Global AccountMenu leads to:
- Profile
- Sign-in & Security
- MFA / supported stronger auth
- Active Sessions / Devices
- Notification Preferences
- Communication Preferences
- Appearance / Accessibility
- connected identity methods
- Privacy / Data Requests where available

A User can belong to multiple Organisations without duplicating account identity. Organisation context switch is explicit and isolated.

## Notification Preferences
Allow per-user optional event/channel/digest/quiet-hour preferences while clearly marking mandatory security/system/client-admin notices that cannot be disabled.

## Privacy / data rights
Where enabled, Account can support:
- review/update personal profile data;
- communication preferences/consent;
- request data access/export;
- request correction;
- request deletion/anonymization review where applicable.

These become verified Privacy workflows, not instant destructive actions.

## Security
Sensitive operations such as role/property/Vault access change, Organisation ownership transfer or own MFA/security changes may require recent reauthentication/step-up.

Access mutation is server-authorized and append-only audited.

## Attention / Notifications
Meaningful events:
- Invitation sent/expiring/accepted/revoked;
- role/property access changed;
- ownership/client-admin change;
- Vault access granted/revoked;
- new session/device;
- MFA/security change;
- data-right request update.

An access/security condition requiring action may also create Attention.

## Àríyá
Portal Àríyá may explain the current User's permitted access or help locate settings, but cannot reveal hidden memberships/Properties or make privileged access changes without registered Action/confirmation.

## API / MCP
Organisation-management APIs require appropriate client-admin capability and current scope.

MCP/client-agent access should default read-only for memberships/access; privileged mutation requires explicit high-trust capability/Action and Audit.

## PWA/mobile
Team/access/invitations use clear lists/cards/drawers rather than forcing a wide permission matrix onto phone. Security/MFA/session flows must work in installed PWA mode.

## Accessibility / Core UI
Use canonical ResolveAvatar/AccountMenu, form, role/status, dialog/sheet and permission components. Permission meaning must be textual, not dependent on icon/color alone.

## Acceptance criteria
- client User identity is not duplicated per Organisation;
- client admins understand effective access;
- Property access does not imply Vault access;
- hidden Properties never leak through administration UI;
- security/access changes are server-authorized and audited;
- individual versus Organisation communication preferences are clear;
- Privacy requests are controlled workflows;
- mobile access administration is genuinely usable;
- no HR/employee-management capability appears.

## Lovable build slices
1. Organisation profile + Team list.
2. Invitations.
3. role/designation/Property access.
4. personal Account/security/sessions.
5. Notification/communication/privacy preferences.
6. access Audit/step-up/mobile polish.
