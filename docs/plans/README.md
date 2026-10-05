# Plans

A plan records what to build and the decisions agreed with the user. Keep one file per feature: grilling records answers in it, then tickets refines the same file into the approved spec. Do not create separate notes and spec copies.

## When to write one

Create a plan when a feature or change needs grilling or ticket decomposition. Update confirmed decisions and open questions as the conversation proceeds. Small changes that need neither do not require a plan.

## How to write one

Name the file `<slug>.md`, using a short English name such as `account-recovery.md`. Use only the sections the change needs:

- Problem and Goal: the problem, who benefits, and the intended outcome.
- Decisions: confirmed behavior, constraints, scope, and module/interface contracts; keep proposals clearly separate.
- Open Questions: unresolved choices that may affect implementation.
- Verification: behavioral tests and human-checkable evidence for acceptance.
- Out of Scope: explicit exclusions.
- Tickets: stable publication keys and GitHub issue links; record each created issue immediately so publication can resume.

Preserve agreed decisions when turning the interview into a spec. Update the same file when an agreed decision changes. Link related ADRs instead of repeating their reasoning, and keep domain definitions in CONTEXT.md.

GitHub owns ticket status, dependencies, implementation results, and PR reviews. Do not duplicate those logs here. Shared rules and settings are in [AGENTS.md](../../AGENTS.md).

## Template-specific contents

[template-loop.md](template-loop.md) describes this template itself. Exclude that file when adopting the template into another project; keep this guide.
