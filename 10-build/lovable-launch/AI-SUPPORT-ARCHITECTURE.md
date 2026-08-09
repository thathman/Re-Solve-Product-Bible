# Re:Solve AI + Support Architecture

## Canonical product boundary

Re:Solve has two distinct AI concerns. They must not be merged, renamed into one another, or treated as interchangeable.

### Àríyá — Re:Solve product AI
- Àríyá is Re:Solve's own AI product and identity.
- Àríyá powers Re:Solve product assistance across client-facing and future authorized product workflows.
- Àríyá owns Re:Solve-specific reasoning, product context, tool use, workflow assistance and conversational product help.
- Àríyá is not Chatwoot Captain and is not powered by Captain.
- Captain must never be used as the general AI brain for Re:Solve.

### Chatwoot — support conversation infrastructure
- Chatwoot is the support conversation/inbox backbone.
- It may provide conversation persistence, inbox routing, assignment, agent participation, human takeover and support history.
- Using Chatwoot as transport does not make Captain the AI behind Re:Solve.

### Captain — client property support only
- Chatwoot Captain is reserved specifically for **client property support**.
- Captain may power or assist AI behavior within the property-support domain/conversations only.
- Captain has no role in powering general Re:Solve functionality, Àríyá, billing assistance, project assistance, CRM assistance, platform reasoning or other non-property Re:Solve AI experiences unless the owner explicitly changes this boundary later.
- Captain must not impersonate Àríyá or be branded as Àríyá.
- Property-support UI may still be presented as Re:Solve Support / Property Support; implementation must retain the architectural distinction between Captain-powered property support and Àríyá-powered Re:Solve assistance.

## Client conversation model

The Client Portal should expose one persistent lower-right conversation/help launcher rather than a permanent Àríyá navbar item or embedded Home-page Àríyá section.

The launcher can begin with Àríyá for general Re:Solve assistance. When the interaction becomes a **property-support** matter, the support workflow may route into the Chatwoot property-support domain where Captain is permitted to operate.

Human takeover/request-human support remains part of the Chatwoot support model. A client should not be forced to restart a support conversation when escalation occurs.

The implementation must make mode/domain transitions understandable and must not silently substitute Captain for Àríyá.

## Non-goals
- Do not use Captain as the Re:Solve copilot.
- Do not make Àríyá a Chatwoot AgentBot/Captain alias.
- Do not expose multiple competing AI identities without clear product purpose.
- Do not let support infrastructure become an authorization source for Re:Solve actions.

## Status
**OWNER-APPROVED / CANONICAL PRODUCT DECISION**
