# Client Portal — Organisation and Account

## Purpose
Let authorized client Users manage permitted Organisation profile, Membership/access, communication/privacy preferences and personal account/security without exposing staff/platform administration.

## Portal activation rule
A business Contact does **not** automatically receive a Portal account because they exist as a Lead, Contact, Organisation member or Opportunity participant.

Default lifecycle:
1. prospect/Contact interacts through public or Secure External Access;
2. Discovery/Form Request and Proposal may be completed without Portal Membership;
3. Proposal acceptance/commercial commitment triggers the default Portal Invitation workflow;
4. Contact accepts invitation into their existing/new Human User identity;
5. Membership becomes active for the exact Organisation/scope.

Staff may manually invite earlier where a legitimate workflow requires it.

Conceptual Membership states: `none -> invited -> active -> suspended -> revoked`.

Suspended/revoked Membership grants no Portal data access.

## Invitations
Lifecycle includes Created/Draft, Sent, Accepted, Expired and Revoked. Support resend, expiry, cancellation and duplicate/existing-User detection.

Invitation accepts into one Human User identity; do not create a duplicate auth identity per Organisation.

The Proposal-acceptance trigger must be idempotent and must not send duplicate active Invitations on retry.

## Organisation Profile
Editable fields are policy controlled and may include approved legal/display/business/contact/address/billing/custom fields. Operating Entity/Brand identity is staff-owned and not client-editable.

## Team & Access
Authorized Organisation Owner/Admin can understand:
- who has Portal access;
- role template/capabilities;
- Property scope;
- Project/Approver/Billing designations;
- Vault authorization summary;
- Membership state/last sign-in where policy permits;
- pending Invitations;
- temporary/expiring Grants.

The UI should answer plainly: Who can see this Property? Who can approve? Who receives Billing? Who can invite others? Who has protected Vault access?

## Client roles/designations
Default templates may include Organisation Owner, Organisation Admin, Billing Contact, Project Collaborator, Approver, Property Manager, Vault User and Read-only Member.

Designations such as Billing Contact, Project Approver, Technical/Property Contact and escalation Contact are relationship/access responsibilities, not HR roles.

## Property/record access
Client admins with authority can grant/revoke permitted Property/record access according to policy. Hidden records/children never leak through selectors/counts. Property access does not imply Vault access.

## Communication preferences
Where allowed, manage Organisation operational destinations such as billing, renewals, maintenance/incident, support/escalation and approved email/WhatsApp. Individual preferences and mandatory security/billing/service rules still apply. Marketing consent is separate.

## Personal Account
Reached from global Account/Avatar rather than heavy root navigation:
- Profile;
- Sign-in & Security;
- MFA/passkeys where supported;
- Sessions/Devices;
- Notification Preferences;
- Communication Preferences;
- Appearance/Accessibility;
- connected identity methods;
- Privacy/Data Requests.

A User can belong to multiple Organisations with explicit isolated context switching.

## Portal live chat / Ariya
Portal Ariya is strictly bound to active Membership + current Organisation/record scope. Canonical live-chat path is:
`Portal -> Ariya -> Chatwoot -> Ariya -> Client`.

Ariya may explain the User's permitted access, Projects, Billing or Property Health; help locate settings; create Support work; and hand off to Chatwoot. It cannot reveal hidden memberships/records or make privileged access changes without registered Action/confirmation.

## Preview as Client
Authorized staff need a read-only `Preview as Client` capability for a specific Organisation/User/scope to verify what the Portal actually exposes.

Preview:
- uses real authorization/visibility evaluation;
- clearly indicates preview mode;
- cannot perform client mutations/signatures/payments/approvals merely because the staff user is previewing;
- is audited where sensitivity justifies it.

## Security
Sensitive role/Property/Vault access changes, ownership transfer or own MFA/security changes may require recent reauthentication/step-up. Access mutation is server-authorized and audited.

## Attention / Notifications
Meaningful events include Invitation sent/expiring/accepted/revoked, role/Property access changed, ownership/admin change, Vault access, new session/device, security change and data-right request update.

## Responsive/accessibility
Membership/access/invitation flows use clear lists/cards/drill-downs on phone rather than impossible permission matrices. Permission meaning is textual, not color/icon-only.

## Acceptance criteria
- Lead/Contact/Opportunity does not automatically create Portal account;
- Proposal acceptance is the default idempotent invite trigger;
- secure guest flows work before Membership;
- one Human User identity can belong to multiple Organisations;
- suspended/revoked Membership grants no data authority;
- client admins understand effective access;
- hidden records do not leak;
- Property access does not imply Vault access;
- Preview as Client is accurate and read-only;
- Ariya/Chatwoot live chat stays client-scoped;
- access/security changes are server-authorized/audited;
- no HR capability appears.

## Build slices
1. Invitation/activation lifecycle + Proposal-acceptance trigger.
2. Organisation profile + Team/access list.
3. client roles/designations/Property scope.
4. personal Account/security/preferences.
5. Preview as Client.
6. Ariya/Chatwoot Portal integration + mobile polish.
