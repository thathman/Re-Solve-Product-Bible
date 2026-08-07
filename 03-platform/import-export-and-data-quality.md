# Import, Export, Migration and Data Quality

## Purpose
Re:Solve must be adoptable, portable and repairable. Data should be importable with validation, exportable under permission, migratable between systems and continuously reviewable for quality.

## Import framework
Supported initial formats may include CSV and spreadsheet-like structured files. Plugins may contribute specialized importers.

An import flow should support:
1. choose record type/importer
2. upload/source file
3. inspect columns/sample
4. map fields
5. configure transformations/defaults
6. duplicate matching strategy
7. dry-run validation
8. review errors/warnings
9. execute as background job
10. review results
11. retry/correct failures
12. retain import history/provenance

## Import batch
Fields:
- id
- source
- target type
- importer/version
- initiated by
- mapping definition
- dry-run summary
- state
- row counts
- created/updated/skipped/failed counts
- started/completed
- error artifact
- rollback/support capability

## Duplicate strategy
Potential matching inputs:
- explicit external id
- canonical reference
- email/phone for Contact only as evidence, never universal identity truth
- organisation name/domain with review
- configured unique field

Imports must not silently merge ambiguous records.

## Migration
Migration jobs may be used for:
- legacy Re:Solve data
- CRM replacement
- external finance/project/contact data
- plugin data upgrades

Migration preserves source identifiers/provenance for troubleshooting.

## Export
Export is permission-controlled and may support:
- current filtered view
- selected records
- report dataset
- client data package
- full administrative backup/export where separately authorized

Exports must exclude unauthorized fields and protected Vault values by default.

Large exports run as background jobs with expiry/revocation policy for generated artifacts.

## Client data package
Authorized staff/client workflows may produce a controlled package containing selected:
- organisation profile
- contacts
- properties
- projects
- generated documents
- invoices/receipts/statements
- files
- knowledge
- permitted Vault items through explicit protected handling

The package uses Files/Document Studio/Secure External Access rather than bypassing their permissions.

## Data Quality Center
Data quality should be an operational surface, not a hidden admin script.

Issue types may include:
- possible duplicate Organisations/Contacts/Properties
- missing required data
- stale contact information
- missing account owner
- invalid/missing connector mappings
- stale connector sync
- orphaned files
- invalid property relationship
- expired portal invitation/access
- unresolved external-id collision
- missing renewal owner/date
- inconsistent derived/source data

## Quality issue lifecycle
- OPEN
- REVIEWED
- FIXED
- IGNORED with reason
- AUTO_RESOLVED

High-value issues may generate Attention items.

## Merge/deduplication
A safe merge flow should support:
- preview both records
- choose field winners
- preserve relationships
- preserve activity
- reconcile external mappings
- preserve old reference as alias/redirect where appropriate
- prevent cross-scope merges
- audit the merge

Organisation/Contact merge is expected first. Other record types require explicit domain rules.

## Reassignment / orphan prevention
Before deactivating a principal or archiving key records, Re:Solve should identify important responsibilities that need reassignment such as account ownership, project ownership, approvals, Vault ownership, connector stewardship and automation ownership.

This is operational responsibility management, not HR.

## API/MCP/Àríyá
Import/export operations require strong scopes. Àríyá may explain quality issues or suggest matches but should not merge large datasets without deliberate confirmation.

## Acceptance criteria
- imports provide dry-run/validation before mutation
- ambiguous duplicates require review
- exports are field/record permission-aware
- Vault secrets are excluded from generic export
- merges preserve history and mappings
- data quality can surface as actionable operational work
- no HR/timesheet subsystem is introduced
