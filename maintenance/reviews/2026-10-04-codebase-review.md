> Historical template record. File paths and configuration roles describe the layout at the time; current rules are in [AGENTS.md](../../AGENTS.md).

# Development loop template review — 2026-10-04

## 1. Scope and evidence

Reviewed all 15 existing files, including the four skills, shared instructions, configuration, glossary, document guides, and README. Compared them with the user's supplied development-loop description. This is a review of a documentation-based workflow: its interface is what a user or another agent must know to move between stages.

The supplied directory has no Git repository metadata; `git status` reports that it is not a repository. Consequently there is no change history or co-change evidence to rank hotspots. There are no application sources or executable test commands in this template. Findings below come from tracing the documented workflow, not from an end-to-end execution. There are no earlier review reports or accepted ADRs; `0000-template.md` is a template.

The foundation is coherent: four explicitly invoked stages, shared skill sources, separate glossary/spec/ADR responsibilities, vertical slices, human prerequisites, and separate standards/spec review passes. Most of the supplied plan is represented. Missing behavior concentrates at handoffs, tracker configuration, and verification.

Only this report was added. Recommendations are proposals, not adopted decisions. No issues, labels, commits, account settings, or skill files were changed.

## 2. Ranked candidates

### 1. Complete the implementation-to-completion handoff

- **Files:** `.agents/skills/implement/SKILL.md:16,28,44,48,54,60`; `.agents/skills/tickets/SKILL.md:55`; `README.md:44`.
- **Problem:** Implementation explicitly leaves a ticket open; review ends with a comment. No stage assigns responsibility for fixing findings, repeating review, integrating the result, closing the ticket, or releasing dependents. A fresh agent cannot determine whether a reviewed ticket is actually available in its checkout. Following every instruction can leave the frontier permanently blocked. Closing a ticket prematurely could instead release work before its prerequisite is integrated. The review interface is also incomplete: commit messages containing `Refs #N` identify intent but do not pin an exact comparison base and reviewed revision.
- **Direction:** Finish the existing implement/review workflow with explicit completion ownership and evidence. Clarify the current-branch prerequisite and treatment of existing user changes. Record the review base and target revision, verification result, unresolved findings, and integration location. Define the correction/review/completion responsibility and when blockers count as satisfied. Keep sequential use as the default.
- **Benefits:** Improves locality of lifecycle rules and makes the handoff reproducible across models. Removes hidden human work from frontier selection and makes a second-ticket demonstration possible.
- **Strength:** Strong.
- **Deletion test:** The implement skill hides real work and should remain. Its lifecycle is incomplete; the missing coordination currently reappears in the user and subsequent agents.

### 2. Persist ordinary planning decisions before the spec exists

- **Files:** `AGENTS.md:44`; `.agents/skills/grill/SKILL.md:8,23,28,30,31,35`; `.agents/skills/tickets/SKILL.md:8,12`; `docs/specs/README.md`.
- **Problem:** The shared rule requires every decision to exist in a file, but grilling only specifies persistent storage for terms and ADR-worthy choices. Ordinary behavior, scope, and test decisions remain in conversation until tickets writes the spec. For example, an agreed maximum batch size is neither a glossary term nor necessarily an ADR. A long interview interrupted or summarized before tickets can lose it despite the repository-memory promise. The finish instruction asks for a summary without specifying a persistent artifact.
- **Direction:** Give confirmed planning answers and open questions a lightweight persistent home, separate from the glossary and ADRs, and make tickets consume it. Clarify that keeping the same session preserves useful discussion but cannot guarantee unlimited context retention. Preserve the current separation between interviewing and final spec writing.
- **Benefits:** Improves handoff testability and reduces dependence on conversation history without inflating CONTEXT.md or producing ADRs for every choice.
- **Strength:** Strong.
- **Deletion test:** The glossary and ADRs hide distinct complexity and should stay separate. Ordinary decisions have no corresponding implementation of persistent storage; that complexity leaks into the conversation.

