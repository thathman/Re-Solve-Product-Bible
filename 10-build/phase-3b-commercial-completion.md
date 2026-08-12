# Phase 3B — Commercial Completion

Prefix: `CCF`

Status: **Active continuation of Phase 3 after the 2026-08 Product Bible replan.**

## Purpose
Finish the canonical commercial foundation while preserving the already-shipped Client/CRM/Property/Sales/Billing truth.

Canonical spine for this phase:

`Lead -> Organisation/Contact -> Opportunity -> Proposal -> Acceptance -> Portal Invitation -> Contract/Recurring Arrangement where applicable -> Invoice/Adjustment -> Payment`

Projects/delivery execution move to Phase 5. Full Communications/Inbox/Chatwoot work moves to Phase 6. Phase 3B implements only the communication/document primitives required for a complete commercial transaction.

## Dependencies / inherited truth
- Phase 1 Data Truth complete.
- Phase 2 Support Operating Foundation complete.
- Phase 3A Clients, CRM and Properties are production foundations.
- Existing Sales Quote implementation and decision evidence are migration foundations, not discarded work.
- Billing migrations/engineering acceptance already exist on the active Billing branch and are released first.
- RLS/tenant isolation, server-authoritative identity, bigint minor-unit money and no silent cross-currency aggregation remain mandatory.

## Legacy CCC reconciliation
- `CCC-001...129` remain historical evidence for Phase 3A; completed engineering is not repeated.
- `CCC-130...151` Projects are transferred to revised Phase 5 Delivery Operations.
- `CCC-152...160` are absorbed into CCF commercial Documents/Email/Data obligations or later Communications/Governance phases.
- `CCC-161...175` are superseded by the CCF phase-wide closure gate below.
- `CCC-037` and equivalent browser-deferred items are covered by the consolidated Phase 3B final Admin/Portal Work/browser gate.

## A. Replan, production baseline and release sequencing
- [x] CCF-001 Create the owner-visible Phase 3B atomic ledger before implementation resumes.
- [x] CCF-002 Verify current application production baseline is `main` v1.18.0.0 SHA `70d08514ef78610472100e9f5544c07e04ebdd91` before Billing promotion.
- [x] CCF-003 Verify active Billing branch exists and preserves Hendrix-authored engineering evidence; latest observed branch SHA is `ee3893fe523071c4e77b4451492055a8b9487303`.
- [x] CCF-004 Reconcile the legacy CCC pending scope into the revised roadmap instead of executing stale Projects/shared-foundation tasks blindly.
- [x] CCF-005 Review the Product Oversight Register and absorb OVR-001/002/003/005/006/007/008/009/021/022/023/024/025/027/028/030 into Phase 3B where their dependency is now real.
- [ ] CCF-006 Re-audit the current Sales Quote and Billing schema/code immediately before migration design so the Product Bible model is mapped onto real production truth.
- [ ] CCF-007 Reconfirm live Supabase migration state and post-rollback Billing baseline before any new CCF migration.
- [ ] CCF-008 Reconfirm generated-type/domain-overlay strategy and eliminate any stale type assumption that would make Proposal/Contract/Adjustment work unsafe.
- [ ] CCF-009 Define the compatibility strategy for existing Quote IDs, decision evidence, routes and historical links during Proposal unification.
- [x] CCF-010 Reserve one consolidated Admin + Portal browser/ChatGPT Work gate for Phase 3B closure rather than claiming browser passes per internal slice.

## B. Close and promote the current Billing release
- [ ] CCF-011 Verify the latest canonical Billing branch CI on the evidence-complete tree: tests, ESLint, TypeScript, production build and PWA/output.
- [ ] CCF-012 Review PR #12 metadata, review submissions, inline threads and comments for unresolved blocking findings.
- [ ] CCF-013 Remove generated/bot attribution and stale claims from PR #12 body while preserving truthful migration/acceptance evidence.
- [ ] CCF-014 Collapse the Billing branch to one clean Hendrix-authored `v1.19.0.0: complete Billing operations` release commit without changing the qualified tree.
- [ ] CCF-015 Verify the clean Billing release commit has the expected `main` parent, one-commit diff and Hendrix author/committer identity.
- [ ] CCF-016 Run exact-SHA canonical CI on the clean Billing release commit.
- [ ] CCF-017 Fast-forward `main` to the exact tested Billing SHA without a synthetic merge commit.
- [ ] CCF-018 Verify independent `main` CI on the exact promoted SHA.
- [ ] CCF-019 Verify OpenShip reaches `ready`, reports the exact promoted SHA and passes production `/api/health`; record the post-release Billing data baseline.

