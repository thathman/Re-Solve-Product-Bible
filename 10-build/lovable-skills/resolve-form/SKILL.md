---
name: resolve-form
description: Use when building or refining a Re:Solve create, edit, intake, configuration, settings, onboarding, request, or other form that needs canonical fields, validation, permissions, responsive behavior, and accessible error handling.
---

# Re:Solve Form

Before building, derive fields/states from the relevant Product Bible spec and Custom Fields contract.

Verify:
- labels/help/defaults;
- required and conditional behavior;
- client/server schema validation;
- async validation when needed;
- sensitive field treatment;
- permission/read-only behavior;
- unsaved-change protection where material;
- server error summary and field errors;
- saving/success state;
- keyboard/focus/error announcements;
- phone/tablet/desktop composition;
- destructive actions separated from ordinary save;
- no arbitrary custom JSON field handling when a typed field exists.

Prefer React Hook Form + Zod or Lovable's strongest compatible equivalent.
