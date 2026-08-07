# Client Portal — Organisation and Account

## Purpose
Let authorised client users manage their own organisation context, team access and personal account without exposing Re:Solve staff controls.

## Organisation
Sections:
- Profile
- Team
- Invitations
- Roles & Access
- Billing Contacts
- Project Approvers
- Property Access
- Audit Summary

Organisation Owners may edit approved organisation profile fields, invite users, revoke users, assign client roles, assign property access and designate billing/project/vault responsibilities. Actions are permission-gated and auditable.

## Invitations
Invitation lifecycle: drafted, sent, accepted, expired, revoked. Support resend, expiry and cancellation. Duplicate invitations and existing memberships are detected.

## Client roles
Suggested default roles are templates over permissions rather than hard-coded behavior: Organisation Owner, Organisation Admin, Billing Contact, Project Approver, Property User, Viewer. Deployments may customize permitted combinations.

## Access matrix
Organisation admins should be able to answer: who can see this property, who can approve work, who receives invoices, and who may access shared Vault items. Sensitive capabilities display warnings and require explicit assignment.

## Personal Account
Sections:
- Profile
- Sign-in & Security
- MFA / Passkeys where supported
- Active Sessions
- Devices
- Notification Preferences
- Appearance / Accessibility preferences
- Connected identity methods

A user may belong to multiple organisations; account identity is not duplicated per organisation. Organisation context switching must be explicit and preserve isolation.

## Notifications
Invitation, access grant/removal, role change, security changes, new session/device and sensitive permission changes generate appropriate notifications. Certain security notices are mandatory.

## API / MCP
Organisation-management APIs require client-admin scopes. MCP may offer read-only membership tools by default. Access changes are high-risk write operations and require strong authorization/audit.

## PWA/mobile
Team/access management remains usable on mobile using cards/drawers instead of wide matrices when necessary. Security flows must work reliably in standalone PWA mode.

## Lovable build slices
1. Organisation profile/team list.
2. Invitations.
3. Roles/property access/designations.
4. Personal account/security.
5. Notification/access audit polish and responsive states.