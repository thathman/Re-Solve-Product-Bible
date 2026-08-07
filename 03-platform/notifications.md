# Notifications Platform

## Purpose
Notifications are a core Re:Solve platform primitive coordinating awareness across staff, clients, Properties, Projects, finance, support, security, connectors, plugins, automations and PWA channels.

A Notification is durable awareness/delivery that something happened. It is **not** the same as an Attention Item, which represents a condition that still requires action/awareness now.

## Goals
- surface the right event to the right User;
- distinguish information from action/urgency;
- support in-app, push, email, WhatsApp and future channels;
- avoid duplicate/noisy delivery;
- preserve useful history;
- deep-link to exact context;
- respect user preferences while preserving mandatory events;
- support digests;
- support client-safe language;
- expose API/MCP/Àríyá access under permissions;
- support plugin/connector event registration.

## Non-goals
Notifications do not replace:
- Attention;
- Chatwoot conversations;
- marketing campaigns;
- Audit;
- Activity/Comments;
- monitoring Incidents.

## Core concepts
### Notification Event
Business/system event eligible to create notifications.

### Notification Policy
Rules for User recipients, delivery destinations/channels, urgency, grouping, timing and mandatory behavior.

### Notification Record
Durable in-app/user-facing awareness instance.

### Delivery Destination
A verified/authorized endpoint such as an email address, phone/WhatsApp identity, push device or future channel target. A Contact without a Re:Solve User may receive an external operational message/delivery but is not an in-app Notification recipient.

### Delivery Attempt
Channel/provider-specific attempt/outcome.

### Preference
User delivery choices.

### Digest
Scheduled grouping of eligible notifications.

## Notification record fields
Conceptually:
- id;
- event type;
- category;
- priority;
- recipient User;
- surface: staff/client;
- Organisation/Property/Project context;
- related record;
- actor Principal;
- title/summary/body;
- primary action/deep link;
- created/seen/read/archive/snooze/expiry timestamps;
- mandatory flag;
- grouping/dedupe key;
- policy id/version;
- data sensitivity;
- source provenance when relevant.

## Priorities
Canonical:
- Informational
- Normal
- Important
- Urgent
- Critical

Features should not invent arbitrary visual scales.

## Categories
### Work
Task, mention, reminder, approval, action requested.

### Projects
Milestone, deliverable, Client Action, project risk/completion.

### Properties
Outage/recovery, degradation, maintenance, backup, domain/hosting/SSL renewal.

### Finance
Invoice, payment, reconciliation, credit/refund, recurring billing.

### Support
Meaningful Chatwoot-linked escalation/status/Incident only; never message-by-message mirror.

### Security & Vault
Access request/grant/revoke, reveal/download policy event, MFA/security, privileged API/MCP/Plugin/Connector changes.

### Platform
Connector/plugin/automation/job/probe/backup/update/system degradation.

### Requests / Commercial
Request assignment/outcome, proposal/contract acceptance/expiry/signature state where useful.

## Recipient resolution
In-app recipients are authenticated Users resolved through:
- explicit User;
- owner/assignee;
- Team;
- Role/capability;
- client Membership;
- Property grant;
- project approver;
- billing role;
- Vault admin/owner;
- escalation policy;
- follow/watch subscription.

Resolution occurs server-side and respects current access.

External operational delivery may target an authorized Contact/destination even when no User exists, but this is a Delivery Destination/Outbound Message relationship rather than an in-app recipient.

## Channels
### In-app
Durable default channel for authenticated Users where eligible.

### Push
PWA/browser push for time-sensitive awareness.

### Email
Formal asynchronous delivery and digests.

### WhatsApp/Baileys
Primarily Re:Solve-to-client operational delivery such as approvals, reminders, billing, renewal/property alerts and status updates.

### Future
Approved channel adapters via Connector/Plugin contracts.

## Channel eligibility
Every event defines eligible/default/mandatory channels via policy rather than hard-coded feature logic.

## Preferences
User preferences may include event group, channel, immediate/digest, quiet hours and push devices.

