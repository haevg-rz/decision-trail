# Changelog

All notable changes to **decision-trail** (the method) are recorded here. The method is
versioned with semver; adopting projects cite the version they copied (ADR-0008).

The format is loosely based on [Keep a Changelog](https://keepachangelog.com/).

**Release-author rule (ADR-0021, refined by ADR-0022):** every release **must**
carry an **`Adopter migration:`** line stating the **required behavioral changes** an
already-adopting repo must perform to take this version — **even when it is "none."**
Write it as steps an agent can execute (e.g. "backfill any missing `Date:` header,
then regenerate `overview.md`"). **New optional scaffolds are not listed here** — they
reach adopters automatically via the copy-driven "bring me current" update. This is
the contract the [`adopting.md`](adopting.md) update path relies on.

## [2.9.0] - 2026-07-10

### Added
- ADR-0024 — **per-family status vocabulary guard** (idea 0015): the method texts
  now state each family's **entry status** in words (a new idea starts `seed`, a
  new proposal `proposed`, a new plan `draft`) and add an **exclusivity guard** —
  a status is drawn only from the artifact's own family, never borrowed from
  another (an idea is never `proposed`/`draft`; a plan is never `proposed`/`seed`;
  a proposal/decision is never `seed`/`draft`) — mirroring the ordinal-numbering
  guard's placement (method body + agent-guidance bullet). Applied to both
  renderings (`starter/docs/working-method.md` + `AGENTS.md`) and the starter
  hand-off file (`starter/AGENTS.md`).

### Changed
- Both `starter/` renderings bump their provenance citation to **v2.9**.

**Adopter migration: none.** This is a documentation/guardrail clarification with
no behavioral change to any state machine; the new wording reaches adopters
automatically via the copy-driven "bring me current" update (ADR-0022).

## [2.8.0] - 2026-07-05

### Added
- ADR-0023 — **promote and teach the method** (idea 0014): the guide is reworked
  from a narrative introduction into a **didactical tutorial** — it motivates the
  problem before the mechanics, introduces the lifecycle progressively, and walks
  one canonical worked example (*"add a dark-mode toggle to a small web app"*) from
  a first idea through proposal, decision, plan, and execution. Two **Mermaid
  diagrams** (rendered natively by GitHub) visualize the lifecycle stages + status
  transitions and the cross-link vocabulary. Applied to **both** guide renderings
  (`guide.md` and `starter/docs/guide.md`).

### Changed
- Both `starter/` renderings bump their provenance citation to **v2.8**.

- **Adopter migration:** none — additive documentation only. The reworked
  `starter/docs/guide.md` reaches you automatically via the copy-driven "bring me
  current" update (ADR-0022). No behavioral change is required.

## [2.7.0] - 2026-07-04

### Added
- ADR-0022 — **copy-driven "bring me current"** (idea 0013): updating an adopter to
  a target version now **re-copies the method-owned set** (exactly `starter/`'s
  contents) into the adopter's `docs/`, so additive scaffolds (travel diary,
  `intermediate-artifacts/`) arrive **automatically** without per-release
  file-addition bookkeeping. A **preserve rule** (copy method text/templates,
  preserve project content) protects the artifact families, a populated
  `travel-diary.md`, `intermediate-artifacts/`, and `overview.md` from being
  overwritten. The method-owned set is `starter/` itself — no separate manifest to
  drift.
- A **conformance check** in [`adopting.md`](adopting.md) — pure agent do-guidance,
  no tool — that verifies mandatory `Date:` headers, `overview.md` in sync with the
  artifact headers, and a consistent `Based on decision-trail vX.Y` citation across
  `docs/working-method.md` and the `AGENTS.md` "How we work" block. It runs at the
  end of an update or any time on request.

### Changed
- `adopting.md` §3 (Update) rewritten from note-driven ("replace two files") to the
  copy-driven procedure above, closing with the conformance check.
- The **release-author rule** is clarified: `Adopter migration:` states **required
  behavioral changes only** (still "none" when apt); new optional scaffolds are not
  enumerated there. Updated in `CHANGELOG.md`'s intro and this repo's `AGENTS.md`
  agent operating guidance.
