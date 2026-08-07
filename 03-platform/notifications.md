# Notifications Platform

## 1. Purpose

Notifications are a core Re:Solve platform primitive. They coordinate attention across staff, clients, properties, projects, finance, support, security, connectors, plugins, automations, and the PWA.

A notification is not merely a bell item. It is a durable attention record with policy, delivery, deep-link, preference, and audit behavior.

## 2. Goals

The system must:

- surface the right event to the right person;
- distinguish informational updates from urgent action;
- support in-app, push, email, WhatsApp, and future channels;
- avoid duplicate/noisy delivery;
- preserve a searchable notification history where appropriate;
- deep-link directly to the relevant action/state;
- support individual preferences without allowing critical security notices to be disabled;
- support digests;
- support client-safe language;
- expose API and MCP access;
- support plugins and connectors registering new event types;
- work consistently in Admin and Portal.

## 3. Non-goals

Notifications do not replace:

- Chatwoot conversations;
- email marketing;
- system audit logs;
- activity timelines;
- project comments;
- monitoring incident records.

A notification may reference these records but should not duplicate their full content.

## 4. Core concepts

### Notification Event
The business/system event that can produce attention.

### Notification Policy
Rules determining recipients, urgency, channels, grouping, timing, and mutability.

### Notification Record
The durable user-facing notification instance.

### Delivery Attempt
A channel-specific delivery attempt and its outcome.

### Preference
A user's configurable delivery choices.

### Digest
A scheduled summary of multiple eligible notifications.

## 5. Notification record fields

Conceptually include:

- id;
- event type;
- category;
- priority;
- recipient user/contact;
- recipient surface (staff/client);
- organisation context;
- property context;
- project context;
- related record type/id;
- actor;
- title;
- short summary;
- optional body;
- primary action label;
- deep link;
- secondary action where justified;
- created at;
- seen at;
- read at;
- archived at;
- snoozed until;
- expires at;
- mandatory flag;
- grouping key;
- deduplication key;
- delivery policy id/version;
- data sensitivity classification.

## 6. Priorities

Canonical priority levels:

### Informational
No action expected. Useful history/status only.

### Normal
Relevant update; may merit attention.

### Important
Action or awareness expected soon.

### Urgent
Time-sensitive action or degradation.

### Critical
Immediate attention required; may invoke mandatory multi-channel delivery.

Features must not invent arbitrary visual priority scales.

## 7. Categories

Initial categories:

### Work
- task assigned;
- mention;
- reminder;
- action requested;
- approval assigned;
- approval outcome.

### Projects
- project created/started;
- milestone approaching/overdue;
- deliverable ready;
- deliverable approved/rejected/requested changes;
- client action due;
- risk raised;
- project completed.

### Properties
- outage;
- degraded state;
- recovery;
- SSL/domain/hosting renewal;
- maintenance;
- backup failure;
- health check stale.

### Finance
- invoice issued;
- invoice due;
- invoice overdue;
- payment received;
- payment failed;
- payment reconciled;
- credit note;
- refund;
- subscription renewal/change.

### Support
- important support escalation mirrored from Chatwoot where policy allows;
- SLA risk;
- linked incident;
- support resolution requiring client/staff awareness.

Re:Solve must not mirror every Chatwoot message into its notification center by default.

### Security & Vault
- credential access requested;
- access granted/denied;
- secret revealed;
- confidential file shared;
- access revoked;
- MFA/security change;
- suspicious login;
- API/MCP token created/revoked;
- privileged plugin/connector change.

### Platform
- connector disconnected;
- connector authentication expiring;
- webhook processing failure;
- plugin failure/update;
- automation failure;
- background job failure;
- backup issue;
- system update available;
- service health degradation.

## 8. Recipient resolution

Recipients may be determined by:

- explicit user;
- record owner;
- assigned staff;
- role/capability;
- client organisation role;
- property grant;
- billing contact;
- project approver;
- vault administrator;
- team;
- escalation policy;
- subscription/following relationship.

Recipient resolution must occur server-side and respect current permissions.

## 9. Channels

### In-app
Default durable channel for eligible events.

### Push
PWA/browser push for time-sensitive attention.

### Email
Formal, asynchronous delivery for important events and summaries.

