# Context Points

**Scrum for AI agent teams.**

In human Scrum the scarce resource is time. When the team is made of agents,
time is nearly free — an agent retries ten times overnight. What stays scarce
is **context** and **your attention as the reviewer**. Every rule in this
methodology derives from that one substitution.

> Status: **v0.1.0**, calibrated on a small number of projects. Counter-examples
> are more useful to this project than endorsements — see
> [CONTRIBUTING.md](CONTRIBUTING.md).

## Install

```
/plugin marketplace add soaresfellipe/context-points
/plugin install context-points@context-points
```

Add the marketplace **by repository** (`owner/repo`), not by a direct URL to
`marketplace.json` — the plugin is referenced by a relative path, which only
resolves when Claude Code has the whole repo.

## What you get

Five roles as subagents, six rites as slash commands, and the methodology as
two skills.

| Command | Rite |
|---|---|
| `/refinement` | Build the context package; the Ready gate |
| `/estimate` | Blind estimation across three isolated contexts |
| `/planning` | Select stories and allocate a model to each |
| `/checkpoint` | The daily, replaced by loop detection |
| `/review` | Demo the increment to the human |
| `/retro` | Produce a diff to a rule file |

| Subagent | Model | Owns |
|---|---|---|
| `product-owner` | Opus | Backlog, context packages, the Ready gate |
| `scrum-master` | Opus | Orchestration, model allocation, the rule body |
| `dev-senior` | Opus | Stories carrying a design decision |
| `dev` | Sonnet | Mechanical stories inside a defined contract |
| `qa` | Opus | The verdict against the Definition of Done |

## The three ideas

**A story point is a context budget, not an effort estimate.** The scale
answers "does this fit in one session without the agent losing the thread?".
An 8 is not a size — it is a refusal, and splitting is mandatory.

**Planning poker detects ambiguity, and only works blind.** The Product Owner,
the Dev Senior and QA estimate the same story in separate clean contexts. A
spread greater than one step means the spec is ambiguous, and the story goes
back to refinement. Never average. Run them in one session and they converge by
anchoring, producing a number that contains no information.

**The Definition of Done is a list of commands.** "Code reviewed and tested" is
worthless — the agent will mark it done, sincerely. The tests pass, the linter
is clean, the build succeeds, and the diff touches no file outside the declared
context package. QA verifies in a clean context, seeing the diff and the
criteria but never the developer's reasoning, because rationale is persuasive.

There is also a fourth artifact. Scrum has three; agents do not learn between
sessions, so the team's accumulated learning has to live somewhere. It lives in
`CLAUDE.md` plus the subagent definitions — versioned, reviewed, owned by the
Scrum Master. Hence the rule that a retrospective which did not produce a diff
did not happen.

## What this is not

Three different things get called "agile with AI", and they have opposite
constraints. Advice about one does not transfer to the others.

| | Who is the team | Who is the human | The hard problem |
|---|---|---|---|
| Agents joining a human team | Humans, with agents as members | A teammate | Trust, handoff, accountability |
| Ceremony automation | Humans | The whole team | Summarising, nudging, reporting |
| **Context Points** | **Agents** | **Stakeholder and reviewer** | **Context budget, verifiable done** |

This project assumes the third case. The context-isolation rules would be
meaningless in the other two — you cannot ask a human developer to forget how
they solved something.

## Repository layout

The repo is both the marketplace and the plugin.

```
.claude-plugin/marketplace.json    generated — the entry point Claude Code reads
spec/                              source of truth: the methodology
  SPEC.md                          the methodology itself
  estimation.md                    the point scale and blind protocol
  manifest.json                    plugin metadata
  roles/                           five role definitions
  rites/                           six rite definitions
adapters/claude-code/...           generated — the installable plugin
tools/build.py                     spec/ -> adapters/
docs/QUICKSTART.md                 first sprint, end to end
```

**Do not edit anything under `adapters/` or `.claude-plugin/` by hand.** Edit
`spec/`, then run `python3 tools/build.py`. CI regenerates and fails the build
if the committed output differs.

Only three paths are fixed by Claude Code: `.claude-plugin/marketplace.json` at
the repo root, `.claude-plugin/plugin.json` inside the plugin folder, and skills
as a directory containing `SKILL.md` (a loose `skills/name.md` is not read).
Everything else here is our own choice.

The spec is embedded into the skill files rather than linked, because a plugin
is copied into a local cache on install and a relative path out of the plugin
folder resolves to nothing on the user's machine.

## Documentation

- [docs/QUICKSTART.md](docs/QUICKSTART.md) — running the first sprint
- [spec/SPEC.md](spec/SPEC.md) — the methodology
- [spec/estimation.md](spec/estimation.md) — the scale and the blind protocol
- [CONTRIBUTING.md](CONTRIBUTING.md) — what this project needs most

## License and trademark

MIT — see [LICENSE](LICENSE).

"Scrum" is used here descriptively, to describe an adaptation of a widely known
framework. This is an independent project with no affiliation to, endorsement
by, or sponsorship from Scrum Alliance, Scrum.org, or Scrum Inc. It offers no
training and no certification of any kind.
