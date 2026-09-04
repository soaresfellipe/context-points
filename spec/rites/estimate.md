---
name: estimate
title: Blind estimation
summary: Estimate a story in three isolated contexts to detect ambiguity. Divergence greater than one step sends the story back to refinement.
argument-hint: [issue number or story description]
---

Estimate this story: $ARGUMENTS

The purpose is **detecting ambiguity**, not forecasting. Divergence means the
story means different things to different readers.

## Protocol

Dispatch the same story to three subagents — `product-owner`, `dev-senior` and
`qa` — **in separate, clean contexts**. Each returns one number and one
sentence.

Critical: none of them may see another's answer or reasoning. Do not summarise
one response into another's prompt, and do not run them as a discussion. If
they share a context they converge by anchoring, and the estimate carries no
information whatsoever.

## Scale

| Points | Meaning |
|---|---|
| 1 | One file, test exists, no design decision |
| 2 | A few files, contract already defined |
| 3 | Crosses layers — API, domain, persistence |
| 5 | Requires a design decision or changes a contract |
| 8 | Does not fit in one session — split it |

## Verdict

| Spread | Action |
|---|---|
| All three agree | Ready |
| One step apart | Take the highest and proceed |
| More than one step | **Back to refinement** — the spec is ambiguous |
| Any 8 | Split the story; report the proposed split |

Never average the three numbers. The average hides the disagreement, and the
disagreement was the only signal produced.

Report each estimate with its justification, then the verdict.
