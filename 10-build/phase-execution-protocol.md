# Re:Solve Phase Execution and Checkpoint Protocol

## Purpose
Define how the broad Product Bible is converted into build phases and how progress is reported to the owner.

This protocol is mandatory for all implementation agents. It exists so a broad roadmap never hides dozens of unfinished product obligations behind a single “Step complete” label.

## Core rule
**Before a phase starts, the complete phase expansion must be created and shown to the owner.**

No phase begins from a broad name such as `Work & Service Operations` alone. It begins from a numbered atomic task ledger that covers the entire phase scope, dependencies, acceptance and release obligations.

## Phase definition
Every phase declares:
- phase number/name;
- stable task prefix;
- purpose/goal;
- product domains/capabilities covered;
- dependencies/prerequisites;
- explicit out of scope;
- migration/data-risk notes;
- external Connector/provider dependencies;
- browser/UX acceptance plan;
- release/closure gate.

## Atomic ledger
Each phase receives a stable numbered ledger before implementation, for example:

```text
WSO-001
WSO-002
WSO-003
...
```

Tasks should be small enough that completion can be evidenced and large enough to represent a real bounded obligation.

A phase ledger should explicitly cover where relevant:
- entry audit/current production truth;
- domain/data model;
- lifecycle/state transitions;
- permissions/RLS/tenant boundaries;
- server-authoritative mutations;
- Admin UX;
- Client Portal/Secure External UX;
- Tasks/Attention/Notifications/Activity/Audit;
- Ariya tools/context/actions;
- Forms/Documents/Communications/Monitoring relationships;
- Automations/Action Registry;
- mobile/responsive/accessibility;
- tests/negative cases;
- migrations/rollback acceptance;
- CI/build/PWA;
- exact-SHA deployment/health;
- Product Bible/oversight reconciliation;
- final phase browser/experience acceptance.

## Owner-visible phase expansion
Immediately before phase implementation, report the entire expanded ledger grouped into logical sections.

The owner must be able to see:
- every task planned for the phase;
- why it belongs there;
- what is deliberately deferred;
- which cross-domain/Product Oversight items were absorbed;
- the phase completion definition.

Do not ask “shall I continue?” when the roadmap is already clear; show the expansion and proceed according to the owner's operating rules unless they redirect.

## Canonical status symbols
Use consistently in owner-facing checklists:
- ✅ **Complete** — implementation/evidence complete for the stated scope;
- 🟡 **Active** — currently being executed or in release closure;
- ⬜ **Pending** — not yet complete;
- ⏭️ **Deliberately deferred** — assigned to a later dependency/phase with reason;
- 🟦 **Phase-final/browser gate** — deliberately reserved for the agreed consolidated browser/experience acceptance where applicable.

Never use ✅ for a task whose acceptance evidence is still missing unless the task text itself explicitly says engineering-only and the browser portion is represented separately.

## Completion/checkpoint report
Every meaningful completion checkpoint reports:
1. current phase, section and exact active task;
2. exact version/SHA/branch/PR/deployment state where applicable;
3. tasks completed since the previous checkpoint;
4. **the full current phase ledger with status for every task, including all pending tasks**;
5. newly discovered product gaps/oversights and where they are assigned;
6. deliberately deferred items and reason/dependency;
7. migrations/database acceptance and rollback state where relevant;
8. tests/lint/typecheck/build/PWA/CI state;
9. exact-SHA production/OpenShip health where relevant;
10. browser/UX acceptance state;
11. next atomic task being executed.

A short prose summary can precede the ledger but never replace it.

## Do not collapse phases into broad Steps
Broad roadmap labels are useful for orientation only. Reporting `Step 9 — Projects` is not a sufficient task list when the actual phase contains dozens of lifecycle/security/Portal/Ariya/Document/Automation obligations.

When asked for status, show the phase hierarchy and the expanded active-phase ledger rather than only a 20–30 item master roadmap.

## Phase closure
A phase closes only when:
- all blocking atomic tasks have evidence;
- deferred items have explicit non-blocking reason and later owner/dependency;
- cross-domain/tenant/security tests pass;
- migration/rollback evidence is recorded where applicable;
- canonical CI/build passes on the release candidate;
- exact tested SHA is promoted where the phase includes production release;
- public/internal health checks pass;
- Product Bible and Product Oversight Register are reconciled;
- phase-final browser/experience gate is complete where required.

`Engineering complete` and `browser/experience closed` are distinct states when browser work is intentionally consolidated.

## Browser acceptance
When the owner chooses consolidated browser testing:
- do not block each internal engineering slice on repetitive browser passes;
- preserve explicit browser-deferred tasks;
- after all engineering sections of the phase are ready, provide one comprehensive browser/ChatGPT Work acceptance script;
- test Admin and Portal, desktop/mobile, real workflows/security/visibility;
- fix defects, rerun checks and redeploy exact tested SHA;
- only then mark browser-dependent tasks/phase closed.

Never claim browser pass without evidence.

## Product-gap discovery
During every phase, new cross-cutting capabilities are recorded immediately in the Product Oversight Register or canonical Bible decision. Discovery does not mean impulsive implementation.

At phase entry and closure:
- review unresolved oversight items;
- absorb those whose dependency is now real;
- explicitly assign later items;
- ensure no new feature silently falls between phases.

## Relationship to build slices
A phase can contain many small reviewable build slices. The phase ledger is the owner-visible completeness contract; a build slice is the implementation unit.

`10-build/build-slice-protocol.md` governs each slice. This file governs the phase that contains those slices.

## Product freeze/replanning
When the owner explicitly pauses implementation to revise the Product Bible/roadmap, implementation remains frozen until:
1. new product decisions are canonicalized;
2. contradictions are reconciled;
3. remaining phases are re-expanded from the revised Bible;
4. the next phase expansion is shown before work resumes.

## Acceptance criteria
- every future phase has an owner-visible atomic expansion before start;
- every checkpoint shows all current-phase pending tasks;
- broad Steps never substitute for the phase ledger;
- engineering/browser states are not conflated;
- new product gaps are captured and assigned;
- exact release evidence remains visible;
- next phase cannot silently begin without its expansion.
