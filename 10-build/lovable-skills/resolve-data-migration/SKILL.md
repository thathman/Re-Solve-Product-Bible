---
name: resolve-data-migration
description: Use when implementing or reviewing Re:Solve imports, exports, legacy migrations, field mapping, deduplication, record merge, reassignment, data-quality correction, or schema/data migrations that affect durable business records.
---

# Re:Solve Data Migration

Read `03-platform/import-export-and-data-quality.md`, data provenance/sync, record lifecycle/reference numbering, domain model, permissions and the affected domain specs.

## Import/migration flow
1. Identify source and authority.
2. Map source fields/entities to canonical Re:Solve concepts.
3. Validate types/required fields/relationships.
4. Detect likely duplicates and conflicts.
5. Run dry-run/preview with counts and errors.
6. Require explicit confirmation for material imports.
7. Execute as observable background work when large.
8. Reconcile results and preserve import/migration history.

## Identity
Do not use email alone as canonical Contact identity. Preserve external ids/mappings separately. Never collapse Operating Entity, Organisation, Contact, Property or other canonical concepts just because legacy data was flatter.

## Provenance
Imported values record source/batch and authority/freshness where material. Do not overwrite an authoritative Re:Solve value silently.

## Dedup/merge
Show preview of surviving values, relationships, activity, mappings and references. Preserve redirects/aliases where needed. Merge must not erase audit/legal history.

## Reassignment
When deactivating/replacing an owner, identify affected records/approvals/automations/Vault ownership and offer controlled reassignment rather than orphaning responsibilities.

## Schema migrations
Version migrations, make rollback/recovery strategy explicit, and never edit production-shaped data manually merely because the development dataset is small.

## Exports
Permission-filtered, auditable when sensitive, and exclude Vault secrets by default. Large exports are background jobs with expiring delivery where appropriate.

## Completion
Verify dry-run, invalid rows, duplicate handling, idempotent/retry behavior, rollback/reconciliation, permission scope, source history and deterministic demo reset where development fixtures are involved.