## C. Opportunities / Deals
- [ ] CCF-020 Audit current CRM/Sales schema and UI for any hidden/shadow Opportunity-like state before adding a new domain.
- [ ] CCF-021 Define the canonical Opportunity record and Organisation/Contact/Lead ownership relationships.
- [ ] CCF-022 Define Opportunity lifecycle/stages without making the core lifecycle arbitrarily user-configurable where state semantics matter.
- [ ] CCF-023 Add configurable sales pipeline/stage presentation only where it does not weaken canonical terminal/commercial states.
- [ ] CCF-024 Preserve Lead conversion separately from Opportunity creation so one Organisation can have multiple Opportunities.
- [ ] CCF-025 Support Opportunity ownership/assignment using active staff principals, not HR hierarchy.
- [ ] CCF-026 Store estimated/expected Opportunity value in bigint minor units with explicit currency.
- [ ] CCF-027 Relate Opportunities to Properties, Contacts and source Leads with same-Organisation validation.
- [ ] CCF-028 Reuse CRM Activities/follow-ups appropriately without duplicating platform Activity.
- [ ] CCF-029 Relate one Opportunity to Proposal history/revisions without copying Proposal financial truth.
- [ ] CCF-030 Define won/lost/abandoned/converted semantics and preserve terminal evidence.
- [ ] CCF-031 Add Opportunity Action Registry actions and risk/confirmation metadata.
- [ ] CCF-032 Derive Opportunity Attention from real stale/follow-up/decision dates rather than a synthetic score.
- [ ] CCF-033 Build Admin Opportunity directory/detail with search, filters, useful zero states and relationship navigation.
- [ ] CCF-034 Keep Opportunities internal by default; Portal sees only client-safe resulting Proposal/Contract/Project records.
- [ ] CCF-035 Add migration, RLS, tenant-isolation, lifecycle and conversion/relationship regression tests with rollback acceptance.

## D. Service Catalogue, Price Books and pricing basis
- [ ] CCF-036 Audit existing product/service/item fields in Sales/Billing before introducing a canonical Service Catalogue.
- [ ] CCF-037 Define Service Catalogue Item identity, type/category, description, active/archive state and Operating Entity scope.
- [ ] CCF-038 Define the canonical pricing-basis contract: `flat`, `quantity`, or `duration`.
- [ ] CCF-039 Support duration units `day`, `week`, `month`, `quarter`, `year` with exact numeric duration and no implied recurrence.
- [ ] CCF-040 Preserve quantity pricing independently from duration so a duration service never needs fake quantity semantics.
- [ ] CCF-041 Define Service Catalogue default price/currency in bigint minor units and preserve historical Proposal/Invoice line snapshots when catalogue prices later change.
- [ ] CCF-042 Support catalogue categories/tags without turning lifecycle authority into free-text taxonomy.
- [ ] CCF-043 Support Price Books/Rate Cards scoped by Operating Entity and, where justified, Client/Organisation.
- [ ] CCF-044 Define deterministic price resolution/fallback precedence and expose which price source was selected.
- [ ] CCF-045 Support Service packages/bundles and optional/add-on items without duplicating individual Service Catalogue identities.
- [ ] CCF-046 Define tax behavior/config references per catalogue item without hardcoding jurisdictional rates.
- [ ] CCF-047 Define discount eligibility/defaults separately from final Proposal/Invoice adjustment evidence.
- [ ] CCF-048 Mark whether a Service is duration-priced, recurring-eligible and/or renewal-relevant without conflating those concepts.
- [ ] CCF-049 Allow an optional future Project Template reference without creating Phase 5 Project work in Phase 3B.
- [ ] CCF-050 Build Proposal line selection from Service Catalogue plus controlled custom-line support.
- [ ] CCF-051 Build Admin Service Catalogue and Price Book management with search/filter/archive states.
- [ ] CCF-052 Register high-impact catalogue/price changes in Activity/Audit and Action Registry where appropriate.
- [ ] CCF-053 Prevent deleting/archiving items blindly when active Proposal/Recurring/other dependencies require an impact warning.
- [ ] CCF-054 Preserve unlike currencies and never silently copy a rate from one currency into another.
- [ ] CCF-055 Add pricing-basis, duration, Price Book, scope, snapshot, money and RLS tests.

