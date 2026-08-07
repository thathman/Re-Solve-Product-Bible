# Platform — Forms

## Purpose
Provide one reusable form engine for intake, onboarding, Requests, quote/service enquiries, questionnaires, surveys and structured submissions without coupling forms to a single domain.

Forms collect structured data. They do not become a second CRM/Request/Approval engine; routing creates/updates authoritative domain records.

## Core records
Form, Form Version, Section/Page, Field, Rule, Submission, Submission File, Routing Rule, Assignment/Processing State and Automation Reference.

## Access modes
A Form may be:
- internal staff;
- authenticated Client Portal;
- public;
- Secure External Access only;
- invitation/recipient-specific where needed.

The mode affects identity verification, allowed fields, abuse controls and routing—not merely page styling.

## Builder
Supported field types may include:
- text / textarea / rich long-answer where justified;
- email / phone / URL;
- number / currency / percentage;
- date/time;
- single/multi select;
- checkbox/radio/switch;
- file upload;
- address;
- Contact/Organisation/Property/Project lookup for authorized internal forms;
- approved custom fields;
- plugin-defined fields through controlled registration.

Public forms should not expose unrestricted internal record lookup components.

## Structure / behavior
- sections/pages;
- conditional visibility;
- required/optional/read-only rules;
- typed validation;
- helper text;
- defaults;
- save draft where enabled;
- confirmation/review step;
- versioning;
- preview/test;
- template/duplicate;
- accessibility/error summary;
- phone-first layout.

Use the canonical Re:Solve Form components and Custom Fields contract rather than one-off controls.

## Use cases
### Lead / quote intake
Public/guest form can create a Lead or Request such as `Request a Quote`, subject to duplicate detection and explicit routing.

### Client Request
Portal/public/secure form can create a Request with Organisation/Property context resolved server-side.

### Client onboarding
Collect business/profile, Property inventory, Contacts, files and other onboarding inputs. Credential/secrets collection must route to Secure Vault-specific secure flows rather than ordinary form fields when appropriate.

### File request
Collect one or more Files into an explicitly authorized destination.

### Feedback / Survey
Forms can power project/service feedback and surveys. Chatwoot remains owner of support CSAT originating in Chatwoot.

### Approval / decision input
Forms may collect structured information before an Approval, but actual decision state remains the Approval domain.

## Routing
A verified Submission may, through explicit rules/Automation/Action Registry:
- create/link Lead;
- create/update Contact/Organisation with duplicate review;
- create Request;
- create Task/Client Action;
- start onboarding step;
- create Project only when the business workflow explicitly calls for it;
- create Approval;
- create Opportunity/Estimate path;
- create Knowledge suggestion;
- notify/assign Team;
- trigger Automation;
- invoke approved plugin/Connector Action;
- route appropriate support intake into Chatwoot.

Routing preserves Submission provenance and link to resulting records.

## Mapping to custom fields
A Form may map fields to approved core/custom fields with type compatibility and explicit permissions. Do not use forms to inject arbitrary unknown JSON fields.

## Duplicate / identity handling
Public Lead/Contact intake uses multiple matching signals and may create a Data Quality review rather than silently merging.

Hidden Organisation/Property/User IDs supplied by a browser are never trusted as authorization. Authenticated context is resolved server-side.

## Files / Vault
Ordinary attachments use Files and upload/scan policy.

Do not use a standard Form field to collect raw passwords/API keys/SSH secrets into ordinary Submission storage. Protected credential/confidential input requires a Vault-aware secure collection flow.

## Public / Secure External security
Controls may include:
- rate limiting;
- spam/bot protection;
- CSRF/session protections appropriate to stack;
- file type/size/scan policy;
- signed/expiring Secure External Access;
- email/OTP verification for higher-risk flows;
- minimal data exposure;
- submission replay/idempotency controls.

## Submission lifecycle
Suggested:
- DRAFT where supported
- SUBMITTED
- PROCESSING
- NEEDS_REVIEW
- ROUTED
- FAILED
- COMPLETED
- ARCHIVED

Submission processing failure must not falsely claim the resulting domain record was created.

## Notifications / Attention
Events may include received, assigned, review needed, processing failed, client clarification needed or completed.

A persistent processing/triage issue may create Attention rather than repeated Notifications.

## Collaboration
Internal reviewers may Comment/Mention on a Submission/Request according to visibility rules. Client-visible clarification should usually occur through the resulting Request/Portal flow.

## API / MCP / Àríyá
Forms/Submissions use scoped APIs.

MCP may list exposed Forms, create authorized Submissions or inspect permitted Submission status—not arbitrary public-form data.

Àríyá may help staff design field wording/routing or summarize permitted Submissions, but cannot bypass validation or public-access policy.

## PWA/mobile
End-user forms are mobile-first. Draft persistence can be resilient/offline only for non-sensitive data under explicit cache policy. Final submission requires verified processing; queued submission must show pending/sync outcome truthfully.

## Privacy / retention
Each Form declares purpose, data sensitivity, retention and client/public privacy notice where needed. Closed/obsolete Form versions remain traceable to historical Submissions.

## Acceptance criteria
- Forms remain reusable across domains;
- routing preserves Submission provenance;
- Requests/onboarding/quote/survey flows reuse the engine;
- public hidden IDs never confer authorization;
- duplicate identity handling is deliberate;
- ordinary forms cannot leak/store Vault secrets casually;
- custom field mappings are typed;
- mobile/accessibility are first-class;
- no HR/employee forms are introduced as core product capability.

## Lovable build slices
1. Form list/builder + canonical fields.
2. conditional rules/versioning/preview.
3. Submission experience + ordinary Files.
4. Request/Lead/onboarding routing + provenance.
5. Secure External/Public security + abuse controls.
6. survey/custom-field/plugin extensions + PWA draft polish.
