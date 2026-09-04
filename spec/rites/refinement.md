---
name: refinement
title: Refinement
summary: Turn a raw backlog item into a Ready story by building its context package. The most important rite in Context Points.
argument-hint: [issue number or a description of the item]
---

Run refinement on: $ARGUMENTS

Refinement absorbs roughly half of what planning does in human Scrum. Its
output is a **context package**, and a story without one is an invitation for
the agent to invent its own.

Delegate to the `product-owner` subagent, which must produce all three parts:

1. **Relevant files** — the explicit list the executing agent may touch.
   Everything omitted is forbidden. Search the codebase; do not guess.
2. **Expected contract** — inputs, outputs, error cases. If an existing
   contract changes, state the before and the after.
3. **Executable acceptance criteria** — commands, not prose. Each criterion is
   something that can be run and observed.

Then apply the gate:

- All three parts present and the criteria are genuinely runnable → mark
  **Ready**.
- Criteria cannot be written as commands → this is **not a story**. Reclassify
  it as a spike and state what the spike must produce so that the real story
  becomes verifiable.
- The file list is speculative → go back and read the code first.

Report the package as the story's body, ready to paste into the tracker.
