---
name: resolve-settings
description: Use when adding, reorganizing, or reviewing Re:Solve Settings pages, configuration schemas, defaults, permissions, diagnostics, or domain-specific administrative controls.
---

# Re:Solve Settings

Read `01-admin/settings.md`, the owning domain spec, Core UI Framework, permissions, Audit and connector/plugin rules.

## Principle
Settings is architecture made visible. It is not a miscellaneous page for controls that did not fit elsewhere.

## For every setting define
- owning domain;
- scope: workspace, Operating Entity, role/user, Organisation/Property, plugin/connector instance or system;
- default and inherited/effective value;
- data type/validation;
- required permission;
- sensitivity/classification;
- apply/save timing and side effects;
- audit requirement;
- health/diagnostic impact;
- reset/recovery behavior;
- API exposure where appropriate.

## Information architecture
Place configuration under the existing major Settings sections. Avoid adding root Settings sections for tiny features. Use tabs/section navigation with clear plain-language names.

## Forms
Use shared form patterns, unsaved-change protection for consequential edits, validation, help text and explicit test/verify actions for provider configuration.

## Connectors/plugins
Provider-specific settings belong to their instance/plugin configuration surfaces and may link from Settings. Secrets are stored/referenced through approved secret handling, not ordinary text fields.

## High-risk changes
Authentication, permissions, API/MCP credentials, payment behavior, DNS/security connectors and destructive retention settings may require confirmation, approval or step-up and must be audited.

## Responsive/accessibility
Large permission/config matrices need intentional narrow-screen alternatives. Do not make Settings desktop-only by accident.

## Completion
Verify ownership, effective values, permission-negative paths, validation, audit, recovery and that the new setting did not create duplicate configuration truth elsewhere.