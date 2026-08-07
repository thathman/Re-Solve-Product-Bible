# Re:Solve Lovable Build Slice Protocol

## Purpose
The Product Bible can describe the whole OS. Lovable receives only the smallest coherent current slice required to create one reviewable outcome.

This prevents broad prompts, premature schema/UI sprawl, design drift and half-built module breadth.

## Build slice definition
A slice is the smallest independently reviewable unit that completes one meaningful user flow or bounded platform capability while remaining architecturally honest.

A slice may touch multiple components/services when required to complete that outcome, but must not become a disguised module rewrite.

## Mandatory slice contents
Every slice defines:
- stable Slice ID;
- objective;
- exact Product Bible sources;
- actor/Principal and goal;
- in scope;
- explicit out of scope;
- existing foundation/Core UI to reuse;
- data/demo requirements;
- permissions/scope/negative cases;
- states;
- responsive/PWA behavior;
- accessibility;
- API/service/provenance boundaries;
- Attention/Notification/Action implications where relevant;
- Plugin/Connector implications where relevant;
- acceptance criteria;
- verification/release checks;
- stop condition/completion report.

## Global non-negotiables for every slice
- preserve canonical terminology;
- use Re:Solve Core UI Component Framework;
- shadcn/Untitled UI/Tremor sourcing rules apply;
- simple navigation/application-chrome rules apply;
- authorization is server-side, not merely hidden UI;
- source/provenance/freshness is truthful where material;
- consequential writes use Action Registry when the capability is shared/cross-interface;
- Notification and Attention are not conflated;
- provider SDKs stay behind Connector/service boundaries;
- no arbitrary Vault secret/search/cache exposure;
- no HR, payroll, leave/attendance, recruitment, employee-performance, Timesheet/Time Tracking or Client Service Consumption feature can be introduced accidentally.

## Forbidden prompt style
Do not send:
- `Build the CRM`;
- `Build Billing`;
- `Implement the Client Portal`;
- `Create full Settings`;
- `Build all Property monitoring`;
- `Create the dashboard and every module`;
- `Make the whole UI look like shadcn/Tremor` without a bounded Core UI contract.

## Preferred prompt style
Examples:
- Build Property list + Saved Views only using existing DataTable/Core UI; do not build Property Workspace.
- Build Property Workspace Overview with fictional Posture evidence only; do not execute real monitoring.
- Build Proposal rendered web view + immutable-version model only; do not implement signature/payment.
- Build Notification personal preference matrix only; do not implement channel delivery.
- Build one Cloudflare read-only Zone/Property mapping flow; do not add production DNS writes.

## Standard template

### Slice ID
Examples: `FOUND-001`, `ORG-002`, `PROP-004`, `DOC-003`.

### Objective
One sentence describing the usable result.

### Product Bible sources
List exact files/sections, not the whole Bible.

### Actor and goal
`<actor> can <measurable goal> without <current friction>`.

### In scope
Exact flow/capability.

### Out of scope
Adjacent domains/advanced behavior specifically prohibited in this slice.

### Existing foundation to reuse
List relevant:
- Core UI components;
- App shell/navigation;
- services/repositories;
- schemas/migrations;
- Action definitions;
- shared states;
- skills;
- test/demo utilities.

### Core UI / design requirements
State which canonical primitives/composites are used and whether a new reusable component must be added to Component Gallery.

Do not allow the slice to invent a second button/table/sidebar/notification/avatar pattern.

### Data requirements
Only realistic fictional subset needed by the slice. Preserve canonical demo universe names/ids.

### Permissions / negative cases
Specify Principal, capabilities, scope, denial, read-only, step-up/Approval/confirmation where applicable.

### Data/provenance
Specify authoritative record/source, connector ownership, freshness/stale behavior and conflict policy when relevant.

### States
At minimum consider:
- default;
- loading/skeleton;
- empty/first-use;
- success;
- error;
- partial/stale/unknown;
- permission denied;
- read-only/disabled;
- disconnected/provider unavailable;
- mobile;
- offline/online-only when relevant.

### Responsive/PWA
Define phone/tablet/laptop/desktop composition and cache/network safety.

### Accessibility
Keyboard/focus/semantics/touch/error-announcement requirements.

### API/service boundaries
State any new domain/service/repository/API/Action contracts. Do not scatter direct provider/Supabase operations through UI.

### Attention / Notifications / Activity / Audit
Specify only the relevant platform effects and distinguish their responsibilities.

### Automations / Plugins / Connectors
Include only when needed by the slice.

### Acceptance criteria
Observable outcomes, including negative/security/design states.

### Verification
Use `resolve-release` and relevant specialist skill(s) to inspect tests, security, responsive/PWA, accessibility, Core UI, visual polish, performance/degraded state, portability and Product Bible drift.

### Completion report
Lovable returns:
- what was built;
- meaningful files/surfaces;
- components/Core UI additions;
- data/schema/migration changes;
- dependencies;
- tests/checks and results;
- responsive/accessibility/PWA/design QA;
- provenance/security concerns;
- known limitations;
- Product Bible contradictions;
- explicit out-of-scope items left untouched.

## Slice sizing
Likely too large when it:
- creates several major record workspaces;
- combines list + many unrelated record tabs/domains;
- introduces multiple unrelated business models;
- implements more than one substantial real external Connector;
- combines foundation architecture with a business module;
- creates a large collection of future placeholder schemas/routes;
- requires a prompt mostly describing future capability rather than current user outcome.

Potentially too small when it:
- has no traversable user outcome;
- creates only decoration with no reusable foundation value;
- leaves a tightly coupled flow broken;
- intentionally ships throwaway shell/UI that will immediately be replaced.

FOUND-001 is allowed to establish several closely coupled shell/Core UI primitives because together they are one coherent application-foundation outcome.

## Build sequence policy
Prefer vertical progress:
1. shared foundation;
2. one visible flow;
3. complete states/negative cases;
4. design/security/portability review;
5. next adjacent flow.

Do not horizontally scaffold dozens of empty modules.

## Review gate
No next slice until current slice passes:
- Product Bible;
- Core UI/design/navigation;
- permission/security;
- state completeness;
- responsive/PWA;
- accessibility;
- data/provenance truthfulness;
- portability;
- test/quality expectations.

## Spec drift
If implementation reveals genuine ambiguity/contradiction:
1. stop;
2. report it;
3. update Product Bible/product decision;
4. continue only after canonical truth is clear.

## Prototype gate
Use Flow Prototype before high-impact/novel interaction such as:
- shell/mobile navigation change;
- Dashboard/Attention composition;
- complex DataTable interaction;
- multi-step onboarding/offboarding;
- Proposal/Contract acceptance;
- Vault reveal/share;
- Plugin install/update;
- Automation builder;
- Connector auth/setup;
- production DNS/registrar Action;
- complex Approval flow.

## Suggested slice prefixes
- `FOUND` foundation/Core UI/shell
- `AUTH` identity/access
- `DASH` Dashboard/Attention
- `ORG` Organisations/Clients
- `CONTACT` Contacts
- `PROP` Properties/Posture
- `MON` native Monitoring/Incidents
- `RENEW` Renewals
- `PROJ` Projects
- `REQ` Requests
- `SALE` CRM/Sales
- `DOC` Document Studio
- `BILL` Billing
- `SUP` Support
- `VAULT` Secure Vault
- `FILE` Files
- `KB` Knowledge
- `NOTIF` Notifications
- `AUTO` Automations
- `PLUGIN` Plugins
- `CONN` Connectors
- `API` API/Webhooks
- `MCP` MCP
- `ARIYA` Àríyá
- `PORTAL` Client Portal
- `SYS` System Operations
