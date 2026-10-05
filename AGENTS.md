# AGENTS.md

This file holds the instructions every agent tool reads. Tool-specific settings do not go here; they go in each tool's own config location.

## Project

[Write the project name and a one-paragraph description here.]

## Conversation language

Talk to the user in the language of user preference. Write code, identifiers, and commit messages in English. Skill files are written in English. Domain terms follow the spelling in `CONTEXT.md`.

## Issue tracker

| Setting | Value | Notes |
| --- | --- | --- |
| Type | GitHub Issues | The only supported tracker |
| Repository | [owner/repo] | `gh` commands point to this repository |

## Labels

| Role | Label | Meaning |
| --- | --- | --- |
| Agent eligibility | `ready-for-agent` | An agent ticket; dependencies must also be satisfied |
| Human prerequisite | `needs-human` | A step only a human can do; agents do not implement it |

## Document locations

| Document | Location |
| --- | --- |
| Domain glossary | `CONTEXT.md` |
| Decision records | `docs/adr/` |
| ADR template | `docs/adr/0000-template.md` |
| Plans | `docs/plans/` |
| Environment declarations | `.env.example` |
| Shared instructions | `AGENTS.md` |
| Skill sources | `.agents/skills/` |

## Read before starting work

1. Read this file for settings and the shared workflow contract.
2. Read the configured Domain glossary to align on terms.
3. Read the configured Decision records. Read the full body of any that relate to the task.
4. Read the plan linked to your assigned ticket.

## Commands

| Task | Command |
| --- | --- |
| Typecheck | [fill in] |
| Lint | [fill in] |
| Single test file | [fill in] |
| Full test suite | [fill in] |

## Development loop

Skills live at the Skill sources location in this file. When asked to use a skill, read its `SKILL.md` and follow it as written.

| Skill | When | Session rule |
| --- | --- | --- |
| `grill` | When fleshing out the plan for a new feature or change | Persist confirmed decisions and open questions during the interview |
| `tickets` | When grilling is done and a spec and tickets are needed | Prefer the same session; the same plan file is the authoritative input |
| `implement` | When implementing or reviewing a single ticket | Start each ticket in a fresh context |
| `review-codebase` | When the user asks for a codebase review, every few days rather than after every ticket | Do not run `grill` in the same session; start it fresh with the chosen candidate |

As a rule, review is done by a different model than the one that implemented.

## Shared workflow contract

Every skill reads AGENTS.md first. Resolve document paths and label names by their roles above; do not duplicate their values in skill instructions. An unfilled Repository blocks remote operations, not local drafting. Target every GitHub operation at the configured repository explicitly.

One agent ticket has one PR targeting the repository's default branch, with `Closes #N` in its body. A coding dependency is satisfied only when that ticket's PR is merged into the default branch and the dependent checkout includes that change. A closed issue alone is insufficient. A human prerequisite is the exception: a human records completion evidence and closes its issue; no PR is required. A cancelled issue does not satisfy a dependency.

Use native dependencies only when local `gh` help exposes the required write and read support and repository permissions allow it. Otherwise keep a `Blocked by: #N, #M` line at the start of the issue body, or `Blocked by: none`. Resolve every listed blocker before selecting a ticket. If native and body relationships disagree, reconcile them before proceeding; never ignore a blocker. Labels express ticket kind, not automatic readiness.

Only a human merges PRs. A review with Blockers returns to a fresh implementation session on the same PR branch, then a different model reviews the changed revision. A review without Blockers can be handed to the human for merge only when required checks and acceptance evidence are verified. Should fix and Nit findings remain visible for the human's decision. Record base and head SHAs on every review; a changed revision requires another review.

Read all four verification entries in Commands. Run filled commands before changes to capture baseline failures and at the end to capture final results, including lint. During behavioral TDD, run typecheck and the relevant single test as needed. For a single-file command, supply the actual test file using the command's documented invocation. Report every empty or placeholder command as skipped; never invent it or claim it passed. Existing failures are evidence, not permission to weaken tests or ignore new failures. Non-code acceptance criteria use reproducible human-checkable evidence instead of artificial tests.

## Document ownership

Maintain one `<slug>.md` per feature under Plans. During grilling it contains confirmed decisions and open questions; tickets refines that same file into the approved spec and a compact ticket publication table. Preserve agreed decisions when refining it. Keep ticket state, blockers, implementation results, and PR reviews in GitHub; the plan stores decisions and links, not duplicate status logs. Record ADRs only when their criteria apply. Codebase reviews normally return findings in conversation; publish selected candidates as GitHub issues only when requested, or record an agreed choice in its plan.

Evaluations and historical reports under `maintenance/` are for this template's maintainers, not required project documents. Exclude them and this template's own plan when adopting into another project. Setup and adoption instructions live in the root README.

## Rules

- Record every decision in a file. A decision that exists only in conversation does not exist.
- Follow the shared workflow contract in this file: one agent ticket per PR, different-model review, human merge, and merge-based dependencies.
- Do not fix anything outside the scope of your ticket. Record problems you find in the ticket or raise them as a new ticket.
- Do not weaken or delete tests to make them pass.
- Never write secret values (keys, tokens, passwords) in conversation, plans, tickets, commits, or logs. The configured Environment declarations list names, issuers, and application read locations only. Never print values while checking presence.
- When you hit a human-only step, stop dependent work. Search existing Human prerequisite issues first, reuse a matching one or create one, and make it a blocker of the current ticket. If the tracker is unavailable or unconfigured, save the exact ticket draft with the current work and report that it has not been published.
- Do not fill gaps with guesses. If you cannot know the answer, ask.
