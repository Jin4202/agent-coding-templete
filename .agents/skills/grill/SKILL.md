---
name: grill
description: Interview the user relentlessly about a plan until every decision is concrete, and record new domain terms and hard-to-reverse decisions in the repo as they appear. Use only when the user explicitly asks to grill, plan, or clarify a feature or change.
---

# Grill

Remove ambiguity before any code is written. The user's answers are the slowest part of the loop, so this is where care pays off. Create or update the feature plan during the interview. Do not write code or publish tickets.

Write domain terms exactly the way the user says them.

## Before asking anything

1. Read `AGENTS.md` first. Resolve every document location and label through its settingss settings and follow its shared workflow contract.
2. Read Shared instructions, Domain glossary, and Decision record titles from AGENTS.md; open related records. Create or resume `<slug>.md` under Plans. If resuming, read confirmed decisions and remaining questions before asking anything.
3. If the request touches existing code, read the relevant modules first. Never ask a question the code or the repo files already answer.

## The interview

- Ask one question at a time. With each question, give your recommended answer and the reason in one or two sentences, so the user can simply agree.
- Walk the decision tree in this order, skipping any branch the request already settles. Start with the goal and who benefits. Then constraints, dependencies and external systems, the shape of the modules and their interfaces, edge cases, how it will be tested, and what is out of scope.
- Probe edge cases with concrete scenarios, for example "what happens when a user does X while Y is still running". Abstract questions get abstract answers.
- If the user's wording conflicts with the Domain glossary, or a term is vague, stop and sharpen it before moving on.
- Prefer keeping the same session through tickets. Persist decisions before moving to the next question so interruption or context summarization does not lose them.
- Stop asking when the remaining questions would not change the implementation. Say so plainly.

## Record as you go

Update the repo files during the interview, not afterwards.

- In the plan, maintain Confirmed Decisions and Open Questions. Record each confirmed answer immediately, with its rationale when useful, and update superseded answers explicitly. Keep recommendations separate from confirmed decisions. Link related terms and ADRs. This same file is the authoritative input to tickets.
- When a new term appears or a term is sharpened, update Domain glossary right away. Use the bold term, a one-sentence definition, and a line listing the synonyms to avoid. Leave out implementation details.
- Offer an ADR only when all three hold: hard to reverse, surprising without context, and the result of a real trade-off. Also offer one when the user rejects an option for a reason that other work will depend on. Ask before writing it, then use ADR template with the next number in Decision records.

## Finish

Check that the plan contains every confirmed decision and remaining question. Summarize the plan path, glossary changes, and ADRs. Tell the user to read and follow the tickets `SKILL.md` under Skill sources next, preferably in this session, using the same plan file as input. Do not invoke it yourself.
