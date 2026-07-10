# Plan: make the per-family status vocabulary explicit and guarded

- Date: 2026-07-10
- Status: done
- Implements: [ADR-0024](../decisions/0024-status-vocabulary-guard-per-family.md)

## Goal

Carry [ADR-0024](../decisions/0024-status-vocabulary-guard-per-family.md) into
the method texts: state each family's **entry status** in words, add a
**per-family exclusivity guard** (never borrow another family's status), and
prescribe the "name the family first, then pick from its list only" heuristic —
so the cross-family status mistake that prompted the ADR cannot recur. Mirror the
placement of the existing ordinal-numbering guard (method body + agent-guidance
bullet), keep both renderings in sync (ADR-0014), and ship it as a release whose
`Adopter migration:` is "none" (pure documentation change; new wording arrives
via the copy-driven update, ADR-0022).

## Tasks

- [ ] **Canonical method body.** In `starter/docs/working-method.md`, in the
      "The lifecycle" section, add — beneath the status-values table — a short
      prose guard: (a) the **entry status** for each family (new idea → `seed`,
      new proposal → `proposed`, new plan → `draft`; decision/execution are
      in-place continuations with no separate entry status); (b) the
      **exclusivity rule** (a status is drawn only from the artifact's own
      family — an idea is never `proposed`/`draft`/`accepted`/…; a plan is never
      `proposed`/`seed`; a proposal is never `seed`/`draft`); (c) the **heuristic**
      (name the family first, then pick from that family's list only).
- [ ] **Canonical agent guidance.** Add a matching one-bullet guard to the
      "Agent operating guidance" list (the canonical copy lives in
      `starter/AGENTS.md` and, for this repo, the repo-root `AGENTS.md`), in the
      same spirit as the ordinal-numbering bullet.
- [ ] **Regenerate the derived rendering.** Regenerate the method body of the
      repo-root `AGENTS.md` from `starter/docs/working-method.md` (section `##
      The contract` through `## How to start working`), applying the standard
      deltas (repo-root paths, construction-ADR refs, no provenance citation),
      and add the agent-guidance bullet there too. Do **not** touch the preamble
      or the non-derived guidance framing.
- [ ] **Skeleton hand-off file.** Check `starter/AGENTS.md`; if it carries the
      lifecycle/agent-guidance guidance, add the entry-status + exclusivity guard
      there as well so adopting repos inherit it.
- [ ] **Optional table annotation.** Decide whether to mark the *initial* value
      in the lifecycle table's status column (e.g. bolding `seed`/`proposed`/
      `draft`) or leave the table as-is and rely on the prose guard. Apply the
      chosen form consistently across both renderings.
- [ ] **Provenance bump.** If cutting a new version, bump the `Based on
      decision-trail vX.Y` citation in both `starter/` renderings
      (`starter/docs/working-method.md` and `starter/docs/guide.md`) and the
      adopter `AGENTS.md` "How we work" block to the new version.
- [ ] **CHANGELOG + release.** Add a new `## [X.Y.0]` entry to `CHANGELOG.md`
      recording ADR-0024 (per-family status guard), with an **`Adopter migration:
      none`** line (documentation/guardrail clarification only — the new wording
      reaches adopters via the copy-driven "bring me current" update; no
      behavioral change to any state machine).
- [ ] **Regenerate `overview.md`** after all edits are done (idea 0016 →
      `promoted`, ADR-0024 → `accepted`, this plan → `done`).
