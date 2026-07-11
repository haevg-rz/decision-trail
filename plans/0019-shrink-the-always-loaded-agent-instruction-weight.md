# Plan 0019: shrink the always-loaded agent instruction weight

- Date: 2026-07-11
- Status: done
- Implements: [ADR-0029](../decisions/0029-shrink-the-always-loaded-agent-instruction-weight.md)

## Goal

Carry [ADR-0029](../decisions/0029-shrink-the-always-loaded-agent-instruction-weight.md)
into the method texts: state each normative rule **once** in the canonical spec
so the always-loaded `AGENTS.md` stops paying for ~3× restated content every
session (est. ~21 KB → ~13 KB, ~2k tokens/session), with **zero behavioral or
mechanism change**. Per the ADR's accepted **A + C** decision: (a) compact the
canonical spec `starter/docs/working-method.md` — collapse the triple-statement
of each rule (lifecycle section + inline prose) into a single normative
mention, other sections cross-referencing rather than restating; (b)
hand-tighten the non-derived `## Agent operating guidance` block in both
`AGENTS.md` and `starter/AGENTS.md`; (c) audit `guide.md`/`starter/docs/guide.md`
so any nuance being de-duplicated out of the spec is narrated there for the
human reader; then regenerate the derived `AGENTS.md` and `overview.md`. Keep
both renderings in sync (ADR-0014) — the derivation rules stay mechanical,
unchanged (option B rejected). Ship as a release whose behavioral migration is
**"none"** (the compacted wording reaches adopters via the copy-driven "bring me
current" update, ADR-0022).

## Tasks

- [x] **Audit the repetition.** Enumerate every rule stated more than once in
      `starter/docs/working-method.md` (numbering, per-family status, canonical
      header format, title-line format, disentangling procedure, cross-link
      reciprocity, overview refresh, insert-and-shift, …), noting for each the
      single section that should **own** the normative statement and which
      occurrences become cross-references. Do the same census for the repo-root
      `AGENTS.md` (its derived body + the non-derived guidance block).
- [x] **Compact the canonical spec.** In `starter/docs/working-method.md`, state
      each rule once in its owning section; replace the other occurrences with
      terse cross-references. Keep the greppable header-block/title-line
      templates intact (ADR-0026/ADR-0028 depend on them). Preserve all
      behavior, all field names, and the confirmation guard's meaning — this is
      prose tightening, not a semantics change. Optimize agent-first: retain no
      repetition merely for human skimmability (ADR-0029 driver).
- [x] **Audit `starter/docs/guide.md`.** For every rule whose restatement is
      collapsed in the spec, confirm the nuance is already narrated in the
      guide's prose; add prose where it was only implied by the spec's
      repetition, so nothing is lost for the human reader. Mirror any needed
      addition into this repo's `guide.md` if it diverges.
- [x] **Hand-tighten `## Agent operating guidance` (non-derived).** In
      `starter/AGENTS.md` and the repo-root `AGENTS.md`, de-duplicate the
      guidance bullets against the (now single-stated) spec: keep each bullet a
      principle + pointer, dropping full restatements of procedures that the
      spec/`adopting.md` already own. Do **not** weaken the confirmation guard,
      the keep-`overview.md`-current rule, or the guard-free notes.
- [x] **Regenerate the derived rendering.** Regenerate the method body of the
      repo-root `AGENTS.md` from the compacted `starter/docs/working-method.md`
      (section `## The contract` through `## How to start working`), applying the
      standard deltas (repo-root paths, construction-ADR refs, no provenance
      citation, entry-point framing). Do **not** touch the preamble or the
      non-derived `## Agent operating guidance` section (edited by hand above).
- [x] **Verify the size win.** Confirm `AGENTS.md` shrank materially (target
      order ~21 KB → ~13 KB) and that no rule, field name, or status vocabulary
      was dropped — a diff-review pass, not just a byte count.
- [x] **Provenance bump.** Bump the `Based on decision-trail vX.Y` citation to
      **v2.12** in `starter/docs/working-method.md`, `starter/docs/guide.md`, and
      `starter/AGENTS.md`.
- [x] **CHANGELOG + release.** Add a `## [2.12.0]` entry to `CHANGELOG.md`
      describing the compaction (ADR-0029: state each rule once, agent-first
      spec register, guide.md absorbs human-narrative nuance), with **`Adopter
      migration: none`** — the compacted method text reaches adopters via the
      copy-driven "bring me current" update (ADR-0022); no behavioral action
      required.
- [x] **Regenerate `overview.md`** after all edits, and set this plan's status
      `draft` → `active` → `done` as work proceeds (ADR-0029 already
      `accepted`, idea 0021 already `promoted`).