### WhatsApp/Baileys
Primarily operational communication between Re:Solve operator and clients. Use for permitted client notifications, reminders, ticket/status updates, and selected staff alerts where configured.

### Future channels
Plugins/connectors may register additional channels through a controlled contract.

## 10. Channel matrix concept

Every event specification must define channel eligibility, not hard-coded delivery.

Example policy:

| Event | In-app | Push | Email | WhatsApp | Mandatory |
|---|---|---|---|---|---|
| Mention | yes | optional | optional | no | no |
| Client approval due | yes | optional | yes | optional | no |
| Invoice issued | yes | optional | yes | optional | no |
| Production outage | yes | yes | yes | optional | policy-based |
| MFA disabled | yes | yes | yes | no | yes |

## 11. Preferences

Users may configure notification preferences by:

- event group;
- channel;
- immediate vs digest;
- quiet hours;
- push device;
- WhatsApp eligibility where applicable.

Preferences must distinguish:

- optional notifications;
- recommended notifications;
- mandatory notifications.

Mandatory security and compliance notices cannot be disabled.

## 12. Quiet hours

Support configurable quiet hours with exceptions for urgent/critical mandatory events.

Client and staff defaults may differ.

## 13. Digests

Support:

- hourly digest where useful;
- daily digest;
- weekly recap.

Digest eligibility is event-specific.

Digest content should group by:

- actions required;
- overdue/urgent;
- projects;
- properties;
- finance;
- informational changes.

Re:Solve AI may summarize eligible digest content, but the underlying records remain deterministic and auditable.

## 14. Grouping and deduplication

Prevent notification storms using:

- event deduplication keys;
- grouping windows;
- state transition awareness;
- replace/update behavior for ongoing conditions;
- incident grouping.

Example: repeated monitor failures for one outage should not create dozens of separate client notifications.

## 15. Escalation

Policies may escalate when:

- unread after threshold;
- action not completed;
- deadline approaches;
- incident remains unresolved;
- first delivery channel fails;
- priority increases.

Escalation can change:

- recipient;
- priority;
- channel;
- message wording;
- automation action.

## 16. Notification center — Admin

The Admin notification center should include:

- All;
- Unread;
- Mentions;
- Approvals/Actions;
- Finance;
- Properties;
- System;
- Security.

Controls:

- search;
- filter by priority;
- filter by client/property/project;
- mark read/unread;
- archive;
- snooze;
- bulk mark read;
- bulk archive;
- open related record;
- notification preference shortcut.

## 17. Notification center — Portal

Client categories should be simplified:

- All;
- Action required;
- Projects;
- Properties;
- Billing;
- Security.

Client wording must be understandable without internal implementation terms.

## 18. Notification item design

Each item should show as applicable:

- semantic icon/status;
- title;
- concise context;
- organisation/property/project label;
- relative time;
- unread state;
- priority;
- primary action;
- grouping count;
- delivery/degraded indicator only when useful.

Do not make every notification visually loud.

## 19. Deep links

A notification deep link should open the exact actionable context where possible, for example:

- approval drawer for a deliverable;
- invoice payment view;
- property incident;
- vault access request;
- project task;
- connector failure detail.

If access changed since creation, show a safe permission-denied/revoked state rather than leaking data.

## 20. Templates

Notification templates should support:

- in-app title/body;
- push title/body;
- email subject/body;
- WhatsApp message;
- variables;
- client-safe variant;
- staff variant;
- locale-ready structure;
- preview/testing;
- versioning for audit-sensitive templates.

Avoid embedding complex business logic inside templates.

## 21. Settings

Workspace settings must expose:

- enabled channels;
- channel providers/connectors;
- defaults by audience;
- event policy defaults;
- priority defaults;
- digest schedules;
- quiet-hour defaults;
- template management;
- mandatory-event rules;
- retry/failure policy;
- retention;
- testing tools.

User preferences live separately from workspace policy.

## 22. Delivery reliability

Each delivery attempt should record:

- notification id;
- channel;
- provider/connector;
- destination reference;
- attempt number;
- queued time;
- sent time;
- provider acknowledgement;
- failure category;
- retry time;
- final state.

Retries must be bounded and observable.

## 23. Failure behavior