## E. Proposal unification — Proposal / Quote / Estimate as one domain
- [ ] CCF-056 Audit `sales_quotes`, quote items, client-decision evidence, routes, notifications and Portal surfaces as the migration foundation.
- [ ] CCF-057 Choose the physical schema migration/compatibility approach that preserves stable IDs/history while making Proposal the canonical product concept.
- [ ] CCF-058 Migrate/bridge existing Quote records and decisions without rewriting historical acceptance evidence or fabricating revisions.
- [ ] CCF-059 Define one Proposal record with presentation style/mode for `proposal`, `quote`, or `estimate` rather than separate business domains.
- [ ] CCF-060 Define Proposal lifecycle from Draft/Ready/Sent/Viewed through Accepted/Declined/Expired/Cancelled.
- [ ] CCF-061 Enforce sent/issued Proposal immutability; commercial changes create a new revision rather than silently modifying what the client saw.
- [ ] CCF-062 Add Proposal revision/version lineage and preserve the exact accepted revision.
- [ ] CCF-063 Use flat/quantity/duration pricing on Proposal lines with server-authoritative totals.
- [ ] CCF-064 Support package/option selection and optional add-ons while preserving the client's exact accepted selection snapshot.
- [ ] CCF-065 Support fixed/percentage line discounts and Proposal-level discounts with explicit calculation evidence.
- [ ] CCF-066 Keep taxes/fees explicit and jurisdiction-configured; no hidden percentage assumptions.
- [ ] CCF-067 Support validity/expiry and derive expiring/expired Attention from authoritative dates.
- [ ] CCF-068 Support narrative Proposal sections: introduction/summary, scope, deliverables, exclusions/assumptions, timeline, pricing, terms and attachments.
- [ ] CCF-069 Relate Proposal to Opportunity, Organisation, Contact, Property and source commercial context with tenant validation.
- [ ] CCF-070 Define deterministic Proposal numbering and Operating Entity prefix/display strategy while preserving historical Quote numbers.
- [ ] CCF-071 Record actual client `Viewed` evidence distinctly from merely `Sent` where secure delivery can prove it.
- [ ] CCF-072 Define Proposal send/delivery state from real delivery attempts rather than optimistic UI state.
- [ ] CCF-073 Support Secure External Access for pre-Portal Proposal viewing/decision with expiring/revocable scoped tokens.
- [ ] CCF-074 Preserve authenticated/secure client accept/decline evidence: actor/contact snapshot, revision, items/options, timestamp and relevant request metadata.
- [ ] CCF-075 Keep issuer-signed PDF mandatory; make client e-signature/explicit signature policy configurable by Proposal/template rather than mandatory for every commercial offer.
- [ ] CCF-076 Prevent staff from impersonating client acceptance/rejection through ordinary Admin mutations.
- [ ] CCF-077 Make accepted Proposal evidence immutable even if Contact/Organisation details later change.
- [ ] CCF-078 Provide explicit accepted-Proposal next actions: create Invoice/deposit, Contract, Project handoff record, Recurring Arrangement and/or Client Journey policy trigger.
- [ ] CCF-079 Make all Proposal downstream handoffs idempotent and retry-safe.
- [ ] CCF-080 Preserve legacy Quote URLs/API references through redirects/compatibility where necessary while canonical UI/routes use Proposal terminology.
- [ ] CCF-081 Build Admin Proposal directory/detail/composer/revision experience without three duplicate Proposal/Quote/Estimate modules.
- [ ] CCF-082 Build client-safe Proposal/secure-guest decision experience with selected option/total/terms clarity.
- [ ] CCF-083 Emit Proposal Activity/Audit/notifications once per real lifecycle/delivery/decision event.
- [ ] CCF-084 Add Proposal lifecycle, revision, pricing, options, acceptance, secure-access, tenant and idempotency tests.