### 3. Make tracker and configuration support match the advertised contract

- **Files:** `docs/agents/config.md:3,9,10,14,19`; `.agents/skills/tickets/SKILL.md:16,38,48,49`; `.agents/skills/implement/SKILL.md:16,24,44,60`; `.agents/skills/review-codebase/SKILL.md`; `README.md:21`.
- **Problem:** Config promises that project values can change without editing skills, but skills repeatedly hard-code document locations and label names. Implement selects a ticket before explicitly reading config. Local-file publishing is offered, yet stable ticket IDs, status updates, implementation notes, review storage, and dependency resolution are unspecified; later stages assume issue numbers and comments. Writing another batch to the single `docs/tickets.md` has no preservation rule. GitHub publishing also lacks a persistent record of successfully created issues if a later creation fails, leaving duplicate creation possible on retry.
- **Direction:** Either narrow the supported configuration to the first proven tracker or carry each advertised option through the full loop. Give tracker behavior one documented source of truth that the skills read before acting. Clarify label eligibility versus dependency readiness, consistent dependency evidence, repository targeting, preserving old local tickets, and resuming partial publication.
- **Benefits:** Makes configuration changes local, removes a misleading interface, and gives both supported trackers demonstrable behavior. GitHub and local files would be real adapters only if both actually implement the loop; a programmatic tracker abstraction is unnecessary at this point.
- **Strength:** Strong.
- **Deletion test:** Configuration would earn its place by hiding project variation, but currently callers still need the same hard-coded knowledge. Deleting the incomplete local option would reduce obligations; retaining it requires implementing its documented behavior.

### 4. Clarify prerequisite and verification behavior for real projects

- **Files:** `.agents/skills/implement/SKILL.md:24,32,36,55`; `.agents/skills/tickets/SKILL.md:26,38`; `AGENTS.md:23`; `.env.example`.
- **Problem:** Prerequisites are reduced to an environment variable being set. That does not distinguish a shell variable from an application-loaded `.env` entry or document a human task with no variable. Runtime discovery creates a human ticket but does not explicitly make the current ticket depend on it or reuse an existing human blocker. Verification requires typecheck/tests but omits the configured lint command, handling of inapplicable or unfilled commands, and baseline failures. Review requires every acceptance criterion to have test evidence, which does not fit purely documentary or dashboard criteria. Tickets' target of exactly one test seam also risks excluding distinct behaviors that need separate verification.
- **Direction:** Describe prerequisite sources and completion evidence without exposing credentials; connect newly discovered prerequisites to the dependent ticket. Establish how to report baseline failures, required versus inapplicable checks, and justified verification for non-code changes. Keep behavioral TDD for changes with executable behavior; choose test surfaces from coverage needs rather than a universal count.
- **Benefits:** Makes instructions usable by a weaker model without guessing commands, creating duplicate blockers, overlooking lint, or inventing meaningless tests.
- **Strength:** Strong.
- **Deletion test:** Prerequisite and verification steps hide valuable complexity. Their incomplete interface pushes project-specific interpretation back into every implementing and reviewing agent.

### 5. Replace setup uncertainty with documented support and one demonstrated loop

- **Files:** `README.md:9,25,34,36,73`; `CLAUDE.md`; `.agents/skills/*/SKILL.md`; `docs/agents/config.md`.
- **Problem:** The README honestly labels the template untested, but several uncertainties can now be resolved from primary documentation. There is still no checked example showing that discovery, decisions, tickets, different-model review, human blockers, and the next frontier work together. The original description's existing-repository adoption path and model evaluation method also have no corresponding local guide or results record. Tool discovery alone cannot establish successful execution.
- **Direction:** Add a concise support/setup guide with documentation links, verification date, tested CLI versions, and a manual discovery check. Provide an existing-repository adoption path that preserves user files. Demonstrate one small loop before investing in bootstrap scripts, a doctor command, global installation, or a large model benchmark. Keep shared procedure separate from tool-specific invocation settings.
- **Benefits:** Gives users reproducible onboarding and a concrete test surface for skill changes. Reduces speculative setup work and distinguishes documented support from observed behavior.
- **Strength:** Strong.
- **Deletion test:** A setup guide earns its place if it hides repeated discovery/configuration work. The current guide sends that uncertainty back to each user; additional automation should wait until the repeated steps are proven.

