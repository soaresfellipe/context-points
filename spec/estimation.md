# The context-point scale

A context point is a **budget**, not a forecast. The scale answers one question:

> Does this fit in one session without the agent losing the thread?

| Points | Meaning |
|---|---|
| **1** | One file. The test already exists. No design decision. |
| **2** | A few files. The input/output contract is already defined. |
| **3** | Crosses layers — API plus domain plus persistence. |
| **5** | Requires a design decision, or changes a contract between modules. |
| **8** | Does not fit in one session. Splitting is mandatory. |

**8 is not a size. It is a rejection.** An 8 means the story was never
estimated — it was refused. Split it and estimate the pieces.

There is deliberately no 13, no 20, and no ½. A finer scale invites debate
about numbers, and the numbers are not the point.

## Splitting: choose the axis that reduces context

An 8 must be split, and a split is only real if each piece needs **less
context** than the whole. That is the definition the scale already uses,
applied one level up — so "split it" is not an instruction that has been
followed until you have said *along which axis*.

The axis that fails most often is **surface**. A story can carry one invariant
restated across several surfaces: the same guarantee on two screens, on three
endpoints, in a web and a mobile client. Splitting by surface looks like the
obvious move and reduces nothing — each piece still needs the whole invariant
in context to be written correctly. What it does reduce is the chance the last
surface is ever done, and it hides that reduction: every piece passes its own
acceptance criteria while the guarantee is false on the surface nobody named.

**Split by state, not by surface.** If the pieces would each restate the same
invariant, it is one story, and the acceptance criteria enumerate the states —
every state, on every surface, in one list.

An 8 that cannot be split along a context-reducing axis is a signal that the
invariant itself is too broad. Narrow the guarantee, not the surface.

This is the *false done* anti-pattern one level up: not an agent reporting work
it did not do, but a split reporting coverage it never had. The mitigation has
the same shape — criteria that enumerate what would be false if the work were
incomplete.

### Observed

A story fixed a display-versus-persistence invariant on the path the story
named. It passed. The same invariant was found alive on the neighbouring path
in the next verification pass, then a third time in a field nobody had named.
Re-work reached roughly two thirds of that story's total cost, and the cause
was not difficulty — the final fix was a boolean clause. The follow-up story
kept all four surfaces together and listed eight states as acceptance criteria.
It was verified in one pass, with the two defects that came back sitting in
neither the invariant nor the states, but in data availability and a missing
CSS rule.

One project, one story. The generalisation worth testing elsewhere:
**re-work is the cost of splitting on the wrong axis, and it appears in the
estimate of neither piece.**

### What this costs elsewhere

Keeping four surfaces in one story widens its declared file list by
construction, so `the diff touches no file outside the context package` is a
weaker scope-drift signal for exactly this shape of work. The declared list
still has to be exhaustive — it simply catches less here, and the states in the
acceptance criteria are what carry the weight instead.

## The second dimension: verifiability

Size and verifiability are independent. A 1-point story can be unverifiable,
and a 5-point story can be perfectly verifiable.

Ask: **can "done" be proven with a command?**

- **Yes** → it is a story. Record the command as an acceptance criterion.
- **No** → it is a **spike**. A spike is not sized on this scale and produces
  no increment. Its only deliverable is the set of criteria that make the real
  story verifiable.

"Improve error handling" is a spike wearing a story's clothes. "`pytest
tests/test_errors.py::test_timeout_returns_504` passes" is a story.

## Blind estimation protocol

The point of the ritual is detecting ambiguity, not producing a number.

1. The Product Owner, the Dev Senior and QA each estimate the same story.
2. Each runs in a **clean context**. None of them sees another's answer, and
   none of them sees another's reasoning.
3. Compare:

| Spread | Meaning | Action |
|---|---|---|
| All three agree | The story is understood | Ready |
| One step apart | Normal noise | Take the highest, proceed |
| More than one step | **The spec is ambiguous** | Back to refinement |

Never average. An average hides the disagreement, and the disagreement was the
only signal the exercise produced.

If the three roles run in the same session, they will converge by anchoring on
whoever answered first. The estimate then looks like consensus and contains no
information. **Isolation is not an optimisation here — it is the mechanism.**

### Mark an estimate that was not blind

An estimate produced in the same session that refined the story is not blind,
whatever the protocol says — the estimator has already seen the work. This
happens legitimately: a story gets refined and sized in one pass because
splitting the pass would cost another session.

**Record it as non-blind on the story.** It stays useful as calibration for its
class of work, and it must not be counted as a hit or a miss when the scale is
reviewed. An unmarked non-blind estimate that lands exactly on target is worse
than a miss: it is evidence of nothing, presented as the scale working.

## Calibration

The table above is calibrated against a Python and TypeScript codebase of
moderate size, with fast tests and a working linter. It will drift on stacks
that differ, notably:

- languages with slow or flaky test suites, where a 2 behaves like a 5
- monorepos where "one file" pulls in generated code
- codebases without tests, where nearly everything is a spike

Calibration data from other stacks is the single most useful contribution this
project can receive. If the scale is wrong for yours, open a PR describing the
story, the points you assigned, and what actually happened.
