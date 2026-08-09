# Re:Solve AI + Support Architecture

## Canonical product boundary

Àríyá, Chatwoot, Chatwoot Captain, client website/property support, and Re:Solve human escalation are separate concerns. They must not be merged or silently substituted for one another.

## Àríyá — Re:Solve-only AI

- Àríyá is Re:Solve's own AI product and identity.
- Àríyá exists only inside Re:Solve surfaces and Re:Solve-controlled workflows.
- Àríyá powers Re:Solve assistance, reasoning, product context, tool use and future authorized product actions.
- Àríyá never becomes the AI embedded on a client's public website/property.
- Àríyá is not Chatwoot Captain, is not powered by Captain, and must never be presented as Captain.
- Captain has no role in powering Re:Solve or Àríyá.

## Client websites/properties and Chatwoot Captain

A client organisation may have one or more properties/websites managed or supported by the Re:Solve owner/provider.

Example:
- Re:Solve owner/provider: Airix Media.
- Client organisation: Adaeze Realty Group.
- Client property: an Adaeze website managed/supported by Airix Media.

When Airix Media is responsible for support on that Adaeze website/property, Chatwoot may be embedded on the Adaeze website as the public/customer support channel for that property.

- Chatwoot Captain may be enabled for that specific property-support inbox/site.
- In that context, Captain is the AI serving visitors/users of the Adaeze website/property support channel.
- Captain belongs to that property's support experience, not to Re:Solve.
- Captain may answer property/site support questions and later hand off to human support according to that property's support configuration.
- This property-support Captain identity must not be branded as Àríyá.

## Re:Solve human takeover through Chatwoot

Àríyá remains inside Re:Solve.

When a Re:Solve user asks Àríyá for a human, or Àríyá escalates according to future policy:

1. Àríyá stops acting as the client-facing responder for the escalated conversation.
2. Re:Solve routes/bridges the conversation into a dedicated Chatwoot inbox/property owned by the Re:Solve owner/provider, for example an Airix Media Re:Solve Support inbox.
3. That Chatwoot inbox is for HUMAN TAKEOVER of Re:Solve conversations.
4. **Captain must NOT be enabled on that Re:Solve human-takeover inbox/property.**
5. Human agents receive the relevant Re:Solve conversation/context and continue the support interaction.
6. This deliberate no-Captain rule prevents an AI-to-AI clash after Àríyá has escalated.

Therefore the canonical flow is:

`Re:Solve user -> Àríyá inside Re:Solve -> request/escalation -> dedicated owner Chatwoot human-support inbox (Captain disabled) -> human agent`

This is different from:

`Visitor on client website/property -> that property's Chatwoot inbox -> Captain if enabled -> human agent if needed`

These are separate conversation domains even when the same provider organisation manages both.

## Chatwoot's role

Chatwoot may support both domains, but with different inbox configurations:

### A. Re:Solve human-takeover inbox
- receives escalations from Àríyá/Re:Solve.
- Captain disabled.
- human support is the destination.
- Chatwoot provides conversation persistence, queueing, assignment, agent participation and history.

### B. Client property/website support inbox
- attached to a specific client property/site where the provider is responsible for support.
- Captain may be enabled when desired.
- Captain serves that property's website/support users.
- human takeover may also exist for that property's support flow.

Inbox/property configuration determines whether Captain participates. Captain is not globally associated with a client organisation and is never globally associated with Re:Solve.

## Client Portal launcher

The Client Portal may expose one persistent lower-right Àríyá launcher instead of a permanent navbar item or Home-page Àríyá section.

- The launcher opens Àríyá inside Re:Solve.
- A visible `Request human support` / `Talk to a person` affordance may initiate the Re:Solve-to-Chatwoot human escalation flow.
- The launcher does not switch to Captain.
- Human takeover is routed to the dedicated owner/provider Re:Solve support inbox with Captain disabled.
- Before the real Chatwoot bridge exists, takeover UI may be visual/demo-only and must not pretend a human is actually connected.

## Non-goals / prohibited conflations

- Do not route Àríyá into a Captain-enabled inbox for human takeover.
- Do not let Captain answer after Àríyá has requested a human.
- Do not use Captain as the Re:Solve copilot.
- Do not make Àríyá a Captain/AgentBot alias.
- Do not silently route a Re:Solve AI conversation into a client's website Captain.
- Do not assume every client property uses Captain; Captain is enabled only on property-support inboxes where explicitly configured.
- Do not let Chatwoot or Captain become an authorization source for Re:Solve actions.

## Status

**OWNER-APPROVED / CANONICAL PRODUCT DECISION**
