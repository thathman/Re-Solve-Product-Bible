# Install Re:Solve Skills in Lovable

## Purpose
Install the canonical source-controlled Re:Solve skills into the Lovable workspace without asking Lovable to rewrite them.

## Current Lovable mechanics
As of 2026-08-07, custom skills are workspace-level. They can be imported from a public GitHub repository/subdirectory, uploaded as ZIP/`.skill`, written manually, or created in chat. Skills imported/uploaded through Settings do not consume normal chat credits.

The canonical Product Bible repository is public:

`https://github.com/thathman/Re-Solve-Product-Bible`

This makes **Import from GitHub** the preferred installation path.

## Preferred installation — Import from GitHub
In Lovable, go to **Settings → Skills → Add → Import from GitHub**.

Because this repository contains multiple skills, import each skill by its public subdirectory URL:

`https://github.com/thathman/Re-Solve-Product-Bible/tree/main/10-build/lovable-skills/<skill-name>`

Example:

`https://github.com/thathman/Re-Solve-Product-Bible/tree/main/10-build/lovable-skills/resolve-feature`

For a copy/paste list of every canonical skill URL, use:

`10-build/lovable-skills/GITHUB-IMPORT-URLS.md`

Lovable also accepts a direct public `SKILL.md` URL and imports its parent folder.

Do not point Lovable at the repository root because the repository contains many Product Bible files and multiple skills rather than one root-level `SKILL.md`.

Do not use `Build with Lovable` to recreate these skills. Their contents are already authored and approved.

## Fallback installation
If GitHub import is temporarily unavailable, use **Upload ZIP/`.skill`** or **Write manually** by copying the exact canonical `SKILL.md`.

The Product Bible remains the source of truth regardless of installation method.

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
3. Re-import or update the corresponding Lovable workspace skill.
4. Verify its description/content.
5. Continue builds.

Never let the Lovable copy become the only version of a custom Re:Solve skill.

## Official Lovable reference
- https://docs.lovable.dev/features/skills
