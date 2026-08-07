---
name: resolve-notifications
description: Use when implementing or reviewing Re:Solve notification events, recipient rules, in-app notification experiences, delivery channels, digests, escalation, grouping, preferences, or notification-related PWA behavior.
---

# Re:Solve Notifications

Read `03-platform/notifications.md`, Attention Engine, Operational Communications, Core UI Framework, PWA, permissions and the source domain spec.

## Core distinction
Notification = durable recipient-specific awareness/delivery that something happened.
Attention Item = a current unresolved condition requiring action or awareness.
Activity = durable business chronology.
Audit = evidentiary security/operational history.
Do not collapse these concepts.

## Event design
For each notification define:
- event id/type and source domain;
- category and priority;
- intended recipient User(s) or recipient-resolution rule;
- organisation/property/record context;
- title/body safe for that channel;
- primary action/deep link;
- grouping/deduplication key;
- expiry/resolve behavior;
- mandatory vs configurable delivery;
- delivery channels and fallback/escalation policy.

Non-user Contacts may be external delivery destinations for email/WhatsApp but are not automatically in-app notification recipients.

## Channels
Support in-app first, then configured push/email/WhatsApp/future connectors. Respect channel suitability and privacy. Never place Vault secrets, private document bodies, auth tokens or unnecessary sensitive information in notification previews.

## UI
Use canonical `NotificationTrigger`, `NotificationTray`, `NotificationItem` and full Notification Center patterns. Make unread/priority visible without visual shouting. Support relevant read/unread, archive, snooze, grouping, filters, bulk actions and preference shortcuts.

## Preferences
User preferences may configure event/channel/digest behavior except policy-mandatory security/system events. Prefer event families rather than hundreds of incomprehensible toggles.

## Reliability
Delivery state must be observable and retryable where appropriate. Avoid duplicate delivery from repeated provider/webhook events through idempotency and dedupe.

## PWA
Push deep-links to exact authorized records after auth. Lock-screen copy is privacy-conscious. Offline/stale tray state is explicit.

## Completion
Verify one event does not produce spam, inaccessible records do not leak through notification bodies or counts, mandatory events cannot be accidentally disabled, and Attention creation/resolution is deliberate rather than inferred from notification unread state.