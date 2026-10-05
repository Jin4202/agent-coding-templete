---
name: review-codebase
description: Survey the whole codebase for structural problems and write a short, ranked report of refactoring candidates that would make shallow modules deeper. Does not change code. Use only when the user explicitly asks for a codebase review, an architecture review, or cleanup candidates. To review a single ticket, use the implement skill instead.
---

# Review codebase

Find the places where the structure of the code makes it harder to change, test, or reason about, and propose candidates for improvement. This is a survey, not a rescue. Do not change code in this skill, and do not design new interfaces. Run it every few days, not after every ticket.

Keep file names, code identifiers and the vocabulary terms below in English.

## Vocabulary

Use these terms consistently, in your notes and in the report.

- A module is anything with an interface and an implementation, from a function to a package.
- The interface is everything a caller must know to use the module, including types, ordering rules, error behavior and performance expectations.
- Depth is how much behavior sits behind the interface compared with how big the interface is. A deep module hides a lot behind a small interface. A shallow module has an interface almost as complex as its implementation.
- A seam is a place where behavior can be swapped without editing the code on either side, and an adapter is a concrete thing plugged into a seam.
- Leverage is what callers gain for the interface they have to learn.
- Locality is how much of a change, and of its bugs, stays in one place.

Three rules of thumb guide the judgment.

- The interface is the test surface. Tests belong at the interface of a deep module, not on small helper functions extracted from inside it.
- One adapter means a seam is hypothetical, and two adapters mean it is real. Do not recommend a seam for a single adapter unless it sits on a real external boundary such as the database, an outside API, time or the filesystem.
- Apply the deletion test to every suspect module. Imagine deleting it. If its complexity would reappear in many callers, the module is earning its place by hiding that complexity. If the complexity would simply vanish or move over unchanged, the module is a pass-through and is shallow.

## 1. Read the ground rules

Read `AGENTS.md` first. Resolve all document paths and labels through its settings and follow its shared workflow contract. Read Shared instructions, Domain glossary, relevant Decision records, and related plans or existing GitHub improvement issues. Do not propose a rejected candidate again unless changes justify reopening it. If Git history is unavailable, disclose that and review the supplied files without inventing hotspots.

## 2. Pick the scope

If the user named an area, review that area. Otherwise start from the hotspots in git history, meaning the files that changed most often recently and the files that tend to change together. A command such as the one below is a good start.

```bash
git log --since="90 days ago" --name-only --pretty=format: | sort | uniq -c | sort -rn | head -30
```

Tell the user in one or two sentences what scope you chose and why.

## 3. Look for friction

If you can hand the exploration to an independent worker that reports back only a summary, you may. Otherwise do it yourself. Look for the following.

- Shallow modules, where reading the interface is about as hard as reading the code behind it
- Low locality, where one change touches many files, the same concept is implemented in several places, or files that always change together live far apart
- Leaky seams, such as an abstraction with a single adapter, implementation details showing through the interface, or callers that must know the order of calls
- Code that is hard to test or untested, such as tests that mock code this repo owns, or logic split into tiny functions tested alone while the way they combine is never tested
- Names that are not the Domain glossary terms

Run the deletion test on each suspect and drop the ones that pass. Be skeptical of your own findings. Style preferences and small cleanups are not candidates. Only report structural problems that cost something when changing or testing the code.

## 4. Write the report

Return a concise report in conversation with scope/evidence, up to five ranked candidates, and the top recommendation. Do not create a standing report folder. Publish selected candidates as GitHub issues only when the user requests publication; otherwise persist an agreed candidate in its feature plan. Save a standalone report only if explicitly requested. Keep verification evidence with the relevant issue or PR rather than duplicating logs.

Each candidate has these fields.

- Files, the files and modules involved
- Problem, in plain words using the vocabulary above
- Direction, the kind of change that would help, such as merging three modules behind one. Do not write interface signatures.
- Benefits, naming the gains in locality, leverage and testability
- Strength, one of Strong, Worth exploring or Speculative
- A before and after diagram, only when it makes the structure clearer than words do. A small Mermaid block or a text sketch is enough.
- ADR conflicts, only when the friction is real enough that the decision should be reopened. Name the ADR.

Report honestly. If the codebase is healthy, list fewer candidates and say so. If it is so tangled that a survey cannot help, say that, and recommend narrowing the scope instead of listing dozens of problems.

## 5. Hand off

Summarize the top recommendation and the list of candidates for the user, and ask which candidate they want to explore. Do not start designing a solution.

When the user picks one, tell them to read and follow grill `SKILL.md` under Skill sources in a new session with the selected issue URL or feature plan and candidate. Do not invoke it yourself.

If the user rejects a candidate for a reason that other work will depend on, offer an ADR using the configured ADR template. Write it only if they agree. Record accepted/rejected decisions in the relevant plan or authorized GitHub issue so later reviews can recover them.