- The forward pointer in `starter/docs/working-method.md` is strengthened into a
  durable, version-carried breadcrumb to `adopting.md` (covering "bring me current"
  and the conformance check); both `starter/` renderings bump their provenance
  citation to **v2.7**.
- ADR-0022 **amends** ADR-0021 (reciprocal `Amends:`/`Amended by:` cross-links).

- **Adopter migration:** none — additive; adopter-facing update guidance and a
  clarified release-author rule only. Optionally re-run the new conformance check to
  confirm your repo matches the version it cites.



### Added
- ADR-0021 — a single adopter **on-ramp** (idea 0004): a top-level
  [`adopting.md`](adopting.md) that walks an agent (or a human) through all three
  ways of using decision-trail in a repo — **fresh** (copy `starter/`), **inject**
  into an existing repo (non-destructive drop-in of `starter/docs/` + append the
  fixed `## How we work` pointer block; the decision-trail ADR log starts fresh at
  0001 and existing history is untouched), and **update** `X.Y → X.Y+n` (replace
  the copied method text, bump the citation, and apply each release's
  `Adopter migration:` steps in order). Delivered as **pure do-guidance** (Option
  D): no adoption tool ships, because the agentic precondition means the agent
  already executes the copy/edit and migration steps — a script would only
  duplicate trivial copying and can't know future migrations.
- A **release-migration contract**: every `CHANGELOG.md` entry now carries an
  **`Adopter migration:`** line — **even when "none"** — as agent-executable steps,
  so the `adopting.md` update path always knows what work a version entails. The
  rule is recorded in this CHANGELOG's intro and in this repo's `AGENTS.md` agent
  operating guidance, and every existing release entry has been backfilled with its
  migration line.

### Changed
- `starter/docs/working-method.md` gains a forward pointer to the standard repo's
  `adopting.md` (for update/(re)adopt guidance), and both `starter/` renderings
  bump their provenance citation to **v2.6**.

- **Adopter migration:** none — additive; new adopter-facing guidance and optional
  tooling only. (You may re-copy `docs/working-method.md` to pick up the new
  `adopting.md` pointer, and bump your citation to v2.6.)

## [2.5.0] - 2026-07-03

