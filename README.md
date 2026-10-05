# Development Loop Template

Four skills for a personal development loop: grill a plan, publish tickets, implement one ticket at a time, and occasionally review the codebase. Repository files preserve decisions across models; GitHub owns work status and PR reviews.

## Daily documents

```text
AGENTS.md                 Rules, commands, repository, labels, and document locations
CONTEXT.md                Domain glossary
docs/
  plans/<slug>.md          One feature plan: interview decisions → approved spec → ticket links
  adr/                    Only decisions that meet the ADR criteria
.agents/skills/            Shared sources for the four skills
```

Maintain one plan per feature. Grilling writes confirmed decisions and open questions; tickets refines the same file into the approved spec. Keep a compact table of ticket keys and issue links for publication recovery. Ticket state, dependencies, implementation results, and reviews stay in GitHub. Do not mirror them into another report or log.

## Start a project

1. Create a repository from the template and clone it.
2. Fill the project description, Repository, and Commands in [AGENTS.md](AGENTS.md). Review its label roles and document locations.
3. Create the configured labels with `gh label create`, explicitly targeting Repository.
4. Connect the tools to the configured Skill sources using the instructions below. Set up `gh` authentication and verify the default branch.
5. Start with: “Read `.agents/skills/grill/SKILL.md` and follow it. What I want to build is …”

Run tickets next, preferably in the same session, using the feature plan as input. Approve the breakdown before publication. Implement each frontier ticket in a fresh session with one branch and one default-branch PR containing `Closes #N`. Review with a different model. Correct Blockers on the same PR and review the changed revision; only a human merges.

Agent dependencies require a merged PR available in the dependent checkout. Human prerequisites require human completion evidence and issue closure. Run all filled verification commands before and after changes, including lint; report baseline failures and skipped unfilled commands. Non-code criteria use human-checkable evidence.

Codebase review normally returns a short list in conversation. Publish selected candidates as issues when requested, or record the agreed choice in its feature plan. A separate review report is optional.

## Connect tools

| Tool | Workspace skills | Shared instructions |
| --- | --- | --- |
| Codex | `.agents/skills/` | `AGENTS.md` |
| Claude Code | `.claude/skills/` | `CLAUDE.md` imports `@AGENTS.md` |
| Gemini CLI | `.agents/skills/` alias or `.gemini/skills/` | Set `context.fileName` to `AGENTS.md`, or import it from GEMINI.md |

Sources: [OpenAI skills](https://learn.chatgpt.com/docs/build-skills), [Claude Code skills](https://code.claude.com/docs/en/skills), [Gemini skills](https://geminicli.com/docs/cli/skills/), [Gemini instruction files](https://geminicli.com/docs/cli/gemini-md/). Dated verification evidence is in [the preparation record](maintenance/evals/2026-10-04-preparation.md).

Use the configured Skill sources as the single source. With the default layout and no existing Claude skills directory:

```bash
mkdir -p .claude
ln -s ../.agents/skills .claude/skills
```

If the directory already exists, inspect it and link individual missing skills instead of replacing it. Adjust links if configured paths differ. In each tool, start a fresh session, confirm the four skills appear, and invoke grill to check that it reads AGENTS.md and persists a confirmed decision in the feature plan. Discovery does not establish invocation policy; keep tool-specific settings separate from common instructions.

Use native GitHub dependencies only when local CLI support and repository permissions allow both writing and reading them. Otherwise use the issue body's `Blocked by` line as defined in AGENTS.md. PRs target the default branch for `Closes #N` to close the linked issue on merge. [GitHub dependencies](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/creating-issue-dependencies), [issue/PR linking](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue).

## Adopt into an existing repository

Use a clean branch or isolated checkout. Copy only absent template files, excluding Git metadata, real environment files, `maintenance/`, and the template-specific plan. Manually merge overlapping instructions, skills, glossary, and environment declarations; retain the project's vocabulary and commands. Define how to supply a single test file and leave truly inapplicable commands empty. Review the diff before opening an adoption PR; preserve existing tool directories and credentials.

## Template maintenance

[maintenance/](maintenance/) contains historical reviews and evaluation records. These are not required project documents. Exclude it and [the template's own plan](docs/plans/template-loop.md) when adopting into another project. Keep the four skills, shared instructions, glossary, environment declaration format, and ADR guide/template.

The live end-to-end demonstration remains deferred. Documentation checks and preparation records are not evidence of a completed live loop. See [the evaluation procedure](maintenance/evals/README.md) when resuming template validation.
# agent-coding-templete
