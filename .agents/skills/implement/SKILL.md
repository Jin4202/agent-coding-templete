---
name: implement
description: Implement one ready ticket in a fresh context with test-driven development, then hand it off for review. Also performs the review when asked to review a ticket. Use only when the user explicitly asks to implement or review a ticket.
---

# Implement

This skill has two modes. Implement mode is the default. Review mode applies when the user asks to review a ticket.

Spell out each step below. Do not skip a step because it seems implied.

In either mode, read `AGENTS.md` first. Resolve labels and document locations through its settings and follow its shared workflow contract. GitHub Issues is the only tracker. Read Shared instructions before acting.

## Implement mode

### 1. Pick the ticket

Use the ticket number the user gave. Otherwise list open Agent eligibility issues in Repository and ask which frontier ticket to take. Never implement a Human prerequisite issue. Check every blocker using the shared dependency contract: agent blockers need a merged PR; human blockers need human completion evidence and closure. A closed or cancelled issue alone does not prove an agent dependency is satisfied.

### 2. Read

Read the ticket, its linked plan, Domain glossary, and relevant Decision records. Use glossary vocabulary in code. Read the existing PR and its reviews if this is a correction session.

### 3. Check prerequisites

Check required variables at their application read locations in Environment declarations, rather than assuming shell exports. Inspect existence only, never values or secret-bearing command output. Check non-variable human prerequisites too. If something is missing, search existing Human prerequisite issues, reuse a matching one or create one, and add it as a blocker of this ticket using the dependency contract. Stop dependent work and tell the user the exact human action and evidence needed. Never fabricate a value. If the tracker cannot be used, preserve the unpublished draft and report the blocker.

### 4. Work on the right branch

Check the checkout, remote repository, default branch, and working tree. Do not include, discard, or overwrite unrelated changes; if they prevent isolation, stop and request an isolated checkout. For a new ticket, create a branch from the latest default branch with merged prerequisites available. Look for an existing PR for this ticket before creating another. For corrections, resume that PR's branch and keep the same PR. Parallel tickets need separate worktrees; stay in your assigned checkout.

Run every filled verification command from Shared instructions before edits, including lint, and record commands, exit status, and existing failures. Report empty or placeholder commands as skipped. Do not repair unrelated baseline failures.

### 5. Build with TDD

For executable behavior, write one failing test, confirm it fails for the intended reason, make it pass, then clean up. Test public behavior at the plan's seams. Mock only real external boundaries such as the database, an outside API, time or filesystem, never owned code. For non-code criteria, collect the plan's human-checkable evidence instead of inventing tests. A correction session addresses review Blockers on the same PR and records each resolution.

### 6. Check often

Run filled typecheck and relevant single-test commands during TDD. Run every filled verification command, including lint and the full suite, at the end. Follow the shared verification contract for missing commands and baseline failures. Fix failures caused by the ticket; leave unrelated failures recorded and never imply unverified behavior passed. Never weaken, skip or delete tests to make them pass.

### 7. Stay in scope

Do only what the ticket delivers. When you find an unrelated problem or a missing prerequisite, write it as a comment on the ticket or as a new ticket, and leave it unfixed.

### 8. Commit and report

Commit with `Refs #N`, push the ticket branch, and open or update its single PR targeting Repository's default branch. Put `Closes #N` in the PR body. Explain the delivered behavior, baseline and final verification results, skipped checks, non-code evidence, unresolved issues, and any review corrections. Link the PR from the ticket. Do not close the issue, merge the PR, or enable automatic merge.

### 9. Hand off for review

Hand off the PR URL and head SHA for review by a different model in a separate session. Blockers require a fresh implementation session on this PR and another review of the new revision. Once the current revision has no Blockers and required evidence is verified, hand it to the human for merge. After merge, verify the issue closed and dependent work includes the merged change; report closure failures rather than treating issue state as merge evidence.

## Review mode

Do not change any code in this mode.

1. Read the PR, linked ticket/plan, Domain glossary, and relevant Decision records. Verify one ticket per PR, the default-branch target, and `Closes #N`. Record the PR's current base and head SHAs; inspect the diff and checkout for those revisions. Commit-message search is not the comparison boundary. Confirm this is a different model from the implementer; otherwise hand off without claiming independent review.
2. Run every filled verification command yourself, including lint. Inspect non-code evidence and baseline failures. Report skipped commands and anything you could not verify; do not rely on the implementer's report.
3. Do two passes and keep their notes separate. If you can run them as independent workers, do so. Otherwise run them one after the other.
   - The standards pass checks Shared instructions, glossary vocabulary, ADRs, and test quality. Look for mocks of owned code, brittle assertions, needless complexity, and secrets without reproducing their values.
   - The spec pass checks every acceptance criterion with test evidence for code behavior or human-checkable evidence for non-code criteria, scope, and interface contracts.
4. Report findings as Blocker, Should fix or Nit. Give the file, the line and one sentence of reason for each. Say so explicitly when a pass found nothing. Do not invent findings to look thorough, and do not approve what you could not verify.
5. Recheck base and head before posting. If either changed, report the review as stale and review the new revisions. Post the report on the PR with both SHAs and verification evidence; link it from the ticket. Blockers return to implementation; no Blockers plus verified required evidence permits human merge. Keep Should fix and Nit visible. Never merge or close the ticket yourself.