## F. Contracts and Recurring Arrangements
- [ ] CCF-085 Audit any reserved Contracts UI/schema references before creating the canonical Contract domain.
- [ ] CCF-086 Define Contract identity/type, Organisation/Contact/Proposal relationships and numbering.
- [ ] CCF-087 Define Contract lifecycle including Draft/Sent/Awaiting Signature/Signed/Active/Expired/Terminated/Cancelled as required by real evidence.
- [ ] CCF-088 Bind each Contract to an immutable template/document revision rather than regenerating historical terms from current templates.
- [ ] CCF-089 Require issuer-signed final Contract PDF and preserve issuer-signature snapshot/hash/verification evidence.
- [ ] CCF-090 Support counterparty signature fields/evidence, signer identity, timestamp, IP/user-agent/auth method and decline reason.
- [ ] CCF-091 Support multiple signers/order only where the initial Contract workflow actually requires it; do not invent a full legal-workflow suite unnecessarily.
- [ ] CCF-092 Support Contract attachments, internal notes/activity and client-safe document access without leaking internal collaboration.
- [ ] CCF-093 Track Contract start/end/expiry and renewal history with derived Attention/reminders.
- [ ] CCF-094 Build Admin and Portal Contract surfaces plus Action Registry/Audit/RLS tests.
- [ ] CCF-095 Define Recurring Arrangement/Retainer as distinct from duration-priced one-off Service lines and from provider card subscriptions.
- [ ] CCF-096 Store Recurring Arrangement frequency, start/end, next billing date, status and related Organisation/Property/Service lines.
- [ ] CCF-097 Reuse Service Catalogue snapshots and explicit currency/pricing rather than mutable catalogue totals.
- [ ] CCF-098 Define draft/issued recurring Invoice generation policy, reminders and manual/automatic approval boundary.
- [ ] CCF-099 Support pause/resume/cancel/end behavior with evidence and no retroactive rewrite of already-issued financial records.
- [ ] CCF-100 Relate Recurring Arrangements to future Projects/Client Services/Renewals without implementing those later-phase engines prematurely.
- [ ] CCF-101 Build Admin/Portal recurring-arrangement visibility appropriate to commercial commitments.
- [ ] CCF-102 Add lifecycle, next-billing, scope, RLS, money and idempotent-generation tests.

## G. Commercial Document Studio minimum + email delivery minimum
- [ ] CCF-103 Implement the shared Document Studio generation boundary required by commercial records; no one-off PDF generators per domain.
- [ ] CCF-104 Add versioned Document Templates and template-variable validation for Proposal, Contract, Invoice, Receipt, Credit Note and statement-like outputs required in this phase.
- [ ] CCF-105 Apply Operating Entity brand/theme inputs including identity, address, registration/tax details, logo and footer/legal content.
- [ ] CCF-106 Add separate Staff Document/PDF Signature profile configuration, distinct from HTML email signature.
- [ ] CCF-107 Add Operating Entity signatory rules/default signatory policy by document family.
- [ ] CCF-108 Enforce the canonical rule: every issued/final generated PDF is issuer-signed, including Invoices and Receipts.
- [ ] CCF-109 Persist immutable PDF snapshot, template version, brand version, signatory snapshot, issued timestamp and SHA-256/document hash evidence.
- [ ] CCF-110 Add safe document verification code/reference and public verification response that never leaks confidential commercial detail.
- [ ] CCF-111 Integrate signed immutable PDFs into Proposal issue/send and accepted revision evidence.
- [ ] CCF-112 Integrate signed immutable PDFs into Contract execution/signing.
- [ ] CCF-113 Integrate signed immutable PDFs into Invoice issue and Receipt creation without rewriting legacy historical records.
- [ ] CCF-114 Integrate signed output for Credit Notes/Adjustments when those records become document-bearing.
- [ ] CCF-115 Implement a provider-agnostic transactional Email delivery interface required by Proposal/Contract/Invoice/Receipt workflows.
- [ ] CCF-116 Implement composable email rendering: universal head/styles -> Operating Entity header -> template body -> Staff or system signature -> footer/legal.
- [ ] CCF-117 Add Staff HTML email-signature configuration separately from Workspace/Operating Entity signature defaults.
- [ ] CCF-118 Persist outbound delivery attempts/results, retries/failures and record linkage without provider secrets.
- [ ] CCF-119 Provide email/document preview and test-send/test-render behavior before template activation where applicable.
- [ ] CCF-120 Add the minimum job/queue/retry worker contract necessary for reliable PDF/email delivery; full Shared Inbox/Connected Mailboxes remain Phase 6.

