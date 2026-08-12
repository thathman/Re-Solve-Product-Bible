# Platform — Template Center

## Purpose
Template Center is Re:Solve's universal library and governance surface for reusable domain-owned templates. It gives users one place to find, preview, version, publish, archive and understand reusable patterns without collapsing those templates into one generic schema or stealing ownership from their domains.

## Principle
A Template Center entry is a **registry/library view over a domain-owned template**.

Examples:
- Proposal Template remains owned by Sales/Document Studio;
- Contract Template remains owned by Contracts/Document Studio;
- Invoice/Receipt/Statement Template remains owned by Document Studio/Billing;
- Project Template remains owned by Projects;
- Form Template remains owned by Forms;
- Email/Review Request Template remains owned by Communications;
- Automation Recipe remains owned by Automations;
- Report Template remains owned by Reports.

Template Center must not create a second shadow copy of template content.

## Supported families
Initial families may include:
- Proposal;
- Contract / SOW;
- Invoice / Receipt / Credit Note / Statement;
- Project;
- Task / recurring Task blueprint where useful;
- Form / questionnaire / survey;
- Email;
- Review Request;
- Client Journey / onboarding pack;
- Automation recipe;
- Report;
- plugin-defined templates through controlled registration.

## Template registry metadata
A registered template should expose normalized metadata such as:
- id/reference;
- template family/domain;
- name/description;
- Operating Entity / Brand scope;
- owner/team;
- draft/published/archived state;
- current version;
- default status;
- tags/category;
- last updated;
- usage count where meaningful;
- dependency/usage references;
- permissions;
- preview/test capability;
- duplicate action;
- source-domain deep link.

## Lifecycle
Suggested normalized lifecycle:
`Draft -> Published -> Archived`.

Underlying domains may have richer states, but Template Center must represent whether a template is usable for new work.

Publishing creates or points to an immutable/versioned usable revision. Editing a published template creates a new draft/version rather than silently rewriting existing generated records or in-flight workflows.

## Versioning
Historical usage must remain reproducible.

Examples:
- a Proposal generated from Template v3 remains linked to v3 after v4 is published;
- a Client Journey already started from Journey Template v2 continues under the frozen v2 plan unless a deliberate migration is performed;
- an Automation using Recipe v5 does not silently change because Recipe v6 is edited.

## Where used / dependency visibility
Before archive/delete/material change, show where a template is referenced:
- default for an Operating Entity/Brand;
- active Service Catalogue item;
- Project/Client Journey template relationship;
- Automation;
- Form Request;
- recurring process;
- system default;
- plugin/connector integration.

This uses the shared Dependency/Impact Inspector.

## Defaults and scope
Templates may be:
- system-provided;
- Workspace-wide;
- Operating Entity/Brand-specific;
- Team/private where the domain permits;
- plugin-provided.

A default template can exist per family/context, but default resolution must be explicit and inspectable.

## Preview / Test
Template Center surfaces the owning domain's test capability:
- rendered Proposal/PDF preview;
- full Email composition preview;
- test Form submission;
- Project Template expansion preview;
- Client Journey step preview;
- Automation Recipe dry run;
- Report preview.

Preview/test never bypasses the source domain's validation or security.

## Search / filters
Search by name, family, owner, tag, status, Brand/Operating Entity and last used/updated. Saved Views can provide common collections such as `Published`, `Needs Review`, `Unused`, `Airix Media`, or `Recently Changed`.

## Permissions
Template Center only exposes actions the user could perform in the source domain. It does not provide a broad `templates.admin` backdoor.

Shared permissions may exist for library/read/governance, while create/edit/publish/archive permissions remain domain-specific.

## Ariya
Ariya may:
- find the right template;
- explain where a template is used;
- recommend a Project/Form/Proposal/Journey template from authorized context;
- draft a new template/version;
- compare revisions;
- flag stale/unused/inconsistent templates.

Ariya cannot publish or replace a high-impact template without the owning domain's registered Action/Approval policy.

## Attention / Notifications
Examples:
- template dependency broken;
- default template archived;
- published template has an invalid variable/dependency;
- template review due;
- draft revision awaiting approval where configured.

## Acceptance criteria
- one library can discover templates across domains;
- source domains remain authoritative;
- historical usage remains tied to exact versions;
- archive/change shows dependencies;
- preview/test routes through the owning domain;
- permissions do not widen through Template Center;
- Ariya can recommend/explain without bypassing publish policy;
- Template Center reduces duplication rather than creating a generic-template monolith.

## Build slices
1. normalized registry/search/filter/library UI.
2. domain adapters for Documents/Projects/Forms/Communications.
3. version/default/usage/dependency display.
4. preview/test integration.
5. Automation/Journey/plugin template registration.
6. Ariya/template-governance polish.
