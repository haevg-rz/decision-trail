# Changelog

All notable changes to **decision-trail** (the method) are recorded here. The method is
versioned with semver; adopting projects cite the version they copied (ADR-0008).

The format is loosely based on [Keep a Changelog](https://keepachangelog.com/).

## [2.2.0] - 2026-06-29

### Added
- ADR-0015 — artifact numbers are **ordinal only**: always assign the next free
  slot in the target family (`ideas/`, `decisions/`, `plans/` are independent
  sequences). Numbers carry no relational meaning; relationships live exclusively
  in cross-link fields (`Implements:`, `Promoted to:`, etc.). Rule added to
  `AGENTS.md`, `starter/docs/working-method.md`, and `starter/AGENTS.md` so it
  is visible to agents in every context.

### Changed
- ADR-0016 — the `overview.md` regeneration trigger changes from *"after every
  artifact change"* to **"on explicit user request only"**. The "as of <date>"
  stamp makes staleness visible; eliminating automatic regeneration honours
  promise #2 (Economy). Rule updated in `AGENTS.md`, `starter/docs/working-method.md`,
  and `starter/AGENTS.md`.

## [2.1.0] - 2026-06-28

### Added
- ADR-0014 — the method text is split into **three registers** (idea 0006): a
  didactic human **guide** (`docs/guide.md`), a terse **reference/spec**
  (`docs/working-method.md`), and an **agent operating guidance** block. The
  `starter/` skeleton gains `docs/guide.md`, and `starter/AGENTS.md` now carries
  the agent operating guidance (confirmation guard, keep-overview-current, method
  settled) — closing a gap where adopting projects' agents received none.

### Changed
- ADR-0014 also **single-sources the spec**: `starter/docs/working-method.md` is
  canonical, and this repo's `AGENTS.md` (plus this repo's `guide.md`) are derived
  renderings, regenerated wholesale with an enumerated set of allowed deltas
  (paths, construction-ADR links, citation, entry-point framing) recorded in
  header sync notes. Amends ADR-0007 (re-frames the single source of truth) and
  ADR-0010 (splits the method body). This repo's `README.md` is slimmed to a thin
  human landing page pointing at `guide.md` and `AGENTS.md`.
  Minor bump: additive and backward-compatible — the provenance citation string is
  unchanged, and existing adopters are not broken.

## [2.0.0] - 2026-06-28

### Changed

- ADR-0013 — the method is renamed from **the-way** to **decision-trail**
  (idea 0005). The provenance citation string becomes `Based on decision-trail vX.Y`;
  the canonical repo URL becomes https://github.com/ckluth/decision-trail.
  All live method surfaces updated: `AGENTS.md`, `README.md`,
  `.github/copilot-instructions.md`, `starter/` skeleton (including the seed
  adoption ADR renamed to `0001-adopt-decision-trail.md`). Historical artifacts
  (ideas, ADRs, plans 0001–0012) retain the old name as a dated record.
  Major bump because the citation string is adopter-visible (ADR-0008).

## [1.4.0] - 2026-06-28

### Added
- ADR-0011 — `overview.md`, a derived status index over all ideas, decisions,
  and plans (name / creation date / state). It is regenerated wholesale from the
  artifact headers as a dated "as of" snapshot — produced on explicit user
  request and as part of the agent's definition of done — rather than
  hand-patched. Keeping it current is the agent's responsibility, never the
  user's. The `starter/` skeleton gains `docs/overview.md`.

### Changed
- ADR-0011 also makes a `Date:` (creation date) header field **mandatory** for
  ideas and plans (ADRs already carried one); it is the source for the
  overview's *Created* column. Amends ADR-0005. Existing idea files were
  backfilled.
- ADR-0012 — the promotion link becomes **reciprocal**: an ADR gains a
  `Promoted from:` header pointing back to its founding idea, mirroring the
  idea's `Promoted to:`. Establishes the criterion that a cross-link is made
  reciprocal only when both ends are single and write-once (so `Parent` and
  `Implements`, whose reverse side accumulates, stay forward-only). Amends
  ADR-0005. Existing promotion targets ADR-0008 and ADR-0011 were backfilled.

## [1.2.0] - 2026-06-28

### Changed
- ADR-0010 — adopters keep the full method text in `docs/working-method.md`;
  the adopter's `AGENTS.md` carries only a fixed `## How we work` pointer (the
  same in every repo). Pins down the previously-undefined merge text and closes
  a circular reference (`AGENTS.md` → `0001` → `AGENTS.md`) that left the method
  text nowhere. Amends ADR-0009. The `starter/` skeleton moves its method body
  to `starter/docs/working-method.md`.

## [1.1.0] - 2026-06-28

### Changed
- ADR-0009 — adopting projects use conventional, unbranded locations
  (`docs/decisions/` for ADRs, plus `docs/ideas/`, `docs/plans/`); the branded
  `the-way/` subfolder is dropped. Amends ADR-0005 and ADR-0008. The `starter/`
  skeleton is restructured to `AGENTS.md` + `docs/{ideas,decisions,plans}/`.

## [1.0.0] - 2026-06-28

First settled release of the method. The full lifecycle is mechanized in plain
markdown, every choice borrowed from an existing standard and recorded as an ADR.

### Added
- ADR-0001 — record decisions as ADRs (`decisions/`).
- ADR-0002 — capture ideas as small markdown files (`ideas/`).
- ADR-0003 — a proposal is an ADR in the `proposed` status.
- ADR-0004 — a plan carries a decision into action (`plans/`); execution is the
  plan in motion.
- ADR-0005 — repo layout and cross-linking conventions.
- ADR-0006 — `AGENTS.md` as the tool-agnostic entry point.
- ADR-0007 — `AGENTS.md` as the single source of truth; concept phase settled.
- ADR-0008 — adopt the-way via a copied `starter/` skeleton; version this repo
  as the standard.
