# ADR-0017: An optional `Tags:` axis for cross-cutting navigation

- Date: 2026-07-03
- Status: accepted
- Promoted from: [Idea-0009](../ideas/0009-cross-cutting-concerns-have-no-home.md)

## Context

Idea 0009 diagnosed a gap: as decisions and parallel threads grow, the
**cross-cutting** aspects of the work have no navigable home. Reconstructing
"everything touching adoption / cross-linking / rendering-sync" means reading
`decisions/` in order (O(n)). The idea's own framing concluded the felt gap is
largely **navigational**, not conceptual — the content already lives in ADRs and
the cross-link graph; what is missing is a *view* that re-slices existing
artifacts along a shared-theme axis.

Of the idea's four candidate directions, the hand-authored `spine.md` (candidate
4) was rejected in the framing itself: authored synthesis drifts the moment any
decision changes, reintroducing the disease the *derived* `overview.md` was
designed to cure (ADR-0011). This ADR takes **candidate 2** — a derived theme
axis — in its lightest possible form.

## Decision drivers

- **Navigation:** make cross-cutting threads findable without an O(n) read.
- **Economy (#2):** add as little as possible — no new artifact family, no new
  lifecycle, ideally one optional field.
- **Transparency (#3):** stay plain, greppable markdown, like the existing
  cross-link fields (`Implements:`, `Promoted to:`).
- **Genericity (#7):** the *method* must ship nothing project-specific. Tags name
  a project's recurring themes, so a fixed content vocabulary cannot be generic —
  the method ships only the mechanism and governance rule; the vocabulary is
  authored per repo.
- **Derived, never authored (ADR-0011):** whatever surfaces in `overview.md` must
  come from artifact headers via wholesale regeneration — zero synthesis, zero
  hand-patching, so it cannot drift.
- **Agility (#5) / no consequence:** the mechanism must be safe to ignore and
  safe to *mis*use — over-tagging or vague tags may reduce a tag's usefulness but
  must never break, spoil, or complicate the trail.

## Considered options

1. **No spine — record the rejection (candidate 1).** Cheapest; declares
   `decisions/` in order to be the spine. Rejected: it leaves the real
   navigational gap open.
2. **Optional `Tags:` axis (candidate 2) — chosen.** One optional header field,
   surfaced as a derived column. Closes the navigation gap at minimal cost.
3. **A single "principles" ADR as one front door (candidate 3).** A spine inside
   the existing vocabulary. Not mutually exclusive with tags, but does not give a
   *cross-slice* view; deferred, can still be authored later as an ordinary ADR.
4. **Hand-authored `spine.md` (candidate 4).** Rejected in the idea's framing —
   authored synthesis drifts against ADR-0011.

### Governance of the vocabulary

A sub-choice within option 2: should the tag set be a **fixed controlled
vocabulary**, **free-form**, or a **recommended-but-not-enforced** list?

- Fixed/controlled maximizes findability but needs curation and can *reject*
  work — a consequence we explicitly do not want.
- Free-form is zero-consequence but fragments (`sync` / `syncing` /
  `rendering-sync`), degrading the very view it exists to provide.
- **Recommended-but-not-enforced** is the middle path and the choice: a short
  vocabulary documented in one place to align on, with off-list tags always
  allowed. Misuse is possible but carries no structural consequence.

Crucially, that vocabulary is **per repo, not part of the method** (Genericity
#7): tags name a *project's* recurring themes, which the method cannot know. The
method ships the mechanism and the governance rule; each repo authors its own
recommended vocabulary.

## Decision

Introduce an **optional `Tags:` axis** across all three artifact families.

- **`Tags:` header field.** Ideas, decisions, and plans may carry an optional
  `Tags:` line — comma-separated tag words. The field is omitted when empty.
- **The method ships the mechanism, not a vocabulary.** The method spec
  (`starter/docs/working-method.md`, rendered per ADR-0014) documents the
  `Tags:` field and the governance rule — *recommended-but-not-enforced, curated
  per repo* — but ships **no content tags**. Each adopting repo authors its own
  recommended vocabulary in *its* method text. The `starter/` skeleton carries an
  **empty vocabulary section** with a one-line instruction ("list your project's
  recurring themes here"), not example tags.
- **This repo keeps its own vocabulary empty.** decision-trail's home repo needs
  no tags of its own; it documents the mechanism but defines no vocabulary and
  applies no tags, avoiding demo pollution. A real vocabulary is expected to live
  in adopting repos that have the need.
- **Governance: recommended, not enforced.** Off-list tags are always allowed and
  nothing rejects them. Over-tagging or vague tags reduce a tag's usefulness but
  have **no structural consequence** — the trail is never spoiled.
- **Derived `Tags` column in `overview.md`.** The three overview tables gain a
  `Tags` column, populated by the existing wholesale regeneration from artifact
  headers (ADR-0011). No synthesis, no hand-patching. The refresh procedure
  additionally reads the `Tags:` header line.
- **A filtered/by-tag view is explicitly deferred.** Tagging makes a "by theme"
  filtered view *possible later*; this ADR does not build it. It remains a future
  option, opened but not taken.

This is additive and safe to ignore: an artifact with no `Tags:` line behaves
exactly as today, and its overview row simply has an empty `Tags` cell.

## Consequences

- The navigational gap from idea 0009 is closed with a single optional field:
  cross-cutting threads become findable by tag (grep the field, or scan the
  overview column) without an O(n) read (Economy #2, Transparency #3).
- The method stays generic (#7): it ships the tagging *mechanism* only, so a
  fixed content vocabulary is never imposed on adopters. Real vocabularies live
  where the need is — in adopting repos.
- Nothing about the existing lifecycle, cross-link vocabulary, or artifact
  families changes; the `Tags:` axis is orthogonal to `Implements:` /
  `Promoted to:` / `Amends:` etc.
- The overview stays a derived, drift-proof snapshot (ADR-0011): the new column
  is regenerated from headers like every other cell.
- Because the vocabulary is recommended, not enforced, the mechanism honors
  Agility (#5) and cannot be *mis*used into harm — the worst case is a less
  useful tag, never a broken or spoiled trail.
- A future filtered/by-tag view is enabled but out of scope here; if pursued it
  would be its own decision.
- On acceptance, a plan will: document the `Tags:` field and the
  recommended-but-not-enforced, curated-per-repo governance rule in
  `starter/docs/working-method.md` (shipping no content tags); add an empty
  vocabulary section to the `starter/` skeleton; regenerate the derived method
  body in `AGENTS.md` (ADR-0014) with this repo's vocabulary left empty; add the
  `Tags` column to the overview tables and its refresh procedure; and ship the
  change in `CHANGELOG.md`.
