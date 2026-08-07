# SETUP-000 — Lovable Bootstrap

Use this as the first substantive message in the fresh Re:Solve Lovable project before FOUND-001.

```text
SETUP-000 — Bootstrap the Re:Solve Lovable workspace/project for supervised development.

Canonical Product Bible:
https://github.com/thathman/Re-Solve-Product-Bible

Do not build product features yet.

1. Confirm the current project/workspace context and whether this session has workspace-owner/admin permission to create/import workspace skills.
2. Load/save the canonical Project Knowledge from:
https://github.com/thathman/Re-Solve-Product-Bible/blob/main/10-build/lovable-launch/PROJECT-KNOWLEDGE.md

3. Install/import canonical Re:Solve workspace skills yourself from the public GitHub subdirectory URLs listed in:
https://github.com/thathman/Re-Solve-Product-Bible/blob/main/10-build/lovable-skills/GITHUB-IMPORT-URLS.md

Preserve each skill exactly; do not rewrite or regenerate it. Keep Automatic use enabled unless the manifest says otherwise.

For FOUND-001, only these skills are required immediately:
resolve-feature, resolve-ui, resolve-shell, resolve-navigation, resolve-responsive, resolve-accessibility, resolve-design-review, resolve-security-review, resolve-pwa, resolve-release, self-host-check.

The remaining canonical skills may be installed later just-in-time under supervisor direction before the first slice that needs them. Do not make the user perform all future skill imports merely to pass bootstrap.

If importing an existing GitHub skill is restricted to a Settings/owner UI action that you cannot perform from this chat, do not recreate the workspace skill. Tell me exactly which one-time UI action is required and which imports remain incomplete.

If you create or stage project-local copies under `.agents/skills/` as a bootstrap workaround, label them temporary. They are not a substitute for the canonical workspace skills and must be removed after the corresponding workspace skills are verified, so duplicate/drifting skill copies do not remain in the application repository.

4. Verify there are no obsolete `airix-*` skills active.
5. Do not initialize the full database or install the UI stack yet.
6. Do not execute FOUND-001 yet.

Return only a setup report containing:
- Project Knowledge: installed/not installed;
- skill import capability from this session;
- required FOUND-001 workspace skills successfully installed;
- skills requiring owner/UI action, if any;
- temporary `.agents/skills/` drafts created, if any;
- obsolete skills found;
- blockers;
- readiness for FOUND-001.

Then STOP.
```

## Observed Lovable behavior
During the initial Re:Solve bootstrap, Lovable could fetch the public Knowledge/skill files and stage project-local `.agents/skills/` drafts, but the active workspace-level import and Project Knowledge save remained owner/UI actions. Treat that as a valid bootstrap outcome: complete the minimal owner actions, verify them, clean up duplicate drafts, then continue under the supervisor protocol.
