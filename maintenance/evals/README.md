# Evaluations

An evaluation records what happened when a defined scenario or check was run. It answers whether the development loop works in practice; improvement recommendations belong in [reviews](../reviews/README.md).

## When to write one

Write an evaluation when testing the template's skills, tool compatibility, or handoff behavior. Ordinary project test results belong in the relevant issue or PR. This directory is for template maintenance and should not be copied into ordinary projects.

## How to write one

Name the file `YYYY-MM-DD-short-title.md`. Add a numbered suffix for another run on the same day rather than overwriting its evidence. Use these sections as a guide:

- Scope: the scenario, success criteria, and evidence type (documentation check, local check, or live execution).
- Environment: repository/input revision, tool versions, model IDs, and effort settings.
- Results: commands, exit statuses, observed outcomes, and issue/PR links or revisions where relevant.
- Interventions and Limits: human interventions, failures, skipped steps, and anything not verified.

Record observations, not expected results presented as facts. Label a procedure as planned until executed. Never include credentials; leave unknown versions or model IDs explicitly unknown. Link a related review when the results lead to improvement candidates instead of repeating its findings.

## First live demonstration

Use an isolated toy GitHub repository with a tiny executable feature and two dependent agent tickets. Configure real commands, labels, and Repository. Use a different model for review. The human performs prerequisite completion and PR merges. Run sequentially; no bootstrap or doctor automation is needed.

1. Grill one ordinary behavior in its feature plan, persist it, interrupt the conversation, and recover it from that same plan in a fresh session.
2. Approve and publish two dependent tickets. Interrupt publication and resume; confirm recorded IDs are reused and no duplicate issue appears, including reconciliation after an unrecorded successful creation.
3. Attempt selection of the blocked second ticket; confirm it is rejected before coding.
4. Implement the first ticket with behavioral TDD and open its single default-branch PR. A different model reviews the pinned revision.
5. Seed one genuine defect in the isolated toy change. Obtain a Blocker, correct it in a new implementation session on the same PR, and review the new revision.
6. Have the human merge the first PR; verify automatic issue closure, the merged prerequisite's presence, and selection of the second ticket.
7. Discover a missing human prerequisite; find or create its Human prerequisite issue and attach it as a blocker. Verify no values were printed and resume only after human completion evidence.
8. Local-file tracker mode has been removed. Replace that earlier report step with a run using the Blocked by body fallback; also check native dependencies only if local CLI support and permissions are available.

After the run, review the template again using observed failures and interventions. A local toy test alone does not satisfy steps involving GitHub, another model, or a human merge.
