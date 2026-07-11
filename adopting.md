# Adopting decision-trail in your own repo

This is the **on-ramp**. It is the single place that tells you how to start using
decision-trail — and how to keep it up to date — in *your* project. It covers three
scenarios:

1. [**Fresh repo**](#1-fresh-repo) — start a new repo directly with the method.
2. [**Inject into an existing repo**](#2-inject-into-an-existing-repo) — add the
   method to a repo that already has code and history.
3. [**Update**](#3-update-xy--xyn) — move an adopting repo from one version of
   decision-trail to a newer one.

> This document lives in the **decision-trail standard repo**
> (https://github.com/haevg-rz/decision-trail), not in your repo. Your repo carries a
> `Based on decision-trail vX.Y` citation that points back here; come back to this
> page whenever you need to (re)adopt or upgrade.

## Preconditions

You need only two things:

1. **A git repo** — local or hosted, it makes no difference. decision-trail is plain
   markdown under version control.
2. **An agentic setup** — you work with an agent and your preferred harness. Every
   agent knows how to handle an `AGENTS.md`, which is the method's entry point, so
   there is no harness-specific wiring to do. You can also follow every step below
   by hand.

Everything below is **plain do-guidance**: steps you (or your agent) follow. No tool
is required — the migration steps in particular are written so your agent can
execute them directly.

---

## 1. Fresh repo

Goal: a near-empty repo becomes a decision-trail repo in one move.

1. **Copy the contents of [`starter/`](starter/) into your repo root.** You get:
   - `AGENTS.md` — the method entry point (the "How we work" + "Agent operating
     guidance" blocks);
   - `docs/working-method.md` (the terse spec) and `docs/guide.md` (the narrative
     intro);
   - empty `docs/ideas/`, `docs/decisions/`, `docs/plans/` families,
     `docs/overview.md`, `docs/travel-diary.md`, and `docs/intermediate-artifacts/`;
   - a seed decision `docs/decisions/0001-adopt-decision-trail.md`.
2. **Fill in the placeholders:**
   - In `AGENTS.md`, replace the `# <project name>` heading with your project's name
     and a one-line description.
   - In `docs/decisions/0001-adopt-decision-trail.md`, set the `Date:` and replace
     `vX.Y` with the version you copied (see the citation in
     `AGENTS.md` / `docs/working-method.md`).
3. **Commit.** Your repo now owns its artifacts and its own ADR log starting at
   `0001`. It never inherits the decision-trail standard repo's construction ADRs.

That's it. Capture your first idea in `docs/ideas/`, and work the lifecycle from
there (see `docs/guide.md`).

---

## 2. Inject into an existing repo

Goal: add the method to a repo that already has code and history, **without
disturbing anything already there.**

It is the **Fresh repo** steps above with two small differences:

1. **Copy `starter/docs/` into your repo's `docs/`** (not the starter root over your
   root). This adds the method text, the three empty families, `overview.md`,
   `travel-diary.md`, and `intermediate-artifacts/` — and touches none of your
   existing files. (Keep docs elsewhere than `docs/`? Adjust paths consistently.)
2. **The one real delta — `AGENTS.md`:**
   - **No `AGENTS.md` yet?** Create it from `starter/AGENTS.md` (fill in the
     project name).
   - **Already have one?** Keep it and **append** the `## How we work` and
     `## Agent operating guidance` blocks from `starter/AGENTS.md` verbatim (adjust
     the version in the citation). Don't hand-merge the method body — it lives in
     `docs/working-method.md`; `AGENTS.md` only points at it.

Then, exactly as in Fresh repo: keep `docs/decisions/0001-adopt-decision-trail.md`
(set its `Date:` and version), and commit. Your decision-trail ADR log starts fresh
at `0001` and never inherits this standard repo's construction ADRs; your prior
history and any existing `0001` elsewhere coexist untouched.

---

## 3. Update `X.Y → X.Y+n`

Goal: pull a newer version of decision-trail into an already-adopting repo cheaply
and safely. In the best case it is a no-op; otherwise it is a small, explicit
migration.

**You don't run the steps by hand — your agent does.** Since an agentic setup is a
precondition, updating is a single spoken intent. Tell your agent to update the
method, and give it two things:

- **the source** — a path or URL to the **target version** of this standard repo
  (the version you want to move *to*); and
- **the how-to** — the path to that version's
  [`updating.agent.md`](updating.agent.md), the terse agent procedure that does the
  work.

> **Example prompt:**
> *"Update the method from `<path/URL-to-target>`. The how-to is
> `<path/URL-to-target>/updating.agent.md`."*

Your agent then reads your current version from the `Based on decision-trail vX.Y`
citation, follows `updating.agent.md` (re-copy the method-owned set with the
preserve rule, apply required migrations in order, bump the citation, regenerate
`docs/overview.md`, run the conformance check, record a bump ADR, commit), and does
it as **one transparent batch under the confirmation guard**: it states the plan,
waits for your green light, executes, and pauses only where a step needs your
judgment.

**Why name the how-to file explicitly?** Bootstrap. A repo on an *older* version has
no in-repo knowledge that this procedure exists — so the prompt hands the agent the
entry point directly. It never depends on prior knowledge in your repo.

The full step-by-step (the preserve rule, migration ordering, citation bump, and
the conformance check) lives in [`updating.agent.md`](updating.agent.md) — a single
operational source of truth, not duplicated here.

---

## Conformance check

After an update — or any time you want to confirm your repo still matches the method
it cites — your agent can run the **conformance check**. It is **pure agent
do-guidance** (no script): the six-point checklist lives with the update procedure
in [`updating.agent.md`](updating.agent.md#conformance-check), and verifies that
headers are present and canonical, numbers don't collide, title lines match
filenames, `docs/overview.md` is in sync, and the `Based on decision-trail vX.Y`
citation is consistent across `docs/working-method.md` and the `AGENTS.md`
`## How we work` block.

---

## Why there's no adoption tool

There isn't a script to run, and that's deliberate. Every step above is either a
plain copy, a small edit, or — for the update procedure in
[`updating.agent.md`](updating.agent.md) — a task written so your **agent** can
carry it out directly (backfilling headers, regenerating `overview.md`, adding
back-links). Since an agentic setup is a precondition, the agent already *is* the
tool; a static script would only duplicate trivial copying and couldn't know about
future releases' migrations anyway.

> A future release may offer this repo as a GitHub *template* for a one-click
> "Use this template" start (recorded as a deferred option in ADR-0008). That is a
> platform convenience, not method tooling.
