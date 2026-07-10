# Plan: carry the `decomposed` idea status into the method

- Date: 2026-07-10
- Status: done
- Implements: [ADR-0027](../decisions/0027-a-decomposed-status-for-a-budded-parent-idea.md)

## Goal

Carry [ADR-0027](../decisions/0027-a-decomposed-status-for-a-budded-parent-idea.md)
into the method texts: add `decomposed` to the **idea** family's status
vocabulary, reframe `seed` as "not yet promoted" (so a standing budding parent
sits there honestly), and state the fixed **disentangling pattern** for breaking a
large idea into a parent + budded children. Keep both method renderings in sync
(ADR-0014), extend the ADR-0024 per-family status guard to the new word, and ship
it in the open `2.10.0` release with `Adopter migration: none` (additive
vocabulary; new wording arrives via the copy-driven update, ADR-0022).

Two design principles govern the split of work — the ADR's placement rule made
concrete:

- **Principle 1 — the guide must stay a good human-advisor, never overloaded.**
  The guide gets *gentle narrative* only: `decomposed` added to the status line,
  and a short, friendly paragraph on "when an idea grows too big, bud it apart and
  mark the parent `decomposed`." **No procedures, no checklists, no edge-case
  machinery** in the guide.
- **Principle 2 — the method body + agent-guidance carry precise agentic
  instruction.** The *fixed procedure* (parent → `decomposed`; each axis buds 1:1;
  reasons documented in the parent; agent proposes, human decides; strategy stays
  free) lives in the terse method body and a crisp agent-guidance bullet, worded so
  an agent can execute it without re-reasoning.

## Tasks

- [x] **Canonical method body — vocabulary + `seed` reframe.** In
      `starter/docs/working-method.md`, "The lifecycle" section: change the idea
      row of the status-values table to `seed` → `promoted` / `dropped` /
      `decomposed`. Beneath the table, in the existing status prose, (a) add a
      one-line gloss of `decomposed` — a *rare, alternative finalized* state: the
      idea broke into budded children and its content moved out; it says nothing
      about the children's fate (told by *their* statuses); hand-curated and
      reversible (#5); and (b) reframe `seed` as "not yet promoted," explicitly
      permitting a standing parent map that is still budding to sit at `seed`
      honestly.
- [x] **Canonical method body — extend the ADR-0024 status guard.** In the same
      file's per-family exclusivity paragraph, add `decomposed` to the **idea**
      family's own list (so the guard reads it as a legitimate idea status), and
      confirm it is never borrowed by another family. Do not weaken the existing
      guard wording.
- [x] **Canonical method body — the disentangling pattern (precise, Principle 2).**
      Add a short passage (near budding / promise #6, or the lifecycle) stating the
      **fixed procedure**: a large idea decomposes into a *parent* + *budded
      children* (`Parent:`); the parent becomes `decomposed`; each child promotes
      1:1 to its own ADR (multi-promotion is *not* the tool — promotion is 1:1,
      ADR-0012); **the reasons for the branching are documented in the parent
      idea**; one status per idea (no stacking `promoted` + `decomposed`). State
      plainly that the **procedure is fixed but the strategy is free** — whether to
      promote an already-decidable core first or bud everything is a judgment call
      decided in conversation — and that **the agent may propose the disentangling
      while the responsible unit is the human.**
- [x] **Canonical agent guidance — one precise bullet (Principle 2).** Add a bullet
      to the "Agent operating guidance" list in the repo-root `AGENTS.md` and the
      starter hand-off `starter/AGENTS.md`, in the spirit of the existing
      status-vocabulary bullet: name `decomposed` as the idea family's alternative
      finalized state for a fully-budded parent map, hand-curated and reversible,
      and point at the fixed disentangling procedure (parent → `decomposed`, axes
      bud 1:1, reasons in the parent, agent proposes / human decides).
- [x] **Regenerate the derived rendering (repo-root `AGENTS.md`).** Regenerate the
      method body (section `## The contract` through `## How to start working`)
      from `starter/docs/working-method.md`, applying the standard deltas
      (repo-root paths, construction-ADR refs, no provenance citation). Do **not**
      touch the preamble or the non-derived `## Agent operating guidance` framing
      beyond adding the one new bullet above.
- [x] **Guide — gentle human advice, both renderings (Principle 1).** In `guide.md`
      and `starter/docs/guide.md`: update the lifecycle Mermaid status line from
      `seed → promoted / dropped` to `seed → promoted / dropped / decomposed`, and
      add **one short, friendly paragraph** — when an idea grows too big to be one
      thought, you bud it into child ideas and mark the parent `decomposed` (its
      substance now lives in the children; follow the `Parent:` links). Keep it
      narrative and reassuring; **no procedure, no edge cases** — those live in the
      method body.
- [x] **CHANGELOG.** Add an `### Added` entry for ADR-0027 under the open
      `## [2.10.0]` section (the `decomposed` idea status + disentangling pattern;
      amends ADR-0024's vocabulary). Include an **`Adopter migration: none`** line
      — additive vocabulary with no reinterpretation of existing artifacts (no
      `seed` becomes `decomposed` retroactively); the new wording and the extra
      permitted status reach adopters via the copy-driven "bring me current" update
      (ADR-0022).
- [x] **Provenance bump (shared with the release).** Bumped to **v2.10** in both
      `starter/` renderings (`starter/docs/working-method.md`,
      `starter/docs/guide.md`) and the adopter `starter/AGENTS.md` "How we work"
      block, shared once with plans 0015/0016.
- [x] **Regenerate `overview.md`.** After all edits, regenerate the derived index
      (idea 0017 → `promoted`, ADR-0027 → `accepted` — already reflected — and this
      plan → `done`), and re-stamp "As of".

## Follow-up (make the concept prominent in the human guide)

Raise the *concept* — "an idea need not be atomic; it may be a bundle of
entangled ideas" — from a footnote of the mechanism to a prominent statement **in
the human guide** (`guide.md` + `starter/docs/guide.md`). Guide-only; the
machine-facing method texts are left untouched.

- [x] **Edit 1 — idea stage, both guides.** At first contact with the idea stage,
      state plainly that an idea is often a *knot of entangled ideas* and needn't be
      untangled up front; it can bud per thread with the original `decomposed`.
- [x] **Edit 2 — budding promise #6, both guides.** Extend the promise to name the
      entanglement motivation ("a knot of entangled ideas can bud into one child
      per thread").
- [x] **Edit 3 — tighten the later paragraph, both guides.** Reframe the existing
      budding paragraph as *mechanism* (the concept now leads up front), opening
      "Budding is the mechanism behind the *knot of entangled ideas* mentioned
      earlier."
- [x] **Re-close.** Set this plan back to `done`; `overview.md` unchanged (already
      reflects idea 0017 `promoted`, ADR-0027 `accepted`, plan 0017 `done`).
- [x] **Promote budding to its own guide section (both renderings).** Pull the
      buried paragraph out of "The vocabulary of links" into a new top-level
      section **"Budding: when an idea is really several"**, placed right after the
      lifecycle section. Vocabulary section reverts to link *fields* only.
