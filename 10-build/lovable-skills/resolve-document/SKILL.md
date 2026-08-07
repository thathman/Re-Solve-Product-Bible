---
name: resolve-document
description: Use when building or reviewing Re:Solve Document Studio, proposals, estimates/quotes, contracts, invoices, receipts, statements, reports, templates, rendering, secure delivery, acceptance, or signing handoff.
---

# Re:Solve Document Studio

Read `03-platform/document-studio.md`, Sales/Commercial, Billing, Secure External Access, Files/Vault, Operating Entity/Brand, Action Registry and security rules.

## Source of truth
The underlying business record remains authoritative. Document rendering must not become a second commercial database.

## Lifecycle
Model Template → Draft/Version → Review → Render → Send/Share → Recipient action → Final Snapshot.

Accepted/executed financial/commercial content receives an immutable Final Snapshot. Editing a template or draft later must never mutate what a recipient accepted/signed.

## Templates
Support typed merge variables, reusable sections/blocks, operating-entity branding, conditional sections, line-item/pricing tables, versioning, preview and validation. Missing required variables must fail visibly rather than render misleading blanks.

## Proposal/Estimate/Contract
Preserve linked Organisation/Contact/Opportunity/Service/Project/Billing context, expiration, revisions, optional items where applicable, approvals and event history.

## Delivery
Use authenticated Portal access or Secure External Access for narrow expiring guest actions. Track sent/viewed/accepted/declined/signature states only when evidence supports them.

## Signing
Re:Solve owns contract/document business truth. SignatureConnector/Documenso owns signature-envelope execution and evidence. Normalize provider status rather than exposing provider internals everywhere.

## Files/Vault
Ordinary generated documents use Files. Confidential protected versions use Vault and must not retain an ordinary File bypass path.

## Àríyá
May draft narrative, summarize scope or suggest clauses from permitted context. AI output is draft content; it cannot silently send, accept or legally execute a document.

## Rendering quality
Web and PDF outputs must preserve typography, tables, pagination, signatures/evidence, print margins, A4/Letter policy, accessible reading order where feasible and brand consistency.

## Completion
Verify version immutability, recipient permissions, secure-link expiry/revocation, missing-variable behavior, PDF/web parity, audit of consequential events and safe mobile review/acceptance.