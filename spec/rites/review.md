---
name: review
title: Sprint review
summary: The one genuinely synchronous rite. Demo the increment to the human stakeholder, who accepts or rejects.
argument-hint: [sprint or increment to review]
---

Run the sprint review for: $ARGUMENTS

This is the **only synchronous rite** in Context Points, because the bottleneck
is the human. Everything else can happen unattended; this cannot.

## Prepare the demo

For each completed story:

1. The acceptance commands, and their **actual output** — run them now, do not
   quote an earlier run.
2. The diff, scoped to the declared context package.
3. One sentence on what changed for the user of the system.

## Present, do not persuade

Show the increment. Do not argue for it. If a story is done but weakly done,
say so — the stakeholder's attention is the resource the whole sprint was
sized against, and spending it on a favourable framing wastes it.

## The verdict is the human's

Accept or reject, story by story. Record rejections with the reason, and carry
them into the retro as input — a rejection at review is usually a refinement
failure, and refinement is where the fix belongs.

## Output

A table: story, points, executor, accepted or rejected, and for rejections, the
stated reason.
