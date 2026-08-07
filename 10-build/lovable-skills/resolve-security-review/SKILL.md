---
name: resolve-security-review
description: Use before completing any Re:Solve slice that touches authentication, permissions, Vault, finance, external access, connectors/plugins, API/MCP, Àríyá, sensitive data, destructive actions, or cross-organisation/property scope.
---

# Re:Solve Security Review

Check:
- Principal/caller identity;
- capability + scope authorization;
- cross-Organisation and cross-Property denial;
- server-side enforcement beyond navigation hiding;
- Action Registry risk/confirmation/approval/step-up;
- Vault/File access-path separation;
- sensitive field/search/log/cache exposure;
- Audit events;
- connector credentials and sync authority;
- webhook verification/replay/idempotency;
- API/MCP rate/scope controls;
- Àríyá permission inheritance/evidence/action policy;
- offline/PWA cache safety;
- Secure External Access expiry/revocation;
- negative tests and failure states.

Report concrete findings and the negative paths actually checked. Do not weaken authorization to make the happy path easier.
