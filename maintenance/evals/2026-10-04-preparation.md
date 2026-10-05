> Historical template record. File paths and configuration roles describe the layout at the time; current rules are in [AGENTS.md](../../AGENTS.md).

# Preparation verification — 2026-10-04

## Status and scope

Completed documentation/skill updates and static checks. The user explicitly requested stopping before the live demonstration. No toy repository was created, no issue or PR was published, no other model was invoked, and no human merge was performed. This is preparation evidence, not an eight-step evaluation result.

The directory has no Git metadata. Repository and the four application verification commands remain intentional template placeholders; they were not guessed. Typecheck, lint, single application test, and full suite are skipped because the commands are unfilled. There is no application test baseline to report for this document-only update.

## Tool and model evidence

| Item | Observed value |
| --- | --- |
| Node | v20.20.2; version inventory only, no toy execution |
| Git | 2.50.1 (Apple Git-155) |
| GitHub CLI | 2.88.1 |
| Python validator | Failed before validation because PyYAML is not installed |
| Implementing model | This session; exact model ID/effort not independently exposed in command output |
| Independent reviewing model | Not invoked; deferred with the demonstration |
| Live-run human interventions | Not measured; no live run |
| Preparation steering | One user clarification to stop before demonstration |

## Commands and results

| Check | Command/method | Exit status and result |
| --- | --- | --- |
| Tool inventory | `node --version`, `git --version`, `gh --version` | 0; versions above |
| Bundled skill validator | `python3 /Users/jinseokheo/.codex/skills/.system/skill-creator/scripts/quick_validate.py .agents/skills/grill` | 1; `ModuleNotFoundError: No module named 'yaml'`; no dependencies installed |
| Alternative frontmatter validation | Ruby standard-library `YAML.safe_load` for all four SKILL.md frontmatters; verify name matches directory, required keys/types, description length | 0; four passed; this does not substitute for behavioral validation or claim the bundled validator passed |
| Local Markdown references | Python pathlib check of relative Markdown link targets throughout the repository | 0; no broken local links |
| Configuration paths | Python pathlib existence check of configured document locations | 0; all configured locations exist |
| Instruction consistency | `rg` search plus manual review of the four skills and guides | No local tracker path, exact-one seam requirement, or hard-coded configured labels/document paths remains in skill bodies; config bootstrap path retained intentionally |
| Live demonstration | Not run | Deferred by user |

Static checks establish formatting and discoverability of references, not correctness under interrupted remote publication, different-model review, or human merge. Historical review reports are in `../reviews/`.

## Setup documentation evidence — 2026-10-04

These source checks were previously stored in a separate setup guide and are preserved here. A documented path is not proof of local CLI discovery or successful skill execution.

| Tool | Documented workspace skill path | Observed evidence |
| --- | --- | --- |
| Codex | `.agents/skills/` | The four skills appeared in the session's supplied skill catalog; separate fresh CLI discovery was not tested |
| Claude Code | `.claude/skills/` | Official documentation checked; local discovery not tested |
| Gemini CLI | `.agents/skills/` alias or `.gemini/skills/` | Official documentation checked; local discovery not tested |

Sources checked directly on 2026-10-04: [OpenAI skill discovery](https://learn.chatgpt.com/docs/build-skills), [Claude Code skills](https://code.claude.com/docs/en/skills), [Gemini skills](https://geminicli.com/docs/cli/skills/), [Gemini instruction filenames and imports](https://geminicli.com/docs/cli/gemini-md/).

Local `gh --version` reported 2.88.1. `gh issue create --help` did not expose the dependency flags described in [GitHub's dependency documentation](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/creating-issue-dependencies), so the body fallback applies to that observed environment. No authenticated GitHub mutation was performed. The [GitHub linking documentation](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue) also established that closing keywords require a default-branch PR target.

Current usage instructions are in the [root README](../../README.md). These observations do not certify newer installed versions or a completed live demonstration.
