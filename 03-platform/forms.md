# Platform — Forms

## Purpose
Provide a reusable form engine for intake, onboarding, requests, questionnaires, surveys and structured submissions that can feed Re:Solve workflows without coupling forms to a single module.

## Form model
Form, Version, Section, Field, Rule, Submission, Submission File, Routing Rule, Assignment, Status, Automation Reference.

## Builder
Support text, textarea, email, phone, number, currency, date/time, select, multiselect, checkbox, radio, file, URL, address, person/contact lookup, organisation lookup, property lookup, project lookup and plugin-defined field types.

Capabilities:
- sections/pages
- conditional visibility
- required/optional rules
- validation
- defaults
- helper text
- save draft where enabled
- confirmation screen
- internal/public/client-authenticated access modes
- versioning
- preview
- duplication/template creation

## Routing
A submission may:
- create/update a lead/contact
- create a client request
- create a project/task/client action
- start an approval
- notify a team
- trigger automation
- call a connector/plugin action

Support ticket/customer-support routing should use Chatwoot where that is the intended destination.

## Security
Public forms require abuse protection, rate limiting and safe file policies. Authenticated forms inherit user scope. Hidden IDs supplied by clients are never trusted for authorization.

## Notifications
Submission received, assignment created, client response required, submission failed processing, automation failed, submission approved/rejected.

## API / MCP
Forms and submissions have scoped APIs. MCP may create or retrieve submissions only for explicitly exposed forms and caller scopes.

## PWA/mobile
All end-user forms are mobile-first. Draft persistence should be resilient. Offline draft support is allowed where safe; final submission requires verified connectivity unless queued with clear status.

## Lovable build slices
1. Form list/builder shell and basic fields.
2. Conditional rules/versioning/preview.
3. Submission experience and files.
4. Routing/automations.
5. Public security, PWA drafts and plugin field extensions.