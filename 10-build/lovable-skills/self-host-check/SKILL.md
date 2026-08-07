---
name: self-host-check
description: Review a Re:Solve change for portability risks, unnecessary Lovable-only runtime assumptions, provider lock-in, and hard-to-replace infrastructure coupling.
---

# Self Host Check

This is an architecture review, not a request to build production infrastructure early.

Check whether the change introduces:
- a Lovable-only runtime dependency for product-critical behavior
- provider-specific APIs scattered through domain/UI code
- direct data-provider calls that should be centralized
- auth assumptions that make provider replacement difficult
- storage URLs used as permanent business identifiers
- proprietary realtime behavior as the only source of truth
- non-exportable UI/configuration
- cloud-specific runtime APIs without a boundary
- secrets embedded in client code or source
- plugin/connector behavior that cannot exist outside Lovable

Confirm where practical:
- source is exportable
- environment configuration is explicit
- business records remain Re:Solve concepts
- providers are behind reasonable boundaries
- migrations/schema changes are reproducible
- PWA behavior is source-controlled
- API/MCP behavior uses portable application services

Do not require Docker, reverse proxies, Kubernetes, or production hosting work unless the current slice is specifically about deployment.

Report:
- portability risks
- severity
- whether action is needed now or can be deferred
- recommended boundary/refactor if needed
