# Document Studio

## Purpose
Document Studio is Re:Solve's shared generation, versioning, review and delivery engine for business documents.

It supports structured commercial and operational documents without collapsing their business records into files.

## Supported document families
Initial and future document types may include:
- proposals
- estimates / quotes
- contracts
- statements of work
- invoices
- receipts
- credit notes
- account statements
- renewal notices
- project reports
- service reports
- incident/postmortem reports
- handover packs
- letters/notices
- plugin-defined document types

## Ownership model
The business record remains authoritative.

Examples:
- Proposal record owns proposal status/pricing/acceptance
- Contract record owns contract lifecycle
- Invoice owns billing truth
- Document Studio owns presentation template, rendered versions, delivery and document snapshot metadata
- Documenso or another SignatureConnector owns the signature transaction

## Core records
- Document Template
- Template Version
- Document Draft
- Document Version
- Render Job
- Recipient/Delivery
- External View Session
- Acceptance Record where applicable
- Signature Reference
- Final Snapshot

## Template capabilities
Templates support:
- Operating Entity / Brand
- document type
- title and description
- sections/blocks
- merge variables
- tables and line items
- pricing blocks
- optional/add-on items
- one-time and recurring charges
- taxes/discounts
- assumptions
- exclusions
- milestones/deliverables
- terms
- attachments
- conditional sections
- page headers/footers
- signatures/acceptance block
- web rendering
- PDF rendering
- A4/Letter output
- locale-ready formatting
- version history

## Variable system
Variables must come from declared data sources with permissions and formatting rules.

Examples:
- client organisation
- contact
- operating entity
- opportunity
- proposal/estimate
- service
- property
- project
- invoice/payment
- dates

Do not allow arbitrary template expressions to bypass security.

## Proposal flow
Typical flow:
Draft -> Internal Review -> Sent -> Viewed -> Client Comment/Revision -> Accepted/Declined/Expired -> Converted/Closed.

Capabilities:
- template selection
- editable narrative
- pricing table
- optional items
- secure external link or Portal delivery
- recipient tracking where privacy policy allows
- comments/questions where enabled
- revision/version history
- accept/decline
- expiry/reminders
- convert accepted proposal into downstream commercial records according to workflow

Àríyá may draft scope, narrative, assumptions, exclusions and summaries from authorized context. Human review remains required before send unless an explicit approved automation says otherwise.

## Contract flow
Typical flow:
Draft -> Internal Review -> Sent for Signature -> Partially Signed -> Executed -> Active -> Expiring/Renewing -> Superseded/Terminated/Expired.

Re:Solve owns contract status/metadata and the exact final snapshot. Signature execution is delegated to a SignatureConnector such as Documenso.

## Immutable accepted/executed snapshots
Once a recipient accepts a proposal/quote or a contract is executed, the accepted/executed content is stored as an immutable final snapshot.

Later template edits must never alter historical accepted documents.

## Secure external access
Documents may be delivered through the Client Portal or a narrow expiring Secure External Access link.

Higher-risk documents may require email verification/OTP before view/acceptance.

## Delivery
Support:
- Portal
- secure web link
- email delivery
- downloadable PDF
- signature handoff
- future connector delivery

Delivery status must distinguish sent, delivered where provider evidence exists, viewed where allowed, failed and revoked.

## Document numbering
Uses the shared human-reference/numbering framework. Numbering may be scoped by Operating Entity and document type.

## Confidential documents and Vault
A generated final document may be promoted to/protected as a Vault Item when confidentiality policy requires it. Ordinary document metadata must not create a bypass around Vault controls.

## Portal
Client users can, where authorized:
- view document
- download permitted version
- comment/request changes where enabled
- accept/decline
- sign through connector
- view status/history safe for client

## Notifications and Attention
Examples:
- proposal sent
- proposal viewed if policy permits
- proposal expiring
- proposal accepted/declined
- contract signature waiting
- contract executed
- contract expiry approaching
- render/delivery failed

## API/MCP
Expose controlled template/document metadata and generation actions. AI/MCP cannot silently send, accept or sign legal/commercial documents without explicit policy and confirmation.

## Audit
Audit:
- template/version changes
- generation
- recipient/send
- access/revoke
- acceptance/decline
- signature references
- final snapshot creation

## Acceptance criteria
- final accepted/executed content cannot change after the fact
- business record and rendered document responsibilities remain distinct
- templates are reusable across brands/entities
- generated documents work as web and PDF experiences
- secure guest delivery does not require creating fake Portal users
- Àríyá drafts remain drafts until approved
- signing remains connector-backed
