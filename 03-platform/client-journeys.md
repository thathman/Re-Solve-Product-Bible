# Platform — Client Journeys and Onboarding Packs

## Purpose
Client Journey is a client-facing orchestration/progress layer that groups real Re:Solve actions into a coherent sequence without creating a second workflow or shadow business-record engine.

It is especially useful after Proposal acceptance, during onboarding, activation, handover, renewal and offboarding.

## Core principle
A Journey step **references authoritative records/actions**. It does not own their business truth.

Examples:
- Contract signature step -> Contract/Signature workflow;
- deposit step -> Invoice/Payment;
- project questionnaire step -> Form Request/Submission;
- brand-assets step -> File Request;
- kickoff step -> Booking/Calendar;
- client approval step -> Approval;
- internal preparation step -> Task;
- Property setup step -> Request/Task/Property action.

Completing the underlying record/action completes or advances the Journey step according to explicit mapping.

## Core records
### Journey Template
Reusable versioned orchestration blueprint.

Fields may include:
- name/type;
- Operating Entity/Brand;
- applicable Service/Proposal/Project/Client lifecycle context;
- step definitions/order/dependencies;
- client/internal visibility;
- optional/required state;
- due-date offset/defaults;
- responsible role/contact/team;
- automation/creation rules;
- current version/state.

### Client Journey
Instantiated journey linked to:
- Organisation;
- accepted Proposal/Contract/Client Service/Project as applicable;
- Template Version;
- owner;
- start/target dates;
- current state/progress;
- client-visible summary;
- underlying step references.

### Journey Step Reference
Maps one step to an underlying authoritative Task, Form Request, File Request, Approval, Contract, Invoice, Booking, Request, Project/Property action or plugin action.

## Journey types
Initial/reusable types may include:
- Client onboarding;
- Service activation;
- Project onboarding/kickoff;
- Project handover/closure;
- Renewal;
- Client offboarding;
- plugin-defined client journeys.

Do not create one hardcoded onboarding engine per service.

## Example — accepted Proposal onboarding
A client might see:

1. Proposal accepted ✅
2. Sign Contract ⬜
3. Pay 50% deposit ⬜
4. Complete website questionnaire ⬜
5. Upload logo/brand assets ⬜
6. Book kickoff call ⬜
7. Project activated ⬜

Underneath these remain Proposal, Contract, Invoice, Form Request, File Request, Booking and Project records.

## Progress
Journey progress is derived from step truth. Avoid manually editable percentage shadow state unless explicitly used only as a presentation override with Audit.

Show:
- completed/total required steps;
- current/next action;
- blocked/waiting reason;
- due/overdue step;
- client/internal responsibility;
- expected next stage.

## Dependencies / branching
Steps may support:
- ordered dependency;
- parallel availability;
- conditional inclusion;
- optional step;
- blocking requirement;
- client versus staff responsibility;
- due offsets from Proposal acceptance/Contract execution/Project start/etc.

Use shared Automation/Action/Approval primitives rather than embed a new workflow language inside Journeys.

## Portal experience
Journeys are primarily useful as a clear client progress experience.

Portal may show a calm checklist/timeline such as:
- `3 of 6 complete`;
- what the client needs to do now;
- what staff are doing;
- why a step is blocked;
- relevant document/form/file/payment action inline;
- expected next step.

Internal-only Tasks/Notes/approvals are summarized only if policy explicitly allows a client-safe status.

## Admin experience
Staff can:
- inspect current Journey;
- see underlying records;
- add/remove optional steps where policy allows;
- resend/reopen a client action;
- resolve mapping/dependency errors;
- change owner/due dates through source records or controlled Journey actions;
- instantiate from Template manually when needed.

## Template Center
Journey Templates register in the universal Template Center and preserve exact version for in-flight Journeys.

Publishing Template v3 does not silently rewrite a Journey already instantiated from v2.

## Automations
Examples:
- Proposal accepted -> invite Portal + instantiate onboarding Journey;
- Contract executed -> activate next parallel steps;
- deposit verified -> complete payment step and reveal questionnaire/kickoff;
- Form submitted -> complete questionnaire step;
- File Request fulfilled -> complete asset step;
- all blocking onboarding steps complete -> allow Service/Project activation;
- Project completed -> instantiate handover/review Journey.

All underlying actions remain idempotent and permissioned.

## Ariya
Ariya may:
- explain what is left in a Journey;
- tell staff/client why a step is blocked;
- draft reminders;
- recommend the appropriate Journey Template;
- summarize onboarding readiness;
- propose missing steps from Service/Project context;
- Watch overdue client actions.

Ariya cannot mark an underlying Contract/Invoice/Form/File/Approval complete when the authoritative record is not complete.

## Attention / Notifications / Tasks
Persistent blocked/overdue steps may generate Attention. Staff responsibility can surface in Tasks. Client actions may generate Portal/email notifications according to policy.

## Security
Journey visibility is derived from underlying record permissions and explicit client-safe step metadata. A Journey must not leak hidden internal source records through titles, counts, links or error text.

## Acceptance criteria
- Journey orchestrates rather than duplicates authoritative domains;
- progress derives from underlying step truth;
- Proposal acceptance can start onboarding idempotently;
- client sees a coherent sequence rather than scattered modules;
- Template versions are stable for in-flight Journeys;
- hidden internal work never leaks;
- Ariya can explain/Watch without fabricating completion;
- no HR/timesheet/work-timer behavior is introduced.

## Build slices
1. Journey Template + Journey/Step-reference model.
2. Proposal acceptance/onboarding integration.
3. Portal Journey experience.
4. Contract/Invoice/Form/File Request/Booking adapters.
5. renewal/handover/offboarding variants.
6. Ariya/Attention/Automation polish.
