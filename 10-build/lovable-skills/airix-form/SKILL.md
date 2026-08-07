---
name: airix-form
description: Build or refine Re:Solve create, edit, intake, configuration, and settings forms with complete validation, state, accessibility, and responsive behavior.
---

# Airix Form

Read the relevant Product Bible feature spec before implementing.

For every form define:
- field order
- labels and help text
- required/optional state
- defaults
- validation and async validation
- sensitive-field treatment
- permission-sensitive fields
- disabled/read-only state
- unsaved changes behavior
- server error mapping
- success confirmation
- destructive actions
- mobile layout
- keyboard/focus order

Use mature accessible primitives and existing Re:Solve form patterns. Do not invent inconsistent controls.

Sensitive values must not be casually prefilled, logged, cached, or exposed.

Before completion test happy path, invalid input, server failure, permission denial, mobile layout, and keyboard navigation.
