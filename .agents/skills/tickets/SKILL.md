---
name: tickets
description: Turn a finished grilling conversation into a spec file and a set of small vertical-slice tickets with blocking relationships, then publish them to the issue tracker. Use only when the user explicitly asks to write the spec or create tickets.
---

# Tickets

Refine the existing feature plan into an approved spec and tickets small enough for one fresh agent context each. Do not interview the user from scratch. If a decision that blocks the work is missing, list the gap and ask only about that.

## 1. Gather context

Read `AGENTS.md` first. Resolve all labels and paths through its settings and follow the shared workflow contract. Read Shared instructions, the named `<slug>.md` under Plans, Domain glossary, and relevant Decision records. The plan is authoritative; if conversation adds an agreed decision, persist it there before using it. Ask for the plan file if it cannot be identified. Resolve blocking Open Questions before publishing. Explore code only as far as needed to place the work; make a necessary prefactor its own ticket.

## 2. Write the spec

Refine the same `<slug>.md` under Plans in place; do not create a separate notes or spec file. Preserve confirmed decisions and unresolved questions. Use only the sections needed for the change, with these as a guide.

- Problem Statement
- Solution
- User Stories, a numbered list in the form "As a (who), I want (what), so that (why)"
- Implementation Decisions, covering modules, interfaces, schemas, contracts and architectural decisions. Do not include file paths or code snippets, except a snippet that encodes a decision made from a prototype.
- Testing Decisions, covering what a good test looks like here (it checks external behavior through a public interface), which modules get tests, and prior art in the repo
- Out of Scope
- Further Notes

For testing, sketch the seams where tests attach. Prefer existing seams at the highest useful point. Use the minimum number that covers all behavior, preferably one. Confirm the seams with the user. For non-code acceptance criteria, define human-checkable evidence.

Show the spec to the user and apply corrections before moving on.

## 3. Draft the tickets

Cut vertical slices. Each ticket is a narrow but complete path through every layer it touches, such as schema, API, UI and tests. It can be demonstrated or verified on its own, and a fresh agent can finish it without this conversation. If you doubt that, split it.

Each ticket has a title, a Blocked by list, a short "what it delivers" paragraph, acceptance criteria as checkboxes, and a link to the plan. Do not put file paths or code in tickets.

Wide refactors are the exception. A mechanical change with a large blast radius, such as renaming a shared column or symbol, is sequenced as expand, migrate, contract. The expand ticket adds the new form beside the old one. Migrate tickets move callers in batches sized by blast radius, each blocked by the expand ticket and each leaving CI green. The contract ticket deletes the old form and is blocked by every migrate ticket. Each still has its own default-branch PR. If batches cannot stay green independently, revise the breakdown with the user; do not silently introduce a shared integration branch that bypasses the merge-based dependency contract.

For human-only work, search existing Human prerequisite issues in the configured repository. Reuse a matching issue or draft a new one with that configured label; dependent tickets list it under Blocked by. Specify the action, variable names, issuers, application read locations, and completion evidence, never secret values. Agent tickets follow one ticket per PR; human prerequisites need no PR.

## 4. Review the breakdown with the user

Ask about granularity, whether each blocking relationship is right, and which tickets to merge or split. Repeat until the user approves. Publish nothing before approval.

## 5. Publish

GitHub Issues is the only tracker. Stop remote publication if Repository is unfilled. Before creating issues, save the approved breakdown in the plan's Tickets table with a stable key per ticket, dependencies, and initially empty issue number/URL fields. After publication, GitHub owns ticket state and full acceptance details; this table keeps stable keys and links for recovery. Make the approved plan available at a remotely readable revision and use that link in issues; local-only paths are not a handoff.

Create in dependency order, explicitly targeting Repository. Apply the configured Agent eligibility or Human prerequisite label by role. Set dependencies using the shared workflow contract's local-capability check and body fallback. Use structured bodies or a body file, preserving newlines.

Immediately after each successful creation, record its number and URL in the plan. On retry, verify recorded issues and skip creating them again; reconcile incomplete labels or dependencies. Include the plan identity and stable ticket key in each issue body. If creation succeeded but local recording was interrupted, search for that exact identity before retrying. An ambiguous result requires reconciliation, not another issue. Stop on an uncertain API result; do not blindly retry. The ticket table must travel with the plan for another session to resume it.

Never close or edit a parent issue.

## 6. Finish

List published tickets and mark the frontier according to the shared merge-based dependency contract, including the human-prerequisite exception. Record any unfinished publication steps in the plan. Tell the user to read and follow implement `SKILL.md` under Skill sources on one frontier ticket at a time, each in a fresh context. Do not invoke it yourself.
