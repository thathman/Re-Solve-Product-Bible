# Human References and Record Lifecycle

## Purpose
Re:Solve uses stable machine identifiers internally while giving people readable references and consistent Archive -> Trash -> Restore -> Purge behavior where each domain permits it.

## Human-readable references
Major records may have references such as:
- `ORG-0042`
- `PRJ-2026-018`
- `TSK-2026-0142`
- `REQ-0098`
- `INC-0032`
- `PROP-0148`
- `PRO-2026-021`
- `CTR-2026-009`
- `INV-2026-0114`
- `PAY-2026-0081`

`Quote`/`Estimate` do not receive separate current-domain prefixes; they are Proposal presentation/import aliases.

Exact prefixes are configurable by domain/Operating Entity where appropriate.

## Numbering policy
A numbering definition may specify record type, Operating Entity, prefix/suffix, date/year segment, sequence padding, next number, reset policy where appropriate and preview.

Sequences must be safe under concurrency. Changing a template affects new references, not historical references.

## Machine identifiers
Human references are not database primary keys and should not be assumed globally immutable routing identifiers. APIs normally expose stable id plus human reference where useful.

## Aliases / redirects
Merged/migrated records may preserve old human/external references as aliases so historical links/import reconciliation remain understandable.

## Shared lifecycle vocabulary
Domains may define their own business statuses, while common record-retention lifecycle concepts include:
- Active;
- Archived;
- Trash / Soft Deleted where supported;
- Restored;
- Pending Purge;
- Purged;
- Retained under Hold.

Not every record supports every state. Financial, Audit, executed/signed commercial and legally retained records may use void/supersede/archive semantics instead of Trash/Purge.

## Archive
Archive removes a record from ordinary active workflows without destroying its historical meaning.

Before Archive, Re:Solve should evaluate material dependencies through the shared Dependency/Impact Inspector, including where relevant:
- active Projects/Tasks/Requests;
- Properties/Client Services/Recurring Arrangements;
- unpaid Billing;
- Contracts/Proposals;
- Portal Membership/access;
- assignments/Approvals/Renewals;
- Automations;
- Connector mappings;
- Monitoring;
- default/template references;
- open Attention;
- client visibility.

Domain policy decides whether a dependency is a blocker, warning, reassignment requirement or safe remaining historical link.

## Trash / Recycle Bin
Where deletion is supported, a record enters Trash rather than disappearing immediately.

The shared Recycle Bin/Trash management surface should show permission-safe:
- record type;
- title/reference;
- original context/location;
- deleted by;
- deleted at;
- purge-eligible date/retention countdown;
- hold/blocker state;
- Restore action;
- permanent-delete eligibility.

A user sees only records they are authorized to manage/restore. Trash must not become a data-leak bypass.

## Restore
Restore revalidates:
- caller permission;
- uniqueness/reference conflicts;
- parent/Organisation/Property relationships;
- required dependencies/defaults;
- access scope;
- Connector/provider state where relevant;
- current lifecycle constraints.

Restore should return a clear dependency/conflict result rather than silently recreating invalid links.

If the original parent/context no longer exists, the domain may require reassignment/selection before Restore completes.

## Purge
Purge is irreversible and honors:
- retention policy;
- legal/operational hold;
- Audit requirements;
- signed/financial/commercial preservation;
- dependency constraints;
- privacy/data-right outcome;
- backup/provider reality where relevant.

Purge is a High Impact Action, normally with step-up/strong confirmation and Dependency Inspector.

Records that must legally/financially remain are never exposed as ordinary purgeable Trash.

## Dependency / Impact Inspector
The shared inspector answers **what breaks or remains if this record is archived, disabled, removed or purged?**

It provides blockers, warnings, reassignment requirements and safer alternatives.

Examples:
- Organisation -> active Projects/Properties/Invoices/Memberships/Services;
- Staff/User -> owned Projects/Tasks/Approvals/Renewals/default signatory rules;
- Property -> Monitoring/Support/Projects/Services/Renewals;
- Service Catalogue item -> active Client Services/Recurring Arrangements/Proposal defaults;
- Template -> defaults/active Journeys/Automations/current usage;
- Connector -> Monitoring/Communications/Payments/Automations/Properties.

Impact counts/details remain authorization-scoped.

## Bulk archive / restore
Where domain policy allows, Archive/Restore may be bulk Actions with per-record eligibility evaluation and a mandatory preview of eligible/skipped/blocked records.

High-risk permanent purge is not broadly bulk-capable by default.

## Merge
Merge behavior is defined further in Import/Export/Data Quality. Merged records preserve Audit/provenance and redirect/alias information where useful.

## Ariya
Ariya may:
- explain why Archive/Delete is blocked;
- summarize dependency impact;
- recommend archive/reassign/merge instead of delete;
- find a recently trashed record;
- propose Restore through the registered Action.

Ariya cannot bypass retention/hold/financial preservation or purge authorization.

## Notifications / Attention
Routine Archive/Restore need not create noise. Blocked archival, orphaned responsibilities, pending purge under error, hold conflicts or restore failures may create Attention for authorized administrators.

## Acceptance criteria
- human references remain readable without becoming database ids;
- Proposal is the single offer numbering domain;
- Archive preserves history and evaluates dependencies;
- supported deletions use Trash/Recycle Bin first;
- Restore revalidates current relationships/permissions;
- Purge respects retention/hold/financial/signed-document constraints;
- Dependency Inspector is permission-aware;
- bulk lifecycle Actions show eligibility/impact;
- financial/Audit/executed records use safe lifecycle semantics;
- Ariya cannot bypass preservation/security rules.
