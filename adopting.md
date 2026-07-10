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
> (https://github.com/ckluth/decision-trail), not in your repo. Your repo carries a
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

Goal: drop the method into a repo that already has content, **without disturbing
anything that is already there**.

1. **Copy `starter/docs/` into your repo's `docs/`.** This adds `working-method.md`,
   `guide.md`, the three empty families, `overview.md`, `travel-diary.md`, and
   `intermediate-artifacts/`. It touches none of your existing files. (If you keep
   docs somewhere other than `docs/`, adjust the paths consistently — the method is
   about the artifacts, not the exact folder name.)
2. **Wire up `AGENTS.md`:**
   - If your repo has **no** `AGENTS.md`, create it from `starter/AGENTS.md`
     (fill in the project name/description placeholder).
   - If your repo **already has** an `AGENTS.md`, keep it and **append** the two
     blocks below verbatim — the `## How we work` pointer block and the
     `## Agent operating guidance` block from `starter/AGENTS.md`. Do not hand-merge
     the method body; it lives in `docs/working-method.md`, and `AGENTS.md` only
     points at it.

   The pointer block to append looks like this (adjust the version):

   ```markdown
   ## How we work

   This project follows **decision-trail** — a generic method for carrying a thought
   through its whole life (idea → proposal → decision → plan → execution) in plain
   markdown. New here? Start with the guide in [`docs/guide.md`](docs/guide.md). The
   terse reference is [`docs/working-method.md`](docs/working-method.md); decision
   records live in [`docs/decisions/`](docs/decisions/), starting with
   [`0001-adopt-decision-trail.md`](docs/decisions/0001-adopt-decision-trail.md).

   Based on decision-trail vX.Y — https://github.com/ckluth/decision-trail
   ```
3. **Seed the adoption decision.** Keep `docs/decisions/0001-adopt-decision-trail.md`,
   set its `Date:`, and record the version you copied. Your pre-existing history and
   any prior decisions coexist untouched: the decision-trail ADR log starts **fresh
   at 0001** and never inherits the standard repo's construction ADRs. (If your repo
   already uses `0001` for something else in the same folder, put decision-trail's
   ADRs in `docs/decisions/` so the sequences don't collide.)
4. **Commit.** From here it is identical to a fresh repo.

---

## 3. Update `X.Y → X.Y+n`

Goal: pull a newer version of decision-trail into an already-adopting repo cheaply
and safely. In the best case it is a no-op; otherwise it is a small, explicit
migration.

1. **Find your current version.** Read the `Based on decision-trail vX.Y` citation
   in your `AGENTS.md` (and `docs/working-method.md`). That is the anchor.
2. **Re-copy the method-owned set** from the target version's `starter/`, so your
   repo lands in the exact shape a *fresh* adopter of the target would have
   ("bring me current"). Overwrite the **method text and templates** with the
   target's `starter/docs/` copies — `working-method.md`, `guide.md`, and any
   companion scaffolds the target ships (e.g. `travel-diary.md`,
   `intermediate-artifacts/`). Because these scaffolds live in `starter/`,
   re-copying lands new additive companions **automatically** — you never have to
   hunt a changelog for "what files got added."

   **Preserve rule — copy method text/templates, preserve project content.** The
   method-owned set is exactly `starter/`'s own contents (it is the source of
   truth; there is no separate manifest to drift). Everything your project
   *authored* is **never** overwritten:
   - `docs/decisions/`, `docs/ideas/`, `docs/plans/` (your artifacts);
   - a populated `docs/travel-diary.md` and `docs/intermediate-artifacts/`;
   - `docs/overview.md` (regenerated, not copied).

   Rule of thumb: if `starter/` ships it as *method text or an empty scaffold*, copy
   it; if your repo *filled it with project content*, keep yours.
3. **Bump the citation.** Update the `Based on decision-trail vX.Y` citation to the
   target version in **both** `docs/working-method.md` and the `## How we work`
   block of `AGENTS.md`.
4. **Apply the release migrations.** In this standard repo's
   [`CHANGELOG.md`](CHANGELOG.md), each release carries an **`Adopter migration:`**
   note stating the **required behavioral changes** for that version. Read the notes
   for every version **between your old version and the target** and apply them **in
   order**. Each is written as steps an agent can execute — for example: *"backfill
   any missing `Date:` header on ideas and plans, then regenerate
   `docs/overview.md`."* When a note says **"none"**, there is nothing required for
   that version (new optional scaffolds already arrived via step 2).
5. **Regenerate `docs/overview.md`** from the artifact headers.
6. **Run the conformance check** (below) to confirm the update landed cleanly.
7. **Record the bump.** Add a short ADR in your own `docs/decisions/` noting that you
   moved to the new version (the method text is copied, not referenced, so the bump
   is a decision worth recording).
8. **Commit.**

---

## Conformance check

After an update — or any time you want to confirm your repo still matches the method
it cites — run this quick check. It is **pure agent do-guidance**: there is no
script, your agent verifies each point directly.

1. **Headers present.** Every artifact in `docs/ideas/`, `docs/decisions/`, and
   `docs/plans/` carries the mandatory `Date:` header (and a `Status:`).
2. **No duplicate numbers.** Within each family (`docs/ideas/`, `docs/decisions/`,
   `docs/plans/`) every four-digit number appears exactly once — no two artifacts
   share a slot. If a collision exists, fix it with insert-and-shift (renumber the
   intruder into place, shift every later artifact, rewire cross-links and prose
   references) and regenerate `docs/overview.md`.
3. **Header format canonical.** Every artifact's header fields use the canonical
   bulleted form — a `# Title` line, a blank line, then `- Date:` / `- Status:`
   and any cross-link / `- Tags:` fields, each on its own `-`-prefixed line. Flag
   any bare (bullet-less) header and fix it, so the overview refresh can't
   silently drop the artifact.
4. **Overview in sync.** `docs/overview.md` matches the artifact headers — same
   names, dates, and states — and is stamped with a current "as of" date. If not,
   regenerate it.
5. **Citation consistent.** The `Based on decision-trail vX.Y` citation is identical
   in `docs/working-method.md` and the `## How we work` block of `AGENTS.md`.

If all five hold, the repo conforms to the version it cites.

---

## Why there's no adoption tool

There isn't a script to run, and that's deliberate. Every step above is either a
plain copy, a small edit, or — for the update migrations — a task written so your
**agent** can carry it out directly (backfilling headers, regenerating
`overview.md`, adding back-links). Since an agentic setup is a precondition, the
agent already *is* the tool; a static script would only duplicate trivial copying
and couldn't know about future releases' migrations anyway.

> A future release may offer this repo as a GitHub *template* for a one-click
> "Use this template" start (recorded as a deferred option in ADR-0008). That is a
> platform convenience, not method tooling.
