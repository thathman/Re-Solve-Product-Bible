# Re:Solve Lovable Supervisor Protocol

## Purpose
ChatGPT acts as the build supervisor for Re:Solve. Lovable is the implementation environment. The Product Bible remains canonical product truth.

The supervisor decides the next bounded step, prepares the exact prompt, reviews Lovable's completion report and implementation evidence, and only then authorizes the next step.

## Operating model
1. User brings the latest Lovable result/completion report, screenshots, errors or repository state back to ChatGPT.
2. ChatGPT reviews the result against the current Product Bible, Build State and prior accepted slices.
3. ChatGPT gives the user the next concise Lovable prompt.
4. User sends that prompt to Lovable.
5. Lovable performs only the requested bounded step, using Project Knowledge, installed Re:Solve skills and exact cited Product Bible files when needed.
6. Lovable stops and returns a structured completion report.
7. ChatGPT reviews before any further build step.

Do not ask the user to invent the next Lovable instruction, select product scope, or decide which Re:Solve skills apply unless a genuine owner decision is required.

## Prompt philosophy
Supervisor prompts should be short and operational. They should not repeat the Product Bible or restate entire PRDs.

A normal prompt should contain only:
- step/slice ID;
- exact next objective;
- exact Product Bible file(s) or public URL(s) to consult if needed;
- required skill tags when automatic selection should not be trusted;
- scope boundary / one or two explicit non-goals when necessary;
- requested verification/completion report;
- stop condition.

The implementation detail belongs in Project Knowledge, Skills and canonical Product Bible files.

## Prompt delivery format
Every user-facing Lovable prompt from the supervisor must be delivered as **one self-contained fenced code block** with no explanatory prose inside the block before or after the actual instruction. This gives the user a reliable built-in Copy button and prevents accidental omission of lines.

Any supervisor commentary, review verdict or explanation should appear outside the code block.

## Umbrella slices and substeps
Large acceptance specifications such as `FOUND-001` are **umbrella review contracts**, not a requirement to send one giant implementation prompt.

The supervisor should normally decompose an umbrella slice into small implementation steps, for example:
- `FOUND-001A` stack/repository preflight;
- `FOUND-001B` UI stack and token foundation;
- `FOUND-001C` Core UI primitives/Component Gallery;
- `FOUND-001D` Admin shell/chrome;
- `FOUND-001E` Portal shell;
- `FOUND-001F` identity/permission foundation;
- `FOUND-001G` PWA/accessibility/CI/engineering hardening;
- `FOUND-001R` integrated review/correction gate.

The umbrella specification remains the final acceptance source. A substep may not widen scope beyond it.

## Standard prompt shape
```text
STEP <ID> — <short title>

Continue Re:Solve from the current accepted build state.

Use <skills> and consult only these canonical Product Bible files if needed:
- <path/url>

Objective: <one bounded outcome>.

Do not expand into adjacent Product Bible features.

Before changing code, inspect the current implementation and preserve accepted architecture/Core UI patterns.

When complete, run the relevant checks, report files/dependencies/migrations changed, tests/results, any Product Bible conflict, and then STOP.
```

## Review rule
No next slice is issued merely because Lovable says `done`.

The supervisor may request:
- screenshots;
- browser/device checks;
- exact build/test output;
- repository diff/commit inspection;
- focused correction prompt;
- Product Bible clarification;
- PASS / CONDITIONAL / FAIL review.

## Skill use
Let Lovable apply skills automatically when the trigger is unambiguous. Explicitly invoke critical review/build skills when consistency matters or the current step has a high-risk boundary.

Do not attach every skill to every prompt merely because all canonical skills are installed. Select only the skills relevant to the current bounded step.

Workspace skills are canonical runtime instructions. Project-local `.agents/skills/` copies created during bootstrap are temporary only and should be removed once the corresponding workspace skills are verified, to prevent duplicate/drifting instruction sources.

## Product Bible references
Because `thathman/Re-Solve-Product-Bible` is public, supervisor prompts may point Lovable directly to exact canonical files.

Do not tell Lovable to broadly browse the entire Product Bible and decide what to build next. The supervisor controls sequencing.

## Scope discipline
Only the currently authorized step may be implemented. Future Product Bible content is context, not permission.

The user may change product direction at any time. When that happens, update Product Bible truth before allowing implementation to establish the new behavior where the decision is architecture/product-significant.

## Human approvals
The supervisor must stop and ask the user only when a true owner decision is needed, such as:
- repository rename/archive/destructive operation;
- workspace-level settings actions Lovable cannot perform from project chat;
- paid/proprietary UI asset/license choice;
- irreversible data migration;
- production credential/provider action;
- major product-direction conflict;
- legal/compliance policy requiring owner input.

## Build State
After each accepted slice, update `10-build/lovable-launch/BUILD-STATE.md` with the real implementation state before drafting the next slice.
