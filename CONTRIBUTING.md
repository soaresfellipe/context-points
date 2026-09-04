# Contributing

The most valuable thing you can send this project is a **counter-example**.

Context Points is v0.1.0 and calibrated on a small number of projects. The
methodology is plausible; the numbers are not yet trustworthy. What it needs is
evidence from stacks that differ from the one it grew in.

## What is most wanted

**Calibration of the point scale.** The scale is tuned against a Python and
TypeScript codebase with fast tests and a working linter. It will drift
elsewhere. If a story sized 2 blew up into a 5, open an issue or a PR with:

- the story, roughly as it was written
- the points assigned, and by which roles
- what actually happened — files touched, iterations, whether it turned green
- the stack: language, test runtime, monorepo or not, tests present or absent

Even one honest data point is useful. A pattern across three is worth a change
to the scale.

**Rites that did not survive contact.** If a rite produced nothing but
ceremony in your setup, say so. A rule that does not trace back to context or
to reviewer attention should be deleted, and deletions are welcome PRs.

**Anti-patterns we have not named.** The three in the spec are the ones seen
repeatedly. There are certainly more.

## How to change the methodology

Edit `spec/`, never `adapters/`.

```bash
# edit spec/SPEC.md, spec/estimation.md, spec/roles/*, spec/rites/*
python3 tools/build.py
git add -A
```

`adapters/` and `.claude-plugin/marketplace.json` are generated. CI runs
`python3 tools/build.py --check` and fails if the committed output does not
match the spec, so a hand-edit of a generated file will break the PR. That is
deliberate — the same logic as the executable Definition of Done in the spec
itself: a rule that cannot be violated observably is decoration.

The build needs only Python 3.11+ from the standard library. There is nothing
to install.

## Adding a role or a rite

1. Add a file to `spec/roles/` or `spec/rites/` with the frontmatter the
   existing ones use — `name`, `model` and `summary` for a role; `name`,
   `summary` and optionally `argument-hint` for a rite.
2. Run `python3 tools/build.py`.
3. Commit both the spec file and the generated output.

Roles map to subagents and rites map to slash commands, so the `name` becomes a
user-visible identifier. Choose it carefully.

## Releases

`version` is declared in `spec/manifest.json` and flows into both
`plugin.json` and `marketplace.json`.

**Bump it on every release.** Claude Code caches an installed plugin by
version: ship a change without a bump and everyone who already installed keeps
the cached copy. (The alternative is to drop the field entirely and let the
commit SHA serve as the version — this project keeps the field and bumps it.)

## Scope

Pull requests that add a new adapter — another agent runtime under
`adapters/` — are welcome, provided the methodology in `spec/` stays runtime
agnostic. If a change to `spec/` only makes sense for one runtime, it belongs
in that adapter instead.
