# Document Studio

## Purpose
Document Studio is Re:Solve's shared generation, versioning, signing, verification, review and delivery engine for business documents. Business records remain authoritative; Document Studio owns presentation and immutable issued output.

## Supported document families
Current/future families include:
- Proposals (including quote-style and estimate-style presentations);
- Contracts / statements of work;
- Invoices;
- Receipts;
- Credit Notes / formal adjustments;
- Account Statements;
- renewal notices;
- Project/Service reports;
- Incident/postmortem reports;
- handover/completion packs;
- letters/notices;
- plugin-defined official documents.

There is no separate Estimate/Quote document domain; those are Proposal presentation styles.

## Ownership model
Examples:
- Proposal owns offer lifecycle/pricing/decision;
- Contract owns agreement lifecycle;
- Invoice owns Billing truth;
- Document Studio owns templates, rendered versions, PDF bytes, issuer signatures, verification metadata and delivery evidence;
- SignatureConnector may own counterparty/legal e-sign transactions where configured.

## Core records
- Document Template;
- Template Version;
- Document Draft;
- Document Version;
- Render Job;
- Recipient/Delivery;
- External View Session;
- Acceptance Record where applicable;
- Issuer Signature Snapshot;
- Counterparty Signature Reference/Evidence where applicable;
- Final Signed PDF Snapshot;
- Document Verification Reference.

## Template capabilities
Templates support Operating Entity/Brand, document family, sections/blocks, declared merge variables, tables/line items, flat/quantity/duration pricing blocks, packages/options, discounts/taxes, assumptions/exclusions, milestones/deliverables, terms, attachments, conditional sections, page header/footer, signatures, web rendering, PDF rendering, A4/Letter, locale formatting and version history.

## Variable system
Variables come only from declared authorised data sources with formatting rules. Arbitrary template expressions cannot bypass record security.

## Universal signing rule
**Every issued/final Re:Solve-generated PDF must be signed by an authorised issuer.**

Draft previews may be visibly watermarked `DRAFT` and can remain unsigned.

The rule applies to Invoices and Receipts as well as Proposals, Contracts, Credit Notes, Statements, renewal documents and formal reports.

## Issuer signatures
Issuer signature is Re:Solve's evidence that an authorised Operating Entity/staff signatory issued the exact document.

Staff profile stores a Document/PDF Signature separately from HTML email signature. Operating Entity settings define authorised/default signatory rules by document family, such as:
- named staff member;
- issuing staff member;
- record owner where policy allows;
- Operating Entity authorised signature/seal.

Invoices/Receipts normally use an Operating Entity-authorised signatory rule and do not require client countersignature.

At issuance, the signature asset/name/title used is copied into an immutable **Signature Snapshot**. Later staff-profile or entity-signature changes do not alter historical documents.

## Counterparty signatures
Some documents additionally require client/third-party signature:
- Contracts;
- selected Proposals;
- formal Approvals/agreements;
- plugin-defined documents.

Counterparty e-signing may use a provider-neutral SignatureConnector. Re:Solve owns the exact final document snapshot and signature evidence/reference. The issuer-signature rule does not depend on a third-party connector.

## Final Signed PDF Snapshot
At minimum stores or deterministically references:
- exact rendered PDF bytes/version;
- business record + immutable revision;
- document number/reference;
- Operating Entity/Brand identity snapshot;
- Template Version;
- issuer Principal/staff/entity;
- signatory name/title;
- signature image/mark snapshot;
- issued timestamp;
- cryptographic document hash (for example SHA-256);
- verification reference/code;
- required counterparty signature evidence;
- delivery/acceptance evidence.

Final snapshots are immutable. Corrections create a new document/business record path rather than rewriting history.

## Verification
Issued documents may carry a human verification code and/or QR/link to a safe verification endpoint.

Public verification may disclose only approved information such as:
- document valid/invalid;
- safe document type/reference;
- issuing Operating Entity;
- issue date;
- hash match/status.

It must not expose confidential document contents, balances, client identity or hidden metadata merely because a code is known.

## Future cryptographic PDF signing
Certificate/X.509/PAdES-style cryptographic PDF signing may be added behind a provider-neutral signing capability. The initial required contract is visible authorised issuer signature + immutable PDF + hash + verification evidence + Audit.

## Proposal flow
Proposal Draft -> Internal Review/Ready -> Sent -> Viewed -> Revision/Negotiation -> Accepted/Declined/Expired/Withdrawn.

Each sent material revision is preserved. Acceptance applies to the exact revision. Final Proposal PDF is issuer-signed; optional client signature can be required by policy.

## Contract flow
Draft -> Review -> Ready for Signature -> Sent -> Partially Signed -> Executed -> Active -> Expiring/Renewing -> Superseded/Terminated/Expired.

Executed Contract preserves issuer signature plus all required counterparty signatures and exact hash/snapshot.

## Billing documents
Invoice, Receipt, Credit Note and Account Statement final PDFs are automatically issuer-signed at issue/generation. Billing truth remains in Billing records; Document Studio never recalculates financial authority independently.

## Secure external access
Documents may be delivered through Client Portal or narrow expiring Secure External Access. Higher-risk documents may require verification/OTP before view/decision.

## Delivery
Support Portal, secure web link, email, downloadable PDF, signature handoff and future Connector delivery. Status distinguishes queued/sent/provider-accepted/delivered/viewed/failed/revoked only where actual evidence exists.

## Document envelopes / packs
A client journey may group multiple real records/documents (for example Contract + Form Request + Invoice + File Request) into an onboarding pack. The pack does not collapse those records into one unstructured PDF.

## Portal
Authorised client users can view/download permitted signed documents, comment/request changes where enabled, accept/decline, sign required documents and view client-safe status/evidence.

## Ariya
Ariya may draft document narrative, explain a permitted document, prepare variables/content, compare revisions and identify missing signature/delivery requirements. It cannot silently issue/sign/send/accept legal or financial documents without the relevant registered action/policy.

## Audit
Audit template/version changes, generation, issue/signature snapshot, recipient/send, access/revoke, acceptance/decline, counterparty signatures, hash/verification creation and final snapshot.

## Acceptance criteria
- every final generated PDF has issuer signature;
- Invoice/Receipt PDFs are included in the rule;
- draft previews are clearly drafts;
- historical signed PDF/template/brand/signature content cannot change after issue;
- hash/verification reference ties evidence to exact bytes/version;
- counterparty signature is additional rather than confused with issuer signing;
- business record and rendered document responsibilities remain distinct;
- Secure External Access does not require fake Portal accounts;
- signing provider is replaceable/optional for issuer signing.

## Build slices
1. Template/version/render foundation.
2. issuer signature profiles/rules + signed PDF snapshot/hash/verification.
3. Proposal rendered web/PDF + revisions.
4. Billing document families.
5. Contract/counterparty SignatureConnector.
6. Secure External Access/delivery evidence.
7. document packs/envelopes + advanced verification/cryptographic connector hook.
