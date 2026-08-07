# Client Portal — Support

## Purpose
Give clients a coherent support entry point while keeping Chatwoot as the actual support/helpdesk system.

## Re:Solve responsibilities
- show support entitlement and channels
- show selected recent/open conversation references
- show property/service context
- show known incidents and service notices
- launch or deep-link into Chatwoot
- preserve account-level support metadata and analytics

## Chatwoot responsibilities
- conversations/messages
- attachments
- web chat
- agent/team assignment
- routing
- support KB
- Captain AI
- conversation states and CSAT

## Portal surface
Sections:
- Support Overview
- Start / Continue Conversation
- Recent Conversations
- Known Incidents
- Support Plan / Entitlement
- Service Status

The global Chatwoot widget remains available where configured. Portal summaries must never pretend to be the full conversation console.

## Context handoff
When launching support, Re:Solve may pass safe context such as organisation, property, property type, source page, authenticated role and support entitlement. Never send secrets, Vault data or unnecessary PII.

## Conversation list
Where API access permits, show subject/preview, property, status, last update and unread state. Opening may either render a safe portal conversation view or deep-link into the Chatwoot experience depending on integration design.

## Incidents
Known Re:Solve incidents may be surfaced independently of Chatwoot to reduce duplicate support contacts. Incident details are client-safe and may link to impacted properties.

## Notifications
Support escalations, staff replies requiring action, incident updates and resolution notices may create Re:Solve notifications. Do not mirror every Chatwoot message into Re:Solve notifications.

## API / MCP
Expose support summaries and permitted conversation references, not unrestricted Chatwoot internals. Example tools: get_my_support_status, list_my_support_conversations, get_known_incidents.

## PWA/mobile
Support must be excellent on mobile. The widget/launch experience must respect standalone PWA mode, safe areas, keyboard behavior and interrupted sessions.

## Lovable build slices
1. Support overview with demo conversation references.
2. Chatwoot launch/context contract.
3. Recent conversations summary.
4. Incidents/entitlement/service status.
5. Mobile/PWA behavior and failure states.