# Collaboration and Following

## Purpose
Re:Solve needs one shared collaboration model for discussion around business records instead of each module inventing comments, mentions and internal notes independently.

## Core concepts

### Comment
A threaded or flat discussion item attached to a supported record.

### Internal Note
Visible only to authorized staff/internal users.

### Client-visible Comment/Update
Explicitly permitted to client users within the related record scope.

### Mention
A reference to an authorized user/team that may create a Notification and My Work/Mentions entry.

### Follow / Watch
A user intentionally subscribes to meaningful updates for a record.

### Reaction
Optional lightweight acknowledgement. Reactions should not replace decisions, approvals or audit evidence.

## Supported contexts
Shared collaboration may attach to:
- Organisation
- Contact
- Property
- Project
- Task
- Deliverable
- Request
- Approval
- Proposal/Estimate/Contract
- Invoice where appropriate
- Incident
- Knowledge suggestion/review
- other plugin-defined records

Vault secret content itself should not be copied into ordinary comments.

## Visibility
Every collaboration item has deliberate audience policy.

Examples:
- Staff only
- Project participants
- selected team
- client-visible
- selected organisation members

Client visibility must never be inferred merely from the parent record without explicit rules.

## Mentions
Mention resolution must validate that the mentioned principal can access the referenced context. Do not create a mention that reveals the existence/title of a hidden record.

## Following
Users may follow records manually or automatically because of ownership/assignment/participation.

Automatic following should be explainable and removable where policy permits.

Following feeds Notification recipient resolution but does not grant access.

## Activity
Comments and important collaboration events may appear in Activity timelines. Activity remains separate from immutable Audit.

## Editing/deletion
Comment editing/deletion policy should be transparent:
- show edited state when material
- retain moderation/audit evidence for sensitive workflows where required
- client-visible deletions should not silently rewrite approval/commercial history

## Attachments
Use the Files platform for ordinary attachments and Vault for protected confidential material.

## Portal
Portal collaboration should prioritize project/request/approval context. Internal notes must never surface through Portal, API, search or Àríyá.

## Notifications
Examples:
- mentioned
- reply to followed thread
- client comment
- staff response on a client-visible thread

Avoid notifying every follower for every minor activity unless policy calls for it.

## API/MCP/Àríyá
Àríyá may summarize authorized discussion and draft a reply. Sending/posting remains a controlled action.

## Acceptance criteria
- all modules reuse a shared collaboration contract
- following never grants authorization
- internal notes cannot leak to clients
- mentions validate target access
- ordinary comments do not become audit substitutes
- attachments respect Files/Vault boundaries
