---
name: resolve-portal
description: Use when building or reviewing a Re:Solve Client Portal page, client-safe projection, client action, organisation/property access flow, guest-to-portal transition, or portal navigation/mobile experience.
---

# Re:Solve Client Portal

Read the relevant `02-portal/*` spec, Client Portal Shell, Core UI Framework, permissions, PWA and source Admin/domain spec.

## Principle
Portal is a distinct calm client experience over shared business truth, not the Admin OS with controls hidden.

## Client-safe projection
Explicitly define what the client can see, why, and at what scope. Do not reuse unrestricted Admin payloads. Internal notes, staff-only health reasoning, hidden files, private costs, security metadata, other organisations and provider internals remain excluded unless explicitly authorized.

## UX
Use plain-language labels, obvious primary actions and calmer density. Surface `Requires your attention`, current work/status, support access and relevant billing/property/project context without exposing internal operational noise.

## Navigation
Keep goal-oriented root navigation simple. Notifications and Account live in global chrome. Vault appears only when authorized. Do not copy Admin's full navigation hierarchy.

## Support
Chatwoot remains the conversation engine. Portal provides support entry, entitlement/status, incidents and safe conversation references without rebuilding the agent console.

## Actions
Approvals, requested files, payments, access requests and profile/team changes use the same source records/registered Actions and are audited/authorized server-side.

## Mobile/PWA
Phone is a primary use case. Use touch-friendly cards, drawers, bottom navigation when appropriate, safe-area handling and explicit offline/stale states. Financial, Vault and high-risk writes require verified connectivity unless specifically designed otherwise.

## Multi-organisation users
Organisation context switching must be explicit and isolation-safe.

## Completion
Verify cross-organisation/property denial, client-safe API projection, hidden-data counts, mobile flow, plain-language copy and that completing a Portal action updates the canonical source record rather than a shadow portal record.