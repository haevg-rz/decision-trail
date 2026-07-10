# Plan: harden next-slot numbering with a collision-proof procedure

- Date: 2026-07-10
- Status: done
- Implements: [ADR-0025](../decisions/0025-harden-slot-numbering-with-collision-proof-procedure.md)

## Goal

Carry [ADR-0025](../decisions/0025-harden-slot-numbering-with-collision-proof-procedure.md)
into the method texts. ADR-0025 amends [ADR-0015](../decisions/0015-artifact-numbering-is-ordinal-only.md):
the *rule* (numbers are ordinal, always the next free slot) stays unchanged, but
it gains a reliable **procedure** so the duplicate-number bug (two `0010` ideas,
seen in two repos) cannot recur. Concretely: sharpen the numbering guidance to
`max(existing number) + 1` + existence-check, add **duplicate-number detection**
to the conformance check, and document **insert-and-shift** as the sanctioned way
to slot an out-of-order artifact. Mirror the existing ordinal-numbering guard's
placement (method body + agent-guidance bullet), keep both renderings in sync
(ADR-0014), and ship it as a release whose behavioral migration is "none" (the
sharpened wording reaches adopters via the copy-driven "bring me current" update,
ADR-0022).

## Tasks

- [x] **Canonical method body — slot procedure.** In
      `starter/docs/working-method.md`, at the ordinal-numbering guidance
      (around the "Artifact numbers are **ordinal only**" line), add the
      agent-executable **slot procedure**: (a) **enumerate the whole family**
      (`ideas/`, `decisions/`, `plans/` are independent sequences); (b) take
      **`max(existing number) + 1`** — never the first apparent gap a glob
      surfaces, and never a number derived from a related artifact; (c) **verify
      the target filename is unused** before writing.
- [x] **Canonical agent guidance — slot procedure.** Sharpen the
      ordinal-numbering bullet in the "Agent operating guidance" list of
      `starter/AGENTS.md` (and the repo-root `AGENTS.md`) with the same
      `max+1` + existence-check procedure, cross-referencing ADR-0025.
- [x] **Insert-and-shift guidance.** In the canonical method text (and mirror in
      `AGENTS.md` guidance where appropriate), document the timeline-preserving
      **insert-and-shift** as the sanctioned repair for an out-of-order or
      colliding artifact: renumber the intruder into place, shift every later
      artifact in the family, rewire reciprocal cross-links and prose references,
      and regenerate `overview.md`.
- [x] **Conformance check — duplicate detection.** In `adopting.md`, add a
      **duplicate-number detection** step to the "Conformance check" list (each
      of `ideas/`, `decisions/`, `plans/` has no repeated four-digit number), so
      a collision is caught even if one slips past the procedure. Keep the check
      pure agent do-guidance (no script).
- [x] **Regenerate the derived rendering.** Regenerate the method body of the
      repo-root `AGENTS.md` from `starter/docs/working-method.md` (section `##
      The contract` through `## How to start working`), applying the standard
      deltas (repo-root paths, construction-ADR refs, no provenance citation),
      and carry the sharpened agent-guidance bullet there too. Do **not** touch
      the preamble or the non-derived guidance framing.
- [x] **Provenance bump.** Bumped the `Based on decision-trail vX.Y` citation to
      **v2.10** in both `starter/` renderings (`starter/docs/working-method.md` and
      `starter/docs/guide.md`) and the adopter hand-off `starter/AGENTS.md`.
- [x] **CHANGELOG + release.** Added the ADR-0025 entry to `CHANGELOG.md`
      `## [2.10.0]` (collision-proof slot procedure + duplicate-number conformance
      step + insert-and-shift), with **`Adopter migration: none`**.
- [x] **Regenerate `overview.md`** after all edits are done (idea 0018 →
      `promoted`, ADR-0025 → `accepted`, this plan → state updated).
