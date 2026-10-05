> Historical template record. File paths and configuration roles describe the layout at the time; current rules are in [AGENTS.md](../../AGENTS.md).

# Development loop follow-up review — 2026-10-04

## 1. Scope and evidence

Reviewed the updated four skills, shared instructions/configuration, environment declarations, README, planning notes, setup guide, and evaluation procedure. The user's five operating decisions are recorded in `../../docs/plans/template-loop.md`. The initial report remains historical evidence, with a follow-up status appended.

The major earlier gaps are addressed in instructions: one default-branch PR per agent ticket, pinned PR review revisions, correction on the same PR, human merge, merge-based agent blockers, human completion evidence, persistent planning notes, GitHub-only tracking, configuration-first reading, publication recovery, and explicit verification/evidence rules. The old shared integration-branch fallback was removed because it conflicted with independently merged ticket PRs.

Four YAML frontmatters, relative Markdown links, and configured document locations passed local checks. The bundled Python validator could not start because PyYAML is absent; alternative YAML checks passed and this limitation is recorded. There is no Git history or application test suite. No independent model reviewed the changes. The user deferred the live demonstration, so empirical success remains unknown. Details are in `../evals/2026-10-04-preparation.md`.

## 2. Remaining candidates

### 1. Specify the remote lifecycle of planning documents and publication metadata

- **Files:** `.agents/skills/tickets/SKILL.md`, `docs/specs/README.md`, `docs/agents/config.md`.
- **Problem:** Tickets now correctly requires a remotely readable spec and immediate local recording of published issue IDs. It does not assign responsibility or a concrete handoff for committing/pushing planning notes, the initial spec, and subsequent publication metadata. A session opening a clean checkout can still miss newer records that only exist in another checkout. Stable issue identity reduces duplicate creation risk but does not make the newest local spec available remotely. This is a remaining interface obligation on the human.
- **Direction:** Choose and document who publishes planning documents and metadata, and what remote revision another session must use. Keep planning publication separate from the one-PR-per-implementation-ticket rule. Do not add automation until the first run shows the practical handoff.
- **Benefits:** Improves locality of publication responsibilities and makes a fresh-checkout resumption test meaningful.
- **Strength:** Worth exploring before the live run.
- **Deletion test:** The spec and publication record hide real coordination and should remain. Their incomplete remote handoff reintroduces that coordination into the next session.

### 2. Close the interval between recorded review and human merge

- **Files:** `docs/agents/config.md`, `.agents/skills/implement/SKILL.md`, `docs/setup.md`.
- **Problem:** The reviewer checks base/head immediately before posting, but the PR or default branch can change after posting and before human merge. Human merge responsibility is explicit, yet there is no concise final check that the human is merging the reviewed revision with acceptable current checks. A PR alone does not freeze either revision.
- **Direction:** Add a short human merge instruction to compare current revision and checks with the review record; require another review when revisions change. Consider repository protection only after the manual procedure is demonstrated, rather than silently assuming it exists.
- **Benefits:** Makes the review-to-merge seam explicit and keeps approval evidence tied to the actual merged change.
- **Strength:** Worth exploring before the live run.
- **Deletion test:** PR review hides real verification work. Omitting the final identity check leaks its revision assumptions into the human merge step.

## 3. Recommendation and deferred verification

Settle candidate 1 before the first fresh-checkout demonstration, then make candidate 2 part of the human merge checklist. Both are narrower than the original gaps; neither justifies adding another user-facing skill, tracker abstraction, bootstrap script, or doctor command now.

The planned eight-step evaluation is ready in `../evals/README.md`. Its eighth step now checks the body dependency fallback, because local-file tracker support was intentionally removed. Toy repository selection, distinct model IDs/effort, and human completion/merge actions belong to that deferred run. After actual execution, re-review based on failures and intervention counts instead of treating the current static checks as evidence of a complete loop.

No candidate in this follow-up has been accepted or rejected. No remote action is required to finish the user's current preparation-only scope.
