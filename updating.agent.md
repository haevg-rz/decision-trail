# `updating.agent.md` — how an agent brings an adopter repo current

**You are an AI agent updating a repo that already uses decision-trail to a newer
version of the method.** This file is the *operational* procedure — terse,
executable steps. It assumes **you know nothing about the method beyond what your
prompt and this file say**, so it works even when the repo you are updating predates
this mechanism (bootstrap: the human's prompt hands you both the source and this
file's path).

- **Human-facing on-ramp:** [`adopting.md`](adopting.md) — the narrative, and the
  one-line human trigger that points here.
- **Why it works this way:** [`decisions/0022-*`](decisions/) (the copy-driven
  contract) and [`decisions/0031-*`](decisions/) (the human-intent / agent-execution
  split). This file is the *steps*; those ADRs are the *rationale*. Do not duplicate
  the steps back into `adopting.md`.

## Inputs you are given

The human triggers an update with intent plus an explicit **source** — e.g.
*"update the method from `<path/URL>`; the how-to is `<path/URL>/updating.agent.md`."*

- **`<source>`** — a path or URL to the **target version** of the decision-trail
  standard repo (the version to update *to*). **Never guess the target or fetch a
  "latest" on your own** — if the source or target version is unclear, ask.

## How to run it — one transparent batch under the confirmation guard

Do **not** silently auto-apply, and do **not** nag step-by-step. Instead:

1. **State the resolved plan** and wait for **one green light**: the adopter's
   current version (from the citation, step 1 below) → the named target; which
   releases' `Adopter migration:` notes will apply; and what you will re-copy and
   regenerate.
2. **Execute the whole batch** (steps below) after the green light.
3. **Pause only** where a step needs genuine human judgment — a non-trivial
   `Adopter migration:` note, or a preserve-conflict you cannot resolve
   mechanically.
4. **Close** by recording the version-bump ADR and reporting the conformance-check
   result.

## Procedure

1. **Read the adopter's current version.** Find the `Based on decision-trail vX.Y`
   citation in the adopter's `docs/working-method.md` (and the `AGENTS.md` "How we
   work" block). That is the anchor version you are updating *from*.

2. **Re-copy the method-owned set** from `<source>`'s `starter/` into the adopter's
   `docs/` locations, overwriting those files — this lands the adopter in the exact
   shape a *fresh* adopter of the target would have ("bring me current"). This
   copies the method **text and templates** (`working-method.md`, `guide.md`, and
   any companion scaffolds the target ships, e.g. `travel-diary.md`,
   `intermediate-artifacts/`). Because additive scaffolds live in `starter/`,
   re-copying lands new companions **automatically** — no changelog hunt for "what
   files were added."

   **Preserve rule — copy method text/templates, preserve project content.** The
   method-owned set is exactly `starter/`'s own contents (the single source of
   truth; there is no separate manifest). **Never overwrite what the project
   authored:**
   - `docs/decisions/`, `docs/ideas/`, `docs/plans/` (the artifact families);
   - a populated `docs/travel-diary.md` and `docs/intermediate-artifacts/`;
   - `docs/overview.md` (regenerated in step 5, not copied).

   Rule of thumb: if `starter/` ships it as *method text or an empty scaffold*, copy
   it; if the repo *filled it with project content*, keep theirs. (If a file is a
   shipped scaffold in `starter/` but the adopter has populated it — a filled
   `travel-diary.md` is the common case — **preserve the adopter's**; that is a
   preserve-conflict to resolve in the project's favor, and to surface if unsure.)

3. **Apply required migrations, in version order.** In `<source>`'s
   [`CHANGELOG.md`](CHANGELOG.md), each release carries an **`Adopter migration:`**
   note stating the **required behavioral changes** for that version. Read the notes
   for every version **between the adopter's current version and the target** and
   apply them **in order**. Each is written as agent-executable steps (e.g.
   *"backfill any missing `Date:` header on ideas and plans, then regenerate
   `docs/overview.md`"*). When a note says **"none"**, there is nothing required for
   that version — new optional scaffolds already arrived via step 2.

4. **Bump the citation** to the target version in **both** places:
   `docs/working-method.md` and the `## How we work` block of `AGENTS.md`.

5. **Regenerate `docs/overview.md`** from the artifact headers (a fresh dated
   snapshot; never hand-patched).

6. **Run the conformance check** (below) to confirm the update landed cleanly, then
   **record a short ADR** in the adopter's own `docs/decisions/` noting the bump to
   the new version, and **commit**.

## Conformance check

Runs at the end of an update, and may be invoked any time to confirm a repo still
matches the version it cites. Pure do-guidance — **no script**; verify each point
directly.

1. **Headers present.** Every artifact in `docs/ideas/`, `docs/decisions/`, and
   `docs/plans/` carries the mandatory `Date:` header (and a `Status:`).
2. **No duplicate numbers.** Within each family, every four-digit number appears
   exactly once. Fix a collision with insert-and-shift (renumber the intruder into
   place, shift every later artifact, rewire cross-links and prose references) and
   regenerate `docs/overview.md`.
3. **Header format canonical.** Every header uses the canonical bulleted form — a
   `# Title` line, a blank line, then `- Date:` / `- Status:` and any cross-link /
   `- Tags:` fields, each on its own `-`-prefixed line. Fix any bare (bullet-less)
   header so the overview refresh can't silently drop the artifact.
4. **Title line matches filename.** Every `# Title` line is typed and zero-padded to
   its filename slot, naming the family — `# Idea 0017: …`, `# ADR-0017: …`,
   `# Plan 0017: …`. Fix any title-line ordinal that disagrees with (or omits) its
   filename ordinal.
5. **Overview in sync.** `docs/overview.md` matches the artifact headers — same
   names, dates, and states — and is stamped with a current "as of" date. If not,
   regenerate it.
6. **Citation consistent.** The `Based on decision-trail vX.Y` citation is identical
   in `docs/working-method.md` and the `## How we work` block of `AGENTS.md`.

If all six hold, the repo conforms to the version it cites.