Mandatory security/compliance/system notices cannot be disabled when policy requires them.

## Quiet hours
Support configurable quiet hours with urgent/critical mandatory exceptions.

## Digests
Support hourly/daily/weekly where useful. Group by action required, overdue/urgent, Projects, Properties, Finance and informational changes.

Àríyá may summarize eligible digest content; underlying records remain deterministic.

## Grouping and deduplication
Use dedupe keys, grouping windows, transition awareness, replace/update behavior and Incident grouping to prevent storms.

Repeated monitor failures for one confirmed outage should not generate dozens of independent client notifications.

## Attention relationship
An event may create both an Attention Item and one/more Notifications.

Examples:
- Invoice becomes overdue -> Attention remains open until paid/resolved; Notification tells responsible Users/client.
- Domain renewal due -> Attention persists through workflow; reminders/notifications may repeat according to policy.
- Approval completed -> Approval Attention resolves; outcome Notification may remain in history.

Reading/archiving a Notification never automatically resolves the underlying Attention condition.

## Escalation
Policies may escalate unread/action-incomplete/deadline/Incident states by changing User recipient, channel or priority, or triggering an Automation.

## Admin Notification Center
Views:
- All
- Unread
- Mentions
- Approvals / Actions
- Finance
- Properties
- System
- Security

Controls include search/filter, read/unread, archive, snooze, bulk actions, deep links and preference shortcut.

## Portal Notification Center
Simplified:
- All
- Action Required
- Projects
- Properties
- Billing
- Security

Client wording avoids internal implementation/provider jargon.

## Global Notification Tray
Core UI provides a polished trigger/tray with unread count, grouping, priority restraint, context, primary action, read/archive/snooze where relevant and link to the full center.

## Deep links
Open the exact actionable context where possible. If access changed, show safe revoked/permission state without leaking title/details.

## Templates
Channel-specific templates support variables, client/staff variants, locale-ready structure, preview/testing and versioning for sensitive events. Complex business logic belongs outside templates.

## Delivery reliability
Delivery Attempt should record channel, provider/connector, destination reference, attempts, queue/send/provider acknowledgment, failure class, retry and final state.

Failures remain truthful. Durable in-app awareness stays where applicable; bounded retry/escalation follows policy.

## Offline/PWA
Support safe cached shell/history, push deep links, stale labeling, queued read/archive only when replay-safe and sync after reconnect. Sensitive bodies follow cache policy.

## Security/privacy
- no raw secrets in notification payloads;
- minimize sensitive push previews;
- client delivery is Organisation/Property scoped;
- destinations verified/authorized where policy requires;
- templates cannot exfiltrate arbitrary fields;
- revocation/access changes affect future delivery.

## Audit
Audit policy/template changes for sensitive events, manual resend, recipient override, destination changes and provider configuration. Ordinary read state does not require immutable Audit unless event policy says so.

## Automations
Automations call the Notification engine instead of implementing channels independently.

## Plugins/connectors
Plugins may register namespaced event types/policies/templates/deep links. Connectors may provide channels/events. Core owns recipient resolution, permission, dedupe, delivery logging and policy.

## API/MCP/Àríyá
Expose permitted list/read/read-state/archive/snooze/preferences/admin diagnostics operations. Agents cannot bypass policy to send arbitrary confidential external messages.

Àríyá may summarize Notifications and Attention but does not own deterministic priority/delivery.

## Analytics
Measure volume, action completion, read time, channel delivery success/failure, opt-out/preferences, digest usefulness and noisy-event patterns to reduce noise rather than gamify engagement.

## Acceptance criteria
- in-app recipients are Users, not arbitrary Contact records;
- external Contact destinations are modeled as delivery/communication targets;
- Attention and Notification lifecycles remain distinct;
- cross-scope leakage tests fail safely;
- mandatory policy and preferences behave correctly;
- dedupe prevents storms;
- failed external delivery is visible/retryable;
- global tray and full center are strong Core UI experiences;
- client wording is safe;
- plugins/connectors cannot bypass policy;
- API/MCP/Àríyá respect scope.