If external delivery fails:

- durable in-app notification remains where applicable;
- retry follows policy;
- repeated systemic failures create a platform alert;
- user-facing record should not falsely claim delivery;
- critical delivery failure may escalate to another channel.

## 24. Offline/PWA behavior

The notification center must support:

- cached notification shell/history where safe;
- push opening into installed PWA;
- offline deep-link fallback;
- queued read/archive actions if safely replayable;
- stale indicator when latest data cannot be fetched;
- sync after reconnection.

Sensitive notification bodies should respect cache policy.

## 25. Security and privacy

- never include raw secrets in notification payloads;
- minimize sensitive information in push previews;
- client notifications must be organisation/property scoped;
- email/WhatsApp destinations must be verified/authorized where policy requires;
- notification templates must not enable data exfiltration through arbitrary variables;
- access changes should invalidate future delivery where appropriate.

## 26. Audit

Audit at minimum:

- policy changes;
- template changes for security/financial events;
- mandatory notification suppression attempts;
- manual resend;
- recipient override;
- WhatsApp destination change;
- provider configuration changes.

Reading ordinary notifications does not need immutable security audit unless the notification itself is sensitive.

## 27. Automation integration

Notifications may be:

- triggered by domain event;
- sent by automation action;
- used as escalation outcome;
- acknowledged by automation condition.

Automations should call the notification engine rather than implementing channel delivery independently.

## 28. Plugin integration

Plugins may register:

- event types;
- categories under approved namespaces;
- default policies;
- templates;
- deep-link handlers;
- optional channel adapters.

Plugin events must still use core recipient resolution, permissions, dedupe, delivery logging, and audit contracts.

## 29. Connector integration

Connectors may provide channels or events. Examples:

- WhatsApp connector provides delivery channel;
- monitoring connector generates property events;
- payment connector generates payment events;
- Chatwoot connector may generate only selected escalation/status events rather than message-by-message noise.

## 30. API

Expose versioned APIs for permitted operations such as:

- list notifications;
- get notification;
- mark read/unread;
- archive;
- snooze;
- get unread count;
- get/update personal preferences;
- admin preview/test template;
- admin policy management;
- delivery diagnostics with appropriate permissions.

## 31. MCP

Read-oriented MCP tools may include:

- `list_notifications`;
- `get_unread_notifications`;
- `get_attention_summary`;
- `get_notification_preferences`.

Controlled write tools may include:

- `mark_notification_read`;
- `snooze_notification`;
- `create_notification` for authorized automation/agent use.

Agents must not bypass event policy to send arbitrary confidential content through external channels.

## 32. Analytics

Measure:

- notification volume by type/channel;
- read time;
- action completion after notification;
- delivery success/failure;
- opt-out/preference rates;
- digest engagement;
- excessive/noisy event detection;
- repeated snoozing/ignoring of event categories.

Analytics must help reduce noise rather than gamify engagement.

## 33. Retention

Define retention by category and sensitivity. Security/financial notification records may have different requirements from ordinary work notifications.

## 34. Acceptance criteria

The platform is acceptable when:

- events resolve correct recipients;
- cross-organisation/property leakage tests fail safely;
- channel preferences are respected;
- mandatory notices cannot be disabled;
- dedupe prevents event storms;
- failed external delivery is visible and retried;
- notification items deep-link correctly;
- mobile/PWA push opens the correct context;
- client wording is safe and understandable;
- plugins/connectors cannot bypass core policy;
- API/MCP access respects scopes and permissions.

## 35. Lovable build slices

### Slice A — in-app model + Admin center
No external channels. Build durable notifications, unread/read/archive, filters, deep links, and realistic demo events.

### Slice B — Portal center
Client-safe categories, wording, permissions, mobile behavior.

### Slice C — preferences
Personal channel/event preferences, mandatory rules, quiet hours.

### Slice D — PWA push
Push permission flow, device registration, notification click/deep-link behavior.

### Slice E — email delivery
Template + delivery attempt model + failure/retry visibility.

### Slice F — WhatsApp delivery
Connector-backed client operational messages with explicit eligibility and diagnostics.

### Slice G — digests and escalation
Digest schedules, grouping, escalation rules, AI-assisted summary presentation where approved.
