---
name: checkpoint
title: Checkpoint
summary: The daily, replaced by an event-driven check. Detects loops rather than reporting progress.
argument-hint: [optional: story or agent to check]
---

Run a checkpoint on: $ARGUMENTS

A daily standup makes no sense for a team that does not sleep. The daily's real
function was catching impediments early; here that becomes catching **loops**.

Delegate to the `scrum-master` subagent, which reacts to state rather than
asking for reports.

## Read state, do not interview

Read status files, diffs and command output. Do **not** open conversations with
the executing agents to ask how things are going — reading is cheap, and
conversation spends the orchestrator's context, which has to survive the whole
sprint.

## The three events

**An agent finished.** Route the diff to `qa` in a clean context. Do not
pre-read it yourself and do not pass along the developer's reasoning.

**An agent is blocked.** Decide between exactly two moves: give it more context
(amend the context package explicitly), or split the story and requeue. Do not
implement the blocking piece yourself.

**An agent has gone N iterations without turning green.** This is a loop, and a
loop is a spec problem rather than an effort problem. Stop the agent and send
the story back to refinement. Retrying costs nothing in time and everything in
review attention.

## Output

For each active story: state, executor, iterations so far, and the decision
taken. Say explicitly when the decision is "no action".
