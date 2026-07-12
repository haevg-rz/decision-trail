# Plan 0026: carry ADR-0037 into the method — plans are mechanical execution, questions return to the decision stage

- Date: 2026-07-12
- Status: done
- Implements: [ADR-0037](../decisions/0037-plans-are-mechanical-execution-questions-return-to-the-decision-stage.md)

## Goal

Land what ADR-0037 accepted: harden the method texts so a plan is understood as
**mechanical execution only** — it never contains a decision-making task — and a
question that surfaces during execution **returns to the decision stage** (clarify
/ patch / amend the governing ADR, or open a new one), then execution resumes.
The mechanic is fixed; the *sizing* of the return (patch vs. amend vs. new ADR)
stays a judgment call. ADR-0004 is amended, not rewritten (the `Amended by:`
back-link is already in place).

Per ADR-0037's placement decision, the change lands in three layers: the spec
body, the agent-guidance checklist, and the guide narrative.

## Sync rules (constraints on the edits below)

Three distinct sync regimes are in play; treat each correctly:

1. **Derived method body** (§ *The contract* → § *How to start working*).
   `starter/docs/working-method.md` is **canonical**; this repo's `AGENTS.md`
   method body is **derived** and regenerated wholesale with declared deltas
   (ADR-0014, ADR-0032): repo-root paths (`plans/`, not `docs/plans/`),
   construction-ADR citations added. Edit the canonical spec's **plans bullet**
   in § *The lifecycle*, then regenerate the matching bullet in `AGENTS.md`'s
   derived body — do **not** hand-diverge them beyond the deltas.

2. **Agent operating guidance checklist** — **not** derived; **hand-authored,
   audience-forked** (ADR-0032). `starter/AGENTS.md` is adopter-facing (section
   references only, **no construction-ADR citations**); this repo's `AGENTS.md`
   is method-home (same bullet **with** an `ADR-0037` citation). Edit **both**;
   do not regenerate one from the other.

3. **Guide** (narrative). `guide.md` (repo, repo-root paths) and
   `starter/docs/guide.md` (adopter, `docs/`-prefixed paths) each get the same
   brief note, in their own path rendering. Edit **both**.

## Tasks

### Spec body — canonical (`starter/docs/working-method.md`)

- [x] In § *The lifecycle*, extend the **Plans** bullet so it states, beyond
      "the ADR is the spec, the plan is the *how*": a plan is for **mechanical
      execution only** and **never contains a decision-making task** (no
      "decide X" / "clarify Y"); if a part still depends on an undecided
      question, the plan is not yet ready for that part. Add the escalation: a
      question surfacing during execution **returns to the decision stage** —
      clarify / patch / amend the governing ADR, or open a new one — then resume;
      *that* it returns is fixed, *which* form it takes is judgment sized to the
      question.

### Spec body — derived (`AGENTS.md`, this repo)

- [x] Regenerate the matching **Plans** bullet in `AGENTS.md`'s derived method
      body from the canonical text, applying the declared deltas (repo-root
      `plans/` paths; add the `(ADR-0037)` construction-ADR citation in the
      decision-trail-repo rendering style). Do not touch the non-derived preamble
      or the § *Agent operating guidance* section here.

### Agent-guidance checklist (audience-forked — edit both)

- [x] `starter/AGENTS.md`: add a "Follow the spec's mechanics" bullet —
      **Plans are mechanical execution** — a plan task is never "decide X" /
      "clarify Y"; a question surfacing during execution returns to the decision
      stage (clarify / patch / amend the ADR, or open a new one), then resume
      (§ *The lifecycle*). **No** ADR citation (adopter delta).
- [x] this repo's `AGENTS.md`: add the same bullet **with** the construction-ADR
      citation `(§ *The lifecycle*; ADR-0037)`, matching the existing bullets'
      style.

### Guide narrative (edit both renderings)

- [x] `guide.md` (repo): in the **Plan** / **Execution** narrative, add a brief
      note that a plan is the mechanical *how* and holds no "decide this" tasks;
      if a question comes up mid-execution you step back to the ADR to settle it,
      then resume. Repo-root paths.
- [x] `starter/docs/guide.md`: add the same note in the adopter rendering
      (`docs/`-prefixed paths).

### Reconcile the index

- [x] Regenerate `overview.md` wholesale from the artifact headers (picks up
      idea 0031 `promoted`, ADR-0037 `accepted`, this plan, and the new
      ADR-0037 → Plan 0026 sub-index row). Re-stamp "as of <date>".

## Verification

- [x] `grep` confirms the hardened rule ("mechanical execution" / "never … decide"
      / return-to-decision-stage) appears in `starter/docs/working-method.md`'s
      Plans bullet **and** in `AGENTS.md`'s derived Plans bullet, differing only
      by the declared deltas (paths, ADR-0037 citation).
- [x] `grep` confirms the new checklist bullet is present in **both** `AGENTS.md`
      files — **without** an ADR citation in `starter/AGENTS.md` and **with** the
      `ADR-0037` citation in this repo's `AGENTS.md` (audience delta preserved).
- [x] `grep` confirms the guide note is present in **both** `guide.md` and
      `starter/docs/guide.md`, each in its own path rendering.
- [x] Confirm the non-derived parts (this repo's `AGENTS.md` preamble and
      § *Agent operating guidance*, other than the intended new checklist bullet)
      were not disturbed.
- [x] `overview.md` rows for idea 0031, ADR-0037, and plan 0026 match their
      headers, and the ADR-0037 → Plan 0026 sub-index row is present under
      ADR-0004's amendment context.

## Notes

- Scope is the **method text** only (spec body, checklist, guide) plus the
  `overview.md` reconcile. Cutting a decision-trail **release** (version bump,
  `CHANGELOG.md` entry with an `Adopter migration:` line per ADR-0021/ADR-0022)
  is separate downstream work. If released, the migration is a **behavioral
  change** — adopters should re-read the plans rule — and is worth an explicit
  `Adopter migration:` line, unlike the "none" case.
- No artifact back-migration: ADR-0004 stands (amended, not rewritten); existing
  plans are unaffected. This is a forward-looking rule for how plans are authored.
