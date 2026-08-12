# Platform — Forms

## Purpose
Provide one reusable form engine for discovery, onboarding, Project questionnaires, Requests, quote/service enquiries, surveys, feedback, review requests and structured submissions without coupling forms to a single domain.

Forms collect structured data. They do not become a second CRM/Project/Request/Approval engine; routing creates/updates authoritative records.

## Canonical records
- **Form Template** — reusable definition;
- **Form Version** — immutable version used by historical responses;
- **Section/Page / Field / Rule** — structure and behavior;
- **Form Request / Assignment** — a specific recipient/context/deadline/expiry;
- **Submission** — submitted answers tied to an exact version;
- **Submission File** — ordinary Files linked to the response;
- **Mapping / Routing Rule** — deliberate mapping into domain records;
- **Processing State / Automation Reference**.

## Access modes
A Form may be internal staff, authenticated Client Portal, public, Secure External Access, or invitation/recipient-specific. Access mode affects identity verification, fields, abuse controls and routing—not only styling.

## Builder
Supported fields may include text/textarea, email/phone/URL, number/currency/percentage, date/time, select/multi-select, checkbox/radio/switch, file upload, address, lookup fields for authorised internal forms, approved custom fields and controlled plugin fields.

Public forms never expose unrestricted internal record lookups.

## Structure / behavior
- sections/pages;
- conditional visibility/branching;
- required/optional/read-only rules;
- typed validation;
- helper text/defaults;
- save draft where enabled;
- review/confirmation step;
- versioning;
- preview/test;
- template/duplicate;
- due date/expiry for Form Requests;
- response limits where needed;
- accessibility/error summary;
- phone-first layout.

## Core use cases
### Discovery and Proposal intake
Public/guest Forms can collect service enquiries, qualification and Discovery information and route to Lead/Opportunity/Proposal workflows with duplicate detection.

### Project questionnaire / creative brief
A Project/Opportunity can send a structured questionnaire/brief before or after Portal activation. Submission remains linked to the Project/Opportunity and can drive Tasks/Milestones only through controlled routing.

### Client onboarding
Collect approved profile, Contacts, Property inventory, Files and delivery information. Credentials/secrets use Vault-aware secure collection rather than ordinary Form fields.

### Requests and Support intake
Portal/public/secure forms may create Requests or route appropriate intake into Re:Solve Support/Chatwoot according to policy.

### File Request
A Form Request can ask a specific recipient to upload one or more Files into an authorised destination with due date/expiry.

### Survey / feedback
Forms power general surveys, Project completion feedback and service feedback. Chatwoot-originated Support CSAT remains Chatwoot truth but can be referenced.

### Review Request
A review flow may ask for private feedback first and/or present configured external review destinations such as Google, Facebook, Clutch, Trustpilot or custom URL.

A Review Request tracks related Organisation/Project/Support/Payment context, recipient, request date, reminders, clicked destination and completion only when evidence exists. Do not fabricate that a public review was posted.

### Approval / decision input
Forms may collect structured context before an Approval; the actual decision remains the Approval domain.

## Routing
A verified Submission may, through explicit rules/Automation/Action Registry:
- create/link Lead or Opportunity;
- create/update Contact/Organisation with duplicate review;
- create Request;
- create Task/Client Action;
- start onboarding step;
- create/link Project when workflow explicitly requires it;
- create Approval;
- start Proposal workflow;
- create Knowledge suggestion;
- notify/assign Team;
- trigger Automation;
- invoke an approved Connector/Plugin Action;
- route Support intake.

Routing preserves Submission provenance and resulting-record links.

## Ariya
Ariya may:
- help design field wording/conditional logic;
- summarize a permitted Submission;
- extract requirements, deadlines, entities and risks;
- compare responses where authorised;
- propose Project Tasks/Milestones/Service items;
- draft personalised review requests;
- classify/reroute ambiguous intake.

Ariya output is not a bypass around validation, duplicate review, approval or permissions.

## Identity / duplicate handling
Public Lead/Contact intake uses multiple matching signals and may create Data Quality review rather than silently merge. Browser-supplied hidden Organisation/Property/User IDs never grant authority.

## Files / Vault
Ordinary attachments use Files. Raw passwords, tokens, SSH/API credentials and protected documents require Vault-aware secure collection.

## Public / Secure External security
Controls may include rate limiting, bot/spam protection, CSRF/session protection, file type/size/scan policy, signed/expiring access, email/OTP verification, minimal exposure and replay/idempotency controls.

## Submission lifecycle
Suggested: Draft -> Submitted -> Processing -> Needs Review -> Routed -> Completed, with Failed/Archived where applicable.

Processing failure must never claim the destination record/action succeeded.

## Notifications / Attention
Events may include Form Request sent/due/overdue, response received, review needed, routing failed, client clarification needed and completed. Persistent triage/processing problems create Attention rather than reminder spam.

## PWA/mobile
End-user forms are mobile-first. Sensitive/private answers follow explicit cache policy. Final submission requires verified processing and truthful pending/sync state.

## Privacy / retention
Each Form declares purpose, sensitivity, retention and appropriate privacy notice. Historical submissions remain tied to the exact Form Version.

## Acceptance criteria
- Forms are reusable across domains;
- Form Request is distinct from reusable Template and immutable Submission;
- Project questionnaires/surveys/onboarding/reviews reuse one engine;
- routing preserves provenance;
- public IDs never confer authorization;
- duplicate identity handling is deliberate;
- ordinary Forms cannot casually collect Vault secrets;
- Ariya suggestions remain controlled proposals/actions;
- mobile/accessibility are first-class;
- no HR/employee forms are introduced as core capability.

## Build slices
1. Template list/builder + canonical fields.
2. conditional logic/versioning/preview.
3. Form Request/assignment + Submission experience + Files.
4. Discovery/Project/Request routing + provenance.
5. surveys/feedback/review requests.
6. Secure External/Public security + abuse controls.
7. Ariya summaries/mapping suggestions + PWA polish.