## H. Commercial Adjustments, discounts, deposits and payment plans
- [ ] CCF-121 Define the canonical Commercial Adjustment/Credit model instead of mutating Payment truth or destructively editing issued Invoices.
- [ ] CCF-122 Support explicit adjustment types including discount, late fee, penalty, service charge, credit, write-off, refund-related adjustment and other controlled fee/credit classifications.
- [ ] CCF-123 Record whether an Adjustment was manual, policy-generated or downstream-provider evidence, with actor/policy/source provenance.
- [ ] CCF-124 Support fixed-amount and percentage policies using bigint minor-unit calculations and explicit rounding rules.
- [ ] CCF-125 Define late-fee grace period, one-time/recurring policy where allowed, caps and applicability without inventing legal/jurisdiction assumptions.
- [ ] CCF-126 Derive Invoice amount due/balance from authoritative issued items, Adjustments, Payments and effective allocations rather than an editable balance field.
- [ ] CCF-127 Add Credit Note evidence/document generation for post-issue reductions that require a commercial document.
- [ ] CCF-128 Preserve Refund evidence separately from Payment receipt evidence; never rewrite the original Payment amount/date/reference.
- [ ] CCF-129 Preserve current verified/failed/allocated Payment evidence and receipted-allocation protections from the Billing foundation.
- [ ] CCF-130 Support Proposal/Invoice deposit requirements and fixed/percentage deposit amounts.
- [ ] CCF-131 Support explicit payment/installment schedules with due dates/amounts while keeping each actual Payment independent evidence.
- [ ] CCF-132 Allow Proposal acceptance policy to idempotently create the configured deposit/first Invoice without assuming automatic card collection.
- [ ] CCF-133 Build Admin Adjustment/Credit/payment-plan controls with suitable confirmation/Approval boundaries.
- [ ] CCF-134 Build Portal evidence for client-safe Adjustments, Credits, due schedule and resulting balance.
- [ ] CCF-135 Emit Activity/Audit/Attention and notifications only from real commercial/financial events.
- [ ] CCF-136 Add adjustment, late-fee, credit, deposit, schedule, money, RLS and negative-case tests.

## I. Portal commitment gate and commercial access
- [ ] CCF-137 Canonicalize Portal Membership lifecycle `none -> invited -> active -> suspended -> revoked` independently from Contact/Organisation existence.
- [ ] CCF-138 Make accepted Proposal the default idempotent Portal invitation trigger, subject to configured commercial/onboarding policy.
- [ ] CCF-139 Preserve a manual `Invite to Portal` Action for exceptional pre-commitment cases with full Audit.
- [ ] CCF-140 Use Secure External Access for discovery/Proposal/Contract/Form-like pre-commitment experiences where a full account is unnecessary.
- [ ] CCF-141 Ensure repeated acceptance/invite requests cannot create duplicate memberships/invitations.
- [ ] CCF-142 Support per-Contact Portal capabilities/relationship scope so billing/project/support contacts need not see identical surfaces.
- [ ] CCF-143 Build/adjust Portal commercial `Needs Your Attention` items for Proposal decisions, Contract signatures and outstanding Billing actions.
- [ ] CCF-144 Expose Proposal history/accepted offer safely to the committed client.
- [ ] CCF-145 Expose Contract documents/signature state safely to the committed client.
- [ ] CCF-146 Preserve Invoice/Payment/Receipt/Adjustment visibility from authoritative Billing data and RLS.
- [ ] CCF-147 Harden Secure External Access token scope, expiry, revocation, one-time/action semantics and tenant isolation.
- [ ] CCF-148 Implement the backend/authorization contract needed for future `Preview as Client` read-only UX; no client-authored mutation may execute in preview context.
- [ ] CCF-149 Add Portal membership, invitation, guest-access, per-contact visibility, suspended-client and cross-tenant regression tests.

