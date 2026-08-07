# Secure External Access

## Purpose
Secure External Access allows a narrowly authorized external recipient to complete one specific view/action without requiring a full Client Portal account.

This is useful before a lead becomes a client or when a third party needs temporary access.

## Use cases
- view/accept proposal
- view/accept estimate
- sign contract through SignatureConnector
- upload requested file
- complete onboarding form
- complete survey
- review/approve deliverable
- download a controlled report/document
- access a handover package

## Access grant
A secure external grant should declare:
- token/reference stored securely
- target resource/action
- recipient identity/destination where known
- Operating Entity/Brand
- expiry
- maximum uses where appropriate
- authentication requirement
- permissions limited to the exact action
- download/copy policy
- revoke state
- created by
- purpose
- activity/audit

## Authentication levels
Depending on risk:
- possession of a strong expiring link
- email verification
- one-time code
- authenticated Portal account redirect when the recipient already has one

High-risk Vault secret access should not be normalized through generic guest links.

## Public URL safety
Links must:
- be unguessable
- expire
- be revocable
- avoid exposing internal record identifiers where possible
- never grant broader API access
- avoid leaking target content in URL parameters

## Experience
External pages should be calm, branded and focused on the requested action. They should not expose the full Re:Solve navigation shell.

Show:
- Operating Entity/Brand identity
- document/action title
- recipient/context where safe
- expiry when useful
- one primary action
- verification flow if required
- success/completion state
- revoked/expired state

## Document Studio
Proposal, estimate, contract and report delivery can use Secure External Access.

## Forms and Requests
External intake forms may either be public according to form policy or protected by a secure grant.

## Files
File request/upload links must restrict accepted destination, size/type and recipient scope.

## Audit
Record meaningful access/view/completion events according to privacy policy. Avoid pretending email/open tracking is perfect evidence.

## Notifications
Notify internal owner for material outcomes such as proposal accepted, contract signed, requested file uploaded or secure link expiring where useful.

## API/MCP/Àríyá
Creation/revocation is a controlled Action Registry operation. Àríyá may prepare a share but cannot expose the underlying secret token in ordinary conversation/history unnecessarily.

## Acceptance criteria
- recipients can complete narrow actions without fake Portal accounts
- link compromise cannot grant broader application access
- expiry/revocation are enforced server-side
- branding is consistent with Document Studio/Core UI
- activity is auditable without invasive tracking claims
