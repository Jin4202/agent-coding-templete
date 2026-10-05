# Architecture Decision Records (ADR)

Code shows only what was done, not why it was done that way. Agents have no memory between sessions, so decisions that have a reason not to be reversed later are recorded here briefly. Where `CONTEXT.md` holds the meaning of terms, this folder holds the reasons behind choices.

## When to write one

Write one only when all three of these hold:

1. It is hard to reverse.
2. It would look surprising without the context.
3. It is the result of a real trade-off between several options.

If any one is missing, do not write it. The agent proposes whether to write one first, and the user decides.

## How to write one

Copy `0000-template.md` and give it the next number. File names follow the format `0001-short-title.md`. A few lines per entry is enough. When a decision changes, do not delete the old record; change its status to "Superseded" and point to its number from the new record.
