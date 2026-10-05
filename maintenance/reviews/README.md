# Reviews

A review records structural problems and ranked improvement candidates. It answers what should change and why; actual execution evidence belongs in [evaluations](../evals/README.md).

## When to write one

The review-codebase skill reports in conversation by default. Save a standalone report here when the user requests a lasting template review. Selected candidates can become GitHub issues when publication is requested, or decisions in their feature plan. Ticket-level code review belongs on its PR.

This directory is for template maintenance and historical reports. Do not copy it into an ordinary project or make a separate report mandatory for every review.

## How to write one

Name the file `YYYY-MM-DD-codebase-review.md`; use a numbered suffix for another review that day. Keep three parts:

1. Scope and Evidence: what was inspected, how it was selected, and verification limits.
2. Candidates: at most five, ranked. Give target files, the problem, improvement direction, benefits, and strength (Strong, Worth exploring, or Speculative).
3. Recommendation: the best next candidate and why, with links to related evaluations, plans, or issues.

Record acceptance or rejection of candidates when decided so later reviews can recover it. A recommendation is not an approved implementation decision. Preserve earlier reports; their paths and line numbers describe the layout when reviewed, not current setup instructions.

Shared rules and settings are in [AGENTS.md](../../AGENTS.md). Template decisions are in [the feature plan](../../docs/plans/template-loop.md).