Official-document checks on 2026-10-04:

- Codex documents repository `.agents/skills` discovery and symlink support. This template already uses a documented location. [OpenAI local skill discovery](https://learn.chatgpt.com/docs/build-skills).
- Gemini CLI documents `.agents/skills/` as a workspace alias and `context.fileName` for selecting instruction files. Its README entries can become concrete setup guidance. [Gemini skills](https://geminicli.com/docs/cli/skills/), [context filenames](https://geminicli.com/docs/cli/gemini-md/).
- Claude Code documents `.claude/skills/` and an explicit manual-invocation setting. A description saying “only when explicitly asked” is an agent instruction; tool-level invocation control is a separate configuration concern. [Claude Code skills](https://code.claude.com/docs/en/skills).
- GitHub documents native issue dependencies and requires at least triage permissions to create them. Current docs also describe CLI dependency flags, but installed `gh 2.88.1` does not list them in `gh issue create --help`. Check local capabilities before choosing the native CLI path; native feature support and CLI version support are separate. No authenticated remote action was attempted. [GitHub dependencies](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/creating-issue-dependencies).

The referenced originals are now readable. The original [code-review](https://github.com/mattpocock/skills/blob/main/skills/engineering/code-review/SKILL.md) pins a fixed comparison point, reinforcing candidate 1. [Domain modeling](https://github.com/mattpocock/skills/blob/main/skills/engineering/domain-modeling/SKILL.md) uses GLOSSARY.md; retaining CONTEXT.md here is an intentional adaptation, not a defect. [Codebase design](https://github.com/mattpocock/skills/blob/main/skills/engineering/codebase-design/SKILL.md) provides shared design vocabulary. The original [wizard](https://github.com/mattpocock/skills/blob/main/skills/engineering/wizard/SKILL.md) generates a human-operated script, a larger responsibility than recording `needs-human` tickets. It is optional, not required for the four-stage loop. Naming or copying additional helper skills is not itself a missing capability; extract shared discipline only where repeated rules actually drift.

## 3. Top recommendation and verification target

Start with candidate 1. The defining property of this template is a repeatable loop, and its present instructions do not complete the first ticket in a way that reliably releases the second. Candidates 2–4 then remove information loss and ambiguous prerequisites. Candidate 5 supplies evidence that those changes work.

A minimal future demonstration should cover:

1. Agree on an ordinary behavior and recover it from files after a conversation interruption.
2. Publish two agent tickets with a dependency; interrupt publishing and resume without duplicates.
3. Confirm the blocked ticket cannot be selected.
4. Implement the first ticket and hand a pinned revision to a different model.
5. Introduce one real review finding, correct it, and verify the corrected revision.
6. Integrate and complete the first ticket; verify the second is selectable with its prerequisite available.
7. Discover a missing human prerequisite, reuse or create its human ticket, and record the blocking relationship without exposing credentials.
8. Repeat tracker-dependent steps with local files only if local mode remains advertised.

Record the tool/model version, input revision, commands/results, interventions, and cost or quota consumption for that demonstration. Do not commit hidden evaluation tests into an agent-visible checkout; keep the evaluator separate if expanding into model comparisons.

At the time of this initial report, these were proposals and none had been accepted or rejected.

## Follow-up status — 2026-10-04

The user accepted directions for all five candidates and authorized a template update. The operating decisions are recorded in `../../docs/plans/template-loop.md`. Skills and guides were updated, and the follow-up review is `2026-10-04-codebase-review-2.md`. The user explicitly deferred the live demonstration; do not describe candidate 5 as empirically complete.