### Added
- ADR-0020 — **intermediate artifacts** (idea 0012): an optional, informal
  `intermediate-artifacts/` folder that gives the *execution* stage a scratch
  persistence layer for material a plan gathers along the way (data, findings,
  intermediate outputs) to work on later, across steps or sessions. It is the
  execution-stage counterpart to the human-facing travel diary: it sits **outside
  the lifecycle and cross-link vocabulary**, is explicitly **not a source of truth**
  (so its drift is harmless), is **internally unstructured** (organization is the
  project's business), and is maintained **guard-free** — creating/using/deleting
  files needs no ADR, no plan, and no confirmation guard. It is **committed by
  default** so gathered material survives across machines and sessions (a repo may
  gitignore it), and is **left to rot harmlessly** once a plan is done. A plan may
  carry an informal forward-only prose pointer for findability (not a formal
  cross-link). The method ships the **mechanism + a documented-but-empty
  `starter/docs/intermediate-artifacts/` folder** (purpose `README`); this home repo
  seeds its own `intermediate-artifacts/`. Documented in
  `starter/docs/working-method.md` (new **Intermediate artifacts** section + layout
  entry), rendered into this repo's `AGENTS.md`, noted as a guard-free exception in
  the agent operating guidance (this repo and `starter/AGENTS.md`), and mentioned in
  both `guide.md` renderings. Provenance citation bumped to v2.5. Minor/additive bump
  — repos without the folder are unchanged.

- **Adopter migration:** none — additive; the `intermediate-artifacts/` folder is
  optional. Take the new method text if you want the mechanism documented.

## [2.4.0] - 2026-07-03

### Added
- ADR-0018 — the **travel diary** (idea 0010): an optional, human-facing companion
  file (`travel-diary.md`) that narrates the journey in loose, newest-first prose —
  *where we are / what we achieved / what is left / what is next* — so a human
  catching up reads one short entry instead of synthesizing across `overview.md`,
  the active plan, and recent ADRs. It is the human-facing counterpart to the
  machine-facing overview: authored/prose/narrative vs. derived/terse/state. The
  diary is **self-describing** (carries its own agent-instructions header), sits
  **outside the lifecycle and cross-link vocabulary**, is explicitly **not a source
  of truth** (so its drift is harmless), and is maintained **guard-free** — "add a
  chapter" is a light-weight task with no ADR, no plan, and no confirmation guard.
  The method ships the **mechanism + a `starter/docs/travel-diary.md` template**;
  unlike the project-specific `Tags:` vocabulary, this home repo **dogfoods a live
  `travel-diary.md`**. Documented in `starter/docs/working-method.md` (new **Travel
  diary** section + layout entry), rendered into this repo's `AGENTS.md`, noted as a
  guard-free exception in the agent operating guidance (this repo and
  `starter/AGENTS.md`), and mentioned in both `guide.md` renderings. Provenance
  citation bumped to v2.4. Minor/additive bump — repos without a diary are unchanged.

- **Adopter migration:** none — additive; `travel-diary.md` is optional.

## [2.3.0] - 2026-07-03

### Added
- ADR-0017 — an optional **`Tags:`** header field (idea 0009) plus a derived
  `Tags` column in `overview.md`, re-slicing artifacts along a cross-cutting
  theme axis so parallel threads stay findable without an O(n) read. The method
  ships only the **mechanism and governance rule** (recommended-but-not-enforced,
  **curated per repo**) — no content vocabulary, since tags name a *project's*
  themes (Genericity #7). Documented in `starter/docs/working-method.md` (new
  **Tags** section + refresh procedure), rendered into this repo's `AGENTS.md`,
  and mentioned in both `guide.md` renderings; the `starter/` skeleton carries an
  empty "recommended tags" placeholder and this repo defines none. A filtered
  by-tag view is explicitly deferred. Minor/additive bump — existing artifacts
  without a `Tags:` line are unchanged.

- **Adopter migration:** none — additive; the `Tags:` field is optional.

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

- **Adopter migration:** none — behavioral rules only; no artifact changes
  required. (Optionally adopt the new numbering and overview-regeneration habits.)

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

- **Adopter migration:** copy the new `docs/guide.md` from the starter, and append
  the `## Agent operating guidance` block from `starter/AGENTS.md` to your
  `AGENTS.md`; refresh the `## How we work` pointer block (it now points at
  `docs/guide.md` as well as `docs/working-method.md`).

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

- **Adopter migration:** rename references from "the-way" to "decision-trail" on
  your *live* surfaces — update the provenance citation string to
  `Based on decision-trail vX.Y` and the repo URL, and rename the seed adoption ADR
  to `0001-adopt-decision-trail.md`. Historical artifacts may keep the old name as a
  dated record.

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

- **Adopter migration:** backfill a `Date:` (creation date) header on every idea
  and plan (ADRs already carry one); create `docs/overview.md` by regenerating it
  wholesale from the artifact headers; and add reciprocal `Promoted from:`
  back-links on any ADR promoted from an idea.

## [1.2.0] - 2026-06-28

### Changed
- ADR-0010 — adopters keep the full method text in `docs/working-method.md`;
  the adopter's `AGENTS.md` carries only a fixed `## How we work` pointer (the
  same in every repo). Pins down the previously-undefined merge text and closes
  a circular reference (`AGENTS.md` → `0001` → `AGENTS.md`) that left the method
  text nowhere. Amends ADR-0009. The `starter/` skeleton moves its method body
  to `starter/docs/working-method.md`.

- **Adopter migration:** move the method body out of your `AGENTS.md` into
  `docs/working-method.md`, and reduce `AGENTS.md` to the fixed `## How we work`
  pointer block (same in every repo).

## [1.1.0] - 2026-06-28

### Changed
- ADR-0009 — adopting projects use conventional, unbranded locations
  (`docs/decisions/` for ADRs, plus `docs/ideas/`, `docs/plans/`); the branded
  `the-way/` subfolder is dropped. Amends ADR-0005 and ADR-0008. The `starter/`
  skeleton is restructured to `AGENTS.md` + `docs/{ideas,decisions,plans}/`.

- **Adopter migration:** move your artifacts out of the branded `the-way/`
  subfolder into conventional `docs/` locations (`docs/ideas/`, `docs/decisions/`,
  `docs/plans/`).

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

- **Adopter migration:** none — first release.
