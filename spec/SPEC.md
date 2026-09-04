# Context Points

**Scrum adapted for teams made of agents.**

Status: `v0.1.0`. Calibrated on a small number of projects. Counter-examples are
the most valuable contribution you can make — see [CONTRIBUTING.md](../CONTRIBUTING.md).

## The premise

Scrum is a protocol for allocating a scarce resource. In a human team that
resource is **time**: story points estimate effort, the sprint boxes a fixed
number of person-hours, velocity forecasts how much fits in the next one.

When the team is made of agents, time is nearly free. An agent attempts a story
in minutes and can retry ten times overnight. Two things stay scarce:

1. **Context** — the window an agent can hold before it loses the thread.
2. **Your attention** — every increment is reviewed by a human, and humans do
   not scale.

Every adaptation below follows from that one substitution. A rule that does not
trace back to context or to reviewer attention is ceremony, and should be
deleted rather than defended.

## What this is not

Three different things get called "agile with AI". They have opposite
constraints, which is why advice about one does not transfer to the others.

| | Who is the team | Who is the human | The hard problem |
|---|---|---|---|
| Agents joining a human team | Humans, with agents as members | A teammate | Trust, handoff, accountability |
| Ceremony automation | Humans | The whole team | Summarising, nudging, reporting |
| **Context Points** | **Agents** | **Stakeholder and reviewer** | **Context budget, verifiable done** |

Context Points assumes the third case: the agents are the team, the human is
the stakeholder. The context-isolation rules below are meaningless in the other
two — you cannot ask a human developer to forget how they solved something.

## Estimation

The scale lives in [estimation.md](estimation.md). Two properties are estimated,
and they are independent of each other.

**Size** answers one question: *does this fit in one session without the agent
losing the thread?* That is a context budget, not an effort forecast.

**Verifiability** answers a second: *can "done" be proven with a command?* If it
cannot, the item is not a story. It is a spike, and the spike's deliverable is
the set of criteria that make the real story verifiable.

### Planning poker, adapted

The original purpose of planning poker was never forecasting. It was
**detecting ambiguity**: when estimates diverge, the story means different
things to different people.

That purpose survives intact and automates cleanly.

1. The Product Owner, the Dev Senior and QA estimate the same story.
2. Each estimates in a **clean, separate context**, without seeing the others'
   answers.
3. Divergence greater than one step on the scale means the spec is ambiguous.
   The story returns to refinement. It is **not** averaged.

The isolation is the entire mechanism. Run all three in one session and they
converge by anchoring on whoever answered first, and the estimate carries no
information at all.

## Rites

### Refinement — the most important rite

Refinement absorbs roughly half of what planning used to do. The Product Owner
may mark an issue **Ready** only when it carries a **context package**:

- the files that are relevant — and, by omission, the ones that are not
- the expected contract: inputs, outputs, error cases
- acceptance criteria written as executable commands

An issue without a context package is an invitation for the agent to invent
one. It will accept the invitation.

### Planning — allocation, not commitment

Planning gains a dimension that does not exist in human Scrum: **model
allocation**. Story by story, the Scrum Master decides who executes — a
cheaper, faster model for mechanical work, a stronger one wherever a design
decision is in play.

Sprint capacity is **how much you can review**, never how much the agents can
produce. Agents will always outproduce a single reviewer; a sprint sized by
agent throughput ends as an unreviewed pile.

### Checkpoint — the daily, by event

A daily standup makes no sense for a team that does not sleep. The daily's real
function was catching impediments early, and here that becomes catching
**loops**.

The checkpoint fires on events, not on a clock:

- an agent finished
- an agent is blocked
- an agent has gone N iterations without turning green

The Scrum Master reads status files. It does not hold a conversation with the
agents — conversation spends the orchestrator's own context, and that is the
one context that has to survive the entire sprint.

### Review — the only synchronous rite

Review is genuinely synchronous, because the bottleneck is the human. Demo the
increment, accept or reject. Everything else in this document can happen while
you sleep. This cannot.

### Retro — must produce a diff

Agents do not learn between sessions. A retrospective whose output is a shared
understanding produces nothing, because there is no head for the understanding
to live in.

The output of a retro is a **diff to a rule file**: `CLAUDE.md`, a subagent
definition, the Definition of Done.

> If the retrospective did not produce a diff, it did not happen.

## Definition of Done

The DoD must be **executable, not descriptive**. "Code reviewed and tested" is
worthless — the agent will mark it done, and it will be sincere.

Replace the prose with commands:

- the test suite passes
- the linter is clean
- the build succeeds
- **the diff touches no file outside the declared context package**

The last one is not a style preference. It is the mechanism that makes scope
drift observable instead of arguable.

QA runs in a **clean context, seeing only the diff and the criteria** — never
the Dev's reasoning. An agent that has read how the code came to be will
approve it. Rationale is persuasive, and that is precisely the problem.

## Artifacts

Scrum has three artifacts. This has a fourth.

1. Product Backlog
2. Sprint Backlog
3. Increment
4. **The rule body** — `CLAUDE.md` plus the subagent definitions

In a human team, learning accumulates in people's heads. Here **the team is the
file**. So the rule body is versioned, reviewed, and has an owner: the Scrum
Master.

## Anti-patterns

**False done.** The most common failure by a wide margin: the agent reports
success on work that does not run. Mitigation: an executable DoD plus
independent QA in a clean context.

**Scope drift.** The agent refactors what nobody asked for and the diff
triples. Mitigation: a diff budget per story, and an SM that rejects any diff
touching files outside the declared context package.

**The Scrum Master writes code.** The orchestrator implements "just this one
small thing", spends its own context, and loses the ability to supervise for
the rest of the sprint. This is the rule most people break, and the one whose
violation is hardest to undo — once the orchestrator's context is gone, the
sprint is over whether or not anybody announces it.

## Roles

| Role | Owns | Never does |
|---|---|---|
| Product Owner | Backlog, context packages, the Ready gate | Implements |
| Scrum Master | Orchestration, model allocation, the rule body | Writes code |
| Dev Senior | Stories carrying a design decision | Estimates alongside the others in a shared context |
| Dev | Mechanical stories inside a defined contract | Widens the contract on its own |
| QA | The verdict against the DoD | Reads the Dev's reasoning |
