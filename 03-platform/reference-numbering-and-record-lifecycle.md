# Human References and Record Lifecycle

## Purpose
Re:Solve uses stable machine identifiers internally while giving people readable references and consistent archive/delete/restore behavior.

## Human-readable references
Major records may have references such as:
- `ORG-0042`
- `PRJ-2026-018`
- `REQ-0098`
- `INC-0032`
- `PROP-0148`
- `PRO-2026-021`
- `EST-2026-015`
- `CTR-2026-009`
- `INV-2026-0114`
- `PAY-2026-0081`

Exact prefixes are configurable by domain/Operating Entity where appropriate.

## Numbering policy
A numbering definition may specify:
- record type
- Operating Entity
- prefix/suffix
- date/year segment
- sequence padding
- next number
- reset policy where appropriate
- preview

Sequences must be generated safely under concurrency.

Changing a numbering template affects new references, not historical references.

## Machine identifiers
Human references are not database primary keys and should not be assumed globally immutable routing identifiers.

APIs should normally expose both stable id and human reference where useful.

## Aliases/redirects
Merged or migrated records may preserve old human/external references as aliases so links/import reconciliation remain understandable.

## Lifecycle vocabulary
Different domains may have specific statuses, but shared record lifecycle concepts include:
- Active
- Archived
- Soft Deleted / Trash where supported
- Restored
- Pending Purge
- Purged
- Retained under Hold

Not every record supports deletion. Financial/audit/executed commercial records may use void/supersede/archive semantics instead.

## Archive
Archive removes a record from normal active workflows without destroying history.

Archive should consider:
- active dependencies
- assignments
- access grants
- automations
- connector mappings
- open Attention
- client visibility

## Trash / restore
Where supported, soft-deleted records may enter a Trash/Recycle Bin for a configured period before purge.

Restore should revalidate conflicts, permissions and relationships.

## Purge
Purge is irreversible and must honor retention, legal/operational holds, audit policy and connected-record constraints.

## Merge
Merge behavior is defined further in Import/Export/Data Quality. Merged records preserve audit/provenance and redirect/alias information where useful.

## Notifications/Attention
Archive/delete actions should not create routine noise, but blocked archival, purge failures or unresolved dependencies may generate Attention for authorized administrators.

## Acceptance criteria
- humans can communicate record references without exposing implementation IDs
- sequence changes never renumber history
- financial/audit records use safe domain lifecycle semantics
- restore/purge behavior is deliberate and permissioned
- archived records stop ordinary workflow participation without losing historical relationships
