---
name: planning
title: Sprint planning
summary: Select Ready stories and allocate a model to each. Capacity is measured in what the human can review, not what the agents can produce.
argument-hint: [sprint goal]
---

Plan the sprint. Goal: $ARGUMENTS

Delegate orchestration to the `scrum-master` subagent.

## Selection

Only **Ready** stories are eligible — those carrying a complete context package
from refinement. A story that has not been refined does not enter the sprint,
however urgent it looks.

## Model allocation

This dimension does not exist in human Scrum. Decide it story by story:

| Story shape | Executor |
|---|---|
| Mechanical, contract defined, 1–2 points | `dev` |
| Crosses layers, no design decision, 3 points | `dev` |
| Design decision or contract change, 5 points | `dev-senior` |
| Verification of anything | `qa`, always in a clean context |

## Capacity

Sprint capacity is **how much the stakeholder can review**, not how much the
agents can produce. Agents outproduce any single reviewer; a sprint sized by
agent throughput ends as an unreviewed pile.

Ask the human directly how much review time they have, and size against that
answer. If they have not given one, state the assumption you used.

## Output

A table of selected stories with points, executor, and the declared file budget
for each. Flag anything whose file list overlaps another story in the same
sprint — concurrent diffs on the same files are a merge problem waiting to be
discovered at review.
