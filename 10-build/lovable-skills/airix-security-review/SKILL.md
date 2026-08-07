---
name: airix-security-review
description: Review Re:Solve authentication, permissions, sensitive data, integrations, billing, and destructive workflows for access-control and exposure risks.
---

# Airix Security Review

Review the affected user flow end to end.

Check:
- authentication assumptions
- capability-based authorization
- organisation and property isolation
- client/admin boundaries
- server-side enforcement
- sensitive-field redaction
- Secure Vault reveal/download/share rules
- step-up authentication requirements
- audit events
- secrets handling
- rate limits where relevant
- webhook verification and duplicate-event protection
- connector credential exposure
- plugin permission boundaries
- API and MCP scopes
- AI tool permissions
- offline/PWA exposure
- destructive-action confirmation and recovery

Do not rely on hidden UI as authorization.

Report concrete findings and recommended fixes. If no issue is found, state which negative paths were checked.
