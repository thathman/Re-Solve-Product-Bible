# Install Re:Solve Skills in Lovable

## Purpose
Install the canonical source-controlled Re:Solve skills into the Lovable workspace without asking Lovable to rewrite them.

## Current Lovable mechanics
As of 2026-08-07, custom skills are workspace-level. They can be imported from a public GitHub repository/subdirectory, uploaded as ZIP/`.skill`, written manually, or created in chat. Skills imported/uploaded through Settings do not consume normal chat credits.

The canonical Product Bible repository is private. Do **not** make it public merely to simplify skill installation.

## Preferred installation for this private repository
Use **Settings → Skills → Add → Upload ZIP** for each canonical skill package exported from its folder, or use **Write manually** by copying the exact frontmatter fields and body from the canonical `SKILL.md`.

Do not use `Build with Lovable` to recreate these skills. Their contents are already authored and approved.

If we later create a dedicated public `Re-Solve-Lovable-Skills` mirror containing only non-sensitive skill packages, `Import from GitHub` becomes the preferred one-click path. The private Product Bible remains the source of truth.

## Install order
Install all skills in `manifest.md`. For the first build, verify these are enabled before FOUND-001:

1. `resolve-feature`
2. `resolve-ui`
3. `resolve-shell`
4. `resolve-navigation`
5. `resolve-responsive`
6. `resolve-accessibility`
7. `resolve-design-review`
8. `resolve-security-review`
9. `resolve-pwa`
10. `resolve-release`
11. `self-host-check`

The remaining platform/domain skills should also be installed before broad feature development.

## Verification
For each installed skill confirm:
- name exactly matches the folder/manifest;
- description starts with `Use when...`;
- content matches the canonical `SKILL.md` without summarization;
- skill is enabled for the Re:Solve project;
- no obsolete `airix-*` skill remains enabled;
- slash-menu invocation shows the expected skill;
- automatic use is enabled unless the manifest says otherwise.

## Workspace-scope warning
Lovable skills are shared across the workspace. If the workspace contains unrelated projects, either:
- use a dedicated Re:Solve Lovable workspace; or
- disable the Re:Solve skills at project level for unrelated projects.

A dedicated Re:Solve workspace is preferred during initial product build because it makes skill/knowledge governance easier.

## Canonical update flow
1. Update `SKILL.md` in the Product Bible.
2. Review/merge the Product Bible change.
3. Replace/update the corresponding Lovable workspace skill.
4. Verify its description/content.
5. Continue builds.

Never let the Lovable copy become the only version of a custom Re:Solve skill.

## Official Lovable reference
- https://docs.lovable.dev/features/skills
