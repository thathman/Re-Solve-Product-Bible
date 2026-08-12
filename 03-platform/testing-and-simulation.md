# Platform — Test, Preview and Dry-Run Framework

## Purpose
Re:Solve must let users test consequential configuration and automation behavior before enabling it against real business data.

The framework provides a shared contract for **Preview**, **Test**, **Dry Run**, **Simulation** and safe provider diagnostics while leaving each domain authoritative for its own validation and execution rules.

## Core rule
If a feature can create external side effects, financial changes, broad data mutations or high-volume client communications, users should normally have a safe way to understand **what would happen** before enabling/executing it.

A dry run must never be presented as successful execution.

## Modes
### Preview
Render or inspect output without performing the target action.

Examples:
- Proposal/PDF preview;
- Email full-composition preview;
- Form preview;
- Project Template expansion preview;
- Client Journey preview;
- Report preview.

### Test
Perform a deliberately limited test against a test destination/context.

Examples:
- send email to test recipient;
- verify mailbox connection;
- send webhook test event;
- run Connector health check;
- render/upload test document;
- test payment-provider connectivity without creating real payment truth.

### Dry Run
Evaluate real rules against selected records without performing the declared mutations/external side effects.

Examples:
- late-fee policy against current Invoices;
- bulk Action eligibility;
- Proposal acceptance handoff;
- Automation trigger/action chain;
- Ariya email classification/routing;
- import mapping;
- archive/dependency impact.

### Simulation
Run a deterministic scenario using chosen/sample inputs and show the expected state transitions/actions.

Useful for complex Approval, Journey, Automation and commercial workflows.

## Normalized result contract
A test/dry-run result should describe where applicable:
- configuration/version being tested;
- actor/Principal and scope;
- sample/real target records;
- matched/not-matched conditions;
- proposed actions;
- skipped actions and reason;
- permission/Approval/step-up requirements;
- resulting values/calculations;
- external calls that **would** occur;
- affected record count;
- warnings/errors;
- deterministic facts versus Ariya inference;
- timestamp/correlation;
- whether any real side effect occurred.

## Side-effect guarantee
A Dry Run must not:
- mutate authoritative business records;
- send client communications;
- create/verify Payments;
- issue/sign documents;
- alter DNS/hosting/Vault/security;
- create live provider charges;
- persist fake completion.

If a provider lacks a true sandbox/test endpoint, the UI must say so rather than pretend a safe external test exists.

## Automation dry run
Given a selected trigger record/event, show:
1. trigger match;
2. conditions and evaluated values;
3. branch selection;
4. Actions that would run;
5. recipients/targets;
6. Approval/confirmation blockers;
7. idempotency key/collision warning where relevant;
8. expected records/external effects.

Users can inspect each Action before enabling the Automation.

## Ariya routing test
Users can provide a sample/selected inbound Communication and see:
- detected sender/Organisation;
- intent/category;
- Property/Project/Support/Billing matches;
- confidence;
- evidence;
- proposed registered routing Action;
- whether current policy would auto-route or send to Inbox Triage.

No real case/Task/Payment is created in Dry Run.

## Billing policy dry run
Late-fee/Adjustment policy can be previewed against current Invoices:
- eligible Invoice count;
- excluded records/reason;
- proposed fee per Invoice;
- currency-separated totals;
- caps/grace-period effect;
- Approval/waiver implications.

Do not aggregate unlike currencies into one false total.

## Proposal/Journey handoff simulation
Simulate Proposal acceptance and show whether the configured workflow would:
- invite Portal Membership;
- create Contract;
- create deposit/full Invoice;
- instantiate Project Template;
- activate Client Service/Recurring Arrangement;
- create Client Journey;
- send Communications;
- require Approval.

Idempotency behavior must be visible.

## Bulk Action preview
Before executing a broad bulk Action, show:
- selected/matched count;
- eligible count;
- denied/skipped count and reasons;
- per-risk warnings;
- expected mutations/notifications;
- records requiring individual handling.

High-impact bulk operations may require a mandatory preview before confirmation.

## Connector tests
A Connector may register safe test capabilities such as authentication, health, read-only lookup, sandbox event, webhook verification or send-test.

Testing must never store raw credentials in logs/output.

## Template Center relationship
Template Center surfaces source-domain preview/test capabilities and records which published version was tested.

## Ariya
Ariya may explain dry-run results, compare two configurations, identify risky consequences and recommend fixes. It cannot convert a dry run into execution without the normal registered Action/confirmation/Approval path.

## Audit / retention
High-risk configuration tests may retain concise Audit/diagnostic metadata. Do not retain sensitive sample content indefinitely merely because it was used in testing.

## Acceptance criteria
- preview/test/dry-run terms are not conflated with actual execution;
- dry runs have a no-side-effect contract;
- Automation/Ariya routing/Billing policies/Proposal handoffs can be inspected before enablement;
- bulk actions expose eligibility/impact before execution;
- provider sandbox limitations are truthful;
- results preserve permission/risk/idempotency context;
- no secrets leak through diagnostics;
- Ariya explains but does not bypass execution policy.

## Build slices
1. normalized test/dry-run result contract + UI pattern.
2. Automation dry run.
3. Communication/Ariya routing test.
4. Billing/Adjustment and Proposal handoff simulation.
5. bulk Action preview.
6. Connector/template integrations + Audit/degraded states.
