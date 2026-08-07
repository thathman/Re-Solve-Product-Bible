# Re:Solve GitHub Transition for Lovable

## Why this transition exists
Current Lovable Git sync creates a new GitHub repository when a project is connected and does not import an existing GitHub repository into Lovable.

The current private `thathman/Re-Solve` repository therefore cannot simply become the starting Lovable project repository.

## Source roles during FOUND-001
### `thathman/Re-Solve-Product-Bible`
Canonical product/specification truth.

### current `thathman/Re-Solve`
Legacy application/reference repository. Preserve it unchanged during initial Lovable setup so historical behavior/code remains available for audits and controlled later migration.

### Lovable-created repository
Fresh private repository automatically connected to the Re:Solve Lovable project. This is where FOUND-001 and all new Lovable implementation work begins.

Suggested temporary names if Lovable exposes naming choice:
- `Re-Solve-Lovable`
- `Re-Solve-Next`

Do not transfer or disconnect this repository casually. Current Lovable documentation says reconnecting creates a new repository.

## FOUND-001 rule
Do not copy the entire legacy codebase into the new repository. FOUND-001 builds the new architecture and Core UI foundation from the canonical Product Bible/Knowledge/skills.

Specific legacy behavior may later be migrated deliberately in feature slices after review.

## Transition gate
Do not change repository names until all are true:
- FOUND-001 passes the canonical review checklist;
- new Lovable repository is syncing correctly;
- Core UI/shell architecture is accepted;
- exported source is considered the forward application baseline;
- Product Bible stack is merged;
- owner explicitly approves the repository-name transition.

## Recommended one-time transition after approval
1. Confirm both repositories are clean and backed by GitHub history.
2. Record the legacy repository's final default-branch commit in the transition note/issue.
3. Rename current `thathman/Re-Solve` to an archival/reference name such as `Re-Solve-Legacy`.
4. Keep it private and clearly mark its README/description as legacy/reference; do not delete it.
5. Rename the Lovable-created synced repository to `Re-Solve`.
6. Verify Lovable Git sync continues after the repository rename.
7. Verify the new canonical repository's default branch, clone URL, CI and external references.
8. Update Product Bible/engineering docs that refer to the transitional repository name.
9. Do not transfer the Lovable repository to another owner/org as part of this rename; repository transfer can break the connection.

Current Lovable documentation states that renaming the repository itself is safe and the connection tracks the rename.

## Alternative
If we decide the old `Re-Solve` name/history must remain permanently untouched, keep the Lovable-created repository under a new canonical name instead and update Product Bible references. Do not merge two unrelated Git histories merely to preserve a name.

## What not to do
- do not delete the legacy repository;
- do not force-push the Lovable-generated history over the legacy history;
- do not copy `.git` history between them;
- do not disconnect/reconnect Lovable merely to obtain a preferred repository name;
- do not rename the GitHub user/organization as part of this transition;
- do not transfer the connected repository without reviewing current Lovable guidance.

## Official current reference
https://docs.lovable.dev/integrations/github
