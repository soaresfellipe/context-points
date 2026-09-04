# Quickstart — your first sprint

This walks one story from raw idea to accepted increment. Expect the first
sprint to expose gaps in your context packages; that is the point.

## Before you start

```
/plugin marketplace add soaresfellipe/context-points
/plugin install context-points@context-points
```

You also need a `CLAUDE.md` in the project. It is the fourth artifact, and it
starts nearly empty — the retro fills it.

## 1. Refine

```
/refinement Add a rate limit to the public search endpoint
```

The Product Owner returns a context package: the file list, the contract, and
acceptance criteria as commands. Read the criteria first. If any of them is
prose rather than a command, refinement is not finished.

A useful early check: could someone who has never seen this codebase run the
criteria and tell whether the story is done? If not, the agent cannot either.

## 2. Estimate

```
/estimate <the refined story>
```

Three isolated estimates come back. What matters is the spread:

- agreement, or one step apart → proceed
- more than one step → the spec is ambiguous; go back to `/refinement`

Resist averaging. The disagreement is the whole output.

## 3. Plan

```
/planning Ship rate limiting on the public API
```

The Scrum Master selects Ready stories and assigns an executor per story —
`dev` for mechanical work, `dev-senior` where a design decision is in play.

When it asks how much you can review, answer honestly. Sprint capacity is your
review bandwidth, not agent throughput. A sprint sized by what the agents can
produce ends as a pile nobody reads.

## 4. Execute and checkpoint

Run the stories. Then, on each event rather than on a schedule:

```
/checkpoint
```

The three events that matter: an agent finished, an agent is blocked, or an
agent has gone several iterations without turning green. The third is a loop,
and a loop is a spec problem — send that story back to refinement instead of
retrying it.

## 5. Review

```
/review sprint 1
```

The only synchronous rite. You watch the acceptance commands run, and you
accept or reject each story. Record the reason for every rejection; it is input
for the retro.

## 6. Retro

```
/retro sprint 1
```

This is where the sprint pays for itself. The output must be a **diff** to
`CLAUDE.md`, to a subagent definition, or to your Definition of Done.

If the retro ends in a list of intentions, nothing survives — agents do not
learn between sessions.

## What usually breaks first

**Context packages are too thin.** The agent touches files nobody declared. Fix
in refinement, not by widening the budget after the fact.

**A false done reaches review.** The Definition of Done was descriptive
somewhere. Replace that line with a command.

**The orchestrator starts coding.** The most damaging and least obvious
failure: once the Scrum Master implements "just one small thing", it has spent
the context it needed to supervise, and the rest of the sprint drifts.
