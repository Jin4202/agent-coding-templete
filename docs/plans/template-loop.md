# Compact development loop

Status: document structure updated; live demonstration deferred by the user.

## Decisions

- Keep project settings, commands, and common workflow rules in AGENTS.md. There is no separate agent configuration file.
- Keep one `<slug>.md` per feature under Plans. Grilling records decisions/questions; tickets refines that same file into the approved spec, preserving decisions. Do not keep separate notes and spec copies.
- Keep domain terms in CONTEXT.md. ADRs are reserved for decisions that are hard to reverse, surprising without context, and based on real trade-offs.
- GitHub Issues is the only tracker. Ticket state, blockers, implementation results, and PR reviews live there. The plan contains agreed behavior and a compact publication table, not duplicate progress logs.
- Each agent ticket has one default-branch PR with `Closes #N`. Different-model review pins base/head SHAs; corrections use the same PR in a fresh session. A human merges. Agent dependencies require merge; human prerequisites require completion evidence and closure.
- Environment declarations name the issuer and application read location without values. Reuse matching human issues and attach them as blockers.
- Run every filled verification command before and after changes, including lint. Report baseline failures and skipped unfilled commands. Non-code criteria use human-checkable evidence. Use the minimum test seams covering behavior, preferably one.
- Codebase review normally reports in conversation. Persist agreed choices in their plan or publish selected issues when requested; standalone review files are optional.
- Setup and adoption instructions live in the root README; dated verification evidence lives in maintenance/evals/. There is no separate setup document. Historical reports and evaluations remain maintenance-only. Demonstrate the loop before building more automation.

## Verification

Check skill metadata, document links, resolved paths, and consistency of the four skills after moving documents. No GitHub mutation, model delegation, or live demonstration is part of this compacting task.

## Tickets

No issues have been published for this template update. When publishing a feature, keep stable ticket keys and issue URLs here, and reconcile uncertain creations before retrying. Read current status from GitHub.

## Deferred

- Choose the toy repository and distinct implementation/review models when resuming the live demonstration.
- Settle how the approved plan and subsequent publication links become available remotely to a fresh checkout.
- Confirm the reviewed revision and check results immediately before human merge.

## References

- [Initial review](../../maintenance/reviews/2026-10-04-codebase-review.md)
- [Follow-up review](../../maintenance/reviews/2026-10-04-codebase-review-2.md)
- [Setup instructions](../../README.md#connect-tools)
- [Setup evidence](../../maintenance/evals/2026-10-04-preparation.md#setup-documentation-evidence--2026-10-04)
- [Evaluation procedure](../../maintenance/evals/README.md)
