# Re:Solve Lovable Readiness Checklist

Use this before sending FOUND-001. If a required item fails, fix setup first rather than spending build credits on avoidable rework.

## Product Bible
- [ ] Foundation/experience/core/business/platform/breadth/execution/expansion/launch-readiness Product Bible PRs are merged or the exact canonical head is otherwise agreed.
- [ ] No unresolved contradiction on Operating Entity vs Organisation, Principal/User, Files/Vault, Chatwoot, Àríyá, Monitoring, Plugin/Connector, Payment truth or permission naming.
- [ ] Explicit exclusions remain: no HR, Timesheets/Time Tracking, Client Service Consumption.

## Lovable workspace/project
- [ ] Re:Solve uses a dedicated Lovable workspace or unrelated projects have Re:Solve skills disabled.
- [ ] Fresh Re:Solve Lovable project exists.
- [ ] Project is not attempting to import the existing legacy `thathman/Re-Solve` repository.

## GitHub
- [ ] Correct GitHub installation/account is connected to Lovable.
- [ ] Lovable-created repository exists and is private.
- [ ] Two-way sync reports Connected.
- [ ] Repository/default branch name is recorded.
- [ ] Existing legacy `thathman/Re-Solve` remains unchanged.
- [ ] No repository transfer/disconnect/reconnect is planned during FOUND-001.

## Project Knowledge
- [ ] `PROJECT-KNOWLEDGE.md` has been pasted into Project settings → Knowledge.
- [ ] Saved Knowledge includes Àríyá.
- [ ] Saved Knowledge includes shadcn/ui + Untitled UI React + Tremor as mandatory major sources/influences.
- [ ] Saved Knowledge includes simple Perfex/Brevo-like navigation and rejected Odoo/Twenty patterns.
- [ ] Saved Knowledge includes native Monitoring and Uptime Kuma as optional connector only.
- [ ] Saved Knowledge includes Chatwoot/Captain separation.
- [ ] Saved Knowledge includes no HR/Timesheets/Client Service Consumption.
- [ ] Saved Knowledge includes portability/self-host requirement.

## Skills
- [ ] `resolve-feature`
- [ ] `resolve-ui`
- [ ] `resolve-shell`
- [ ] `resolve-navigation`
- [ ] `resolve-responsive`
- [ ] `resolve-accessibility`
- [ ] `resolve-design-review`
- [ ] `resolve-security-review`
- [ ] `resolve-pwa`
- [ ] `resolve-release`
- [ ] `self-host-check`
- [ ] each required skill is enabled and appears in slash menu;
- [ ] descriptions begin with `Use when...`;
- [ ] no deprecated `airix-*` skill remains active.

## FOUND-001 input
- [ ] Complete current `FOUND-001-foundation.md` is ready to paste/send.
- [ ] Required skill tags are attached.
- [ ] No extra request for Dashboard/CRM/Properties/Projects/Billing/etc. is appended.
- [ ] `AGENTS.md.template` is available to provide/create in the application repository.

## Backend/demo
- [ ] No full future schema has been pre-created.
- [ ] Any Supabase project used is development-only.
- [ ] No production keys/secrets are being used.
- [ ] Demo identities are fictional except the intentional Airix Media Operating Entity name.

## Quality expectation
- [ ] You are prepared to reject/refine a generic starter shell rather than moving on.
- [ ] Component Gallery is a required deliverable.
- [ ] Sidebar, TopBar, Avatar/Account, Notifications, Search/Command, Quick Create, Àríyá and mobile navigation are treated as foundation features.
- [ ] phone/tablet/laptop/desktop review will happen before the next slice.
- [ ] accessibility, security, PWA and portability review will happen before the next slice.

## Go / No-Go
**GO** only when every setup-critical item above is checked.

If the only unchecked items are checks that require the application to exist (for example actual test output), they belong to the FOUND-001 review rather than this preflight.