## J. Phase-wide acceptance, browser gate and closure
- [ ] CCF-150 Verify foreign-Organisation denial across Opportunity, Catalogue/Price Book, Proposal, Contract, Recurring, Adjustment and Portal workflows.
- [ ] CCF-151 Verify suspended/revoked Portal principals cannot gain access through guest, membership, Proposal or Billing paths.
- [ ] CCF-152 Verify no new ordinary CRUD path depends on service-role authority.
- [ ] CCF-153 Verify all commercial money uses bigint minor units and rejects float-based authority.
- [ ] CCF-154 Verify unlike currencies are never silently aggregated, priced or converted.
- [ ] CCF-155 Verify Proposal acceptance, Portal invitation, Contract/Recurring creation and deposit/Invoice handoffs are idempotent on retry.
- [ ] CCF-156 Verify Activity/Audit/notification evidence is emitted exactly once for important cross-domain lifecycle events.
- [ ] CCF-157 Run rollback-only production database acceptance for new migrations/triggers/RPCs and restore the exact baseline after probes.
- [ ] CCF-158 Regenerate/reconcile live Supabase TypeScript types after Phase 3B schema stabilizes and retire temporary domain overlays where safe.
- [ ] CCF-159 Run complete Vitest, ESLint, TypeScript, production build and PWA/output gates on every release candidate.
- [ ] CCF-160 Promote only exact CI-tested SHAs through OpenShip and require `ready`, exact SHA and `/api/health` evidence.
- [ ] CCF-161 Reconcile all absorbed OVR items and add/assign every newly discovered oversight before browser closure.
- [ ] CCF-162 Produce the consolidated Phase 3 Admin browser/ChatGPT Work acceptance script covering Clients, CRM, Properties, Opportunities, Catalogue, Proposals, Contracts, Recurring and Billing.
- [ ] CCF-163 Produce the consolidated Phase 3 Portal/secure-guest browser acceptance scope covering tenant isolation, Proposal/Contract decisions, Portal invitation and Billing evidence on desktop/mobile.
- [ ] CCF-164 Fix all blocking browser findings end-to-end, rerun database/security/CI gates and update the phase ledger.
- [ ] CCF-165 Deploy the exact corrected SHA through OpenShip and re-verify production health after browser fixes.
- [ ] CCF-166 Close Phase 3 only when every blocking CCF item is evidenced and every defer has an explicit later-phase owner/reason.

## Explicitly later, not forgotten
- Projects, Project Templates, Tasks, Project Financial Plan, Client Journeys, full Forms/File Requests/Booking/Approvals: Phase 5.
- Full Connected Mailboxes/Shared Inbox/inbound email/Chatwoot/Review Requests/Notes/Calendar: Phase 6.
- Full Property Health/Monitoring, Files, Knowledge, Vault: Phase 7.
- Full Ariya/Automations/Dry Run/Reports/Search intelligence: Phase 8.
- Template Center governance, Custom Fields, Saved Views, granular permissions, Recycle Bin, Dependency Inspector, Bulk Actions/import/export: Phase 9.
- Connector/API/MCP/plugin breadth: Phase 10.
- First-run installer, PWA/product documentation/full production-readiness closure: Phase 11.

## Completion definition
Phase 3B is complete only when the canonical commercial spine is operational and evidence-backed from Opportunity through Proposal/Contract/Billing/Portal commitment, every new issued commercial PDF is signed/immutable, current Billing has been production-promoted, cross-tenant/money/idempotency tests pass, and the consolidated Admin/Portal browser gate is closed on the exact deployed SHA.
