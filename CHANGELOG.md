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

## [2.18.1] - 2026-07-17

**Adopter migration:** **Required if you took v2.18.** v2.18 introduced the optional
overview-regeneration script at `docs/scripts/regen-overview.ps1`, meant to arrive
automatically via the copy-driven "bring me current" re-copy. A real adopter update
missed it — the agent anchored on step 2's example list (which omitted `scripts/`)
instead of the "copy everything under `starter/`" instruction, so the `docs/scripts/`
subtree was silently skipped. To remediate: re-run the step-2 re-copy of the source's
`starter/` into your `docs/` (overwriting method text/scaffolds, preserving your
artifact families and populated companions), or minimally confirm
`docs/scripts/regen-overview.ps1` is present and copy it from the source if absent.
Nothing else behavioral is required; the script is optional and your hand-regeneration
of `docs/overview.md` keeps working. Repos that never took v2.18, or that already have
the script, need do **nothing**.

### Fixed
- ADR-0041 (idea 0035, promoted; **amends ADR-0022**) — **the copy-driven re-copy
  could silently miss a shipped scaffold.** `updating.agent.md` step 2 correctly says
  "copy `starter/`'s own contents," but its parenthetical example list
  (`working-method.md`, `guide.md`, `travel-diary.md`, `intermediate-artifacts/`)
  omitted `scripts/` and read as exhaustive — so an executing agent narrowed the copy
  scope to the named items and skipped `docs/scripts/regen-overview.ps1` when updating
  a real adopter to v2.18. Fix: step 2's list is reframed as **explicitly
  non-exhaustive** — *"copy **everything** under `starter/`, including but not limited
  to …, and `scripts/`"* — so no example list can override the "copy everything"
  instruction, fixing the whole class (any future scaffold subtree), not just this
  file. `starter/` stays the single source of truth; no manifest is introduced. This
  amends ADR-0022 in **execution detail only** — the copy-driven mechanics are
  unchanged (reciprocal `Amended by: ADR-0041` added to ADR-0022). Deliberately *not*
  added: a post-copy tree-parity check and a conformance-check item were weighed as
  belt-and-suspenders and dropped as over-engineering for a misleading-list bug. The
  omission surfaced from a **real adopter update**, which is why this ships as a
  remediating release rather than a silent edit.

### Changed
- All three `starter/` renderings bump their provenance citation to **v2.18.1**
  (`starter/docs/working-method.md`, `starter/docs/guide.md`, `starter/AGENTS.md`).
- First **patch** release of decision-trail (prior releases were all `2.x.0` minors):
  a pure bugfix with no new behavior, so semver patch rather than minor.

## [2.18.0] - 2026-07-16

**Adopter migration:** **None.** The optional overview-regeneration script is a new
scaffold that reaches you automatically via the copy-driven "bring me current"
update (it lands at `docs/scripts/regen-overview.ps1`). Nothing behavioral is
required: your existing hand-regeneration of `docs/overview.md` keeps working
unchanged, because the prose refresh procedure stays normative. If you *want* the
faster path after updating, just ask the agent to regenerate the overview — it will
run the script when present, or regenerate by hand otherwise.

### Added
- ADR-0040 — **An optional, deterministic `overview.md` regeneration script**
  (idea 0033, promoted). Overview regeneration had grown from a trivial agent task
  into a mechanical-yet-error-prone one (five derived views over ~100 artifacts;
  three drift classes already observed), pitting Economy (#2) against
  tool-agnosticism (#3/#7/#8). The resolution keeps both: a cross-platform `pwsh`
  script (`scripts/regen-overview.ps1`, shipped in `starter/docs/scripts/`) that
  deterministically rebuilds the three family tables, the ADR → plans sub-index, and
  the stand-alone list, and **flags** non-conformant headers (bare/bullet-less block
  per ADR-0026; title-line ordinal disagreeing with the filename slot per ADR-0028)
  instead of silently copying drift — aborting rather than emitting a misfiled index.
  Four guards preserve agnosticism: the **prose refresh procedure stays normative**
  (the script is an *implementation of* it, not a second source of truth); it is
  **strictly optional and additive**; its trigger is **standing agent guidance,
  invisible to the user** (the same plain "regenerate the overview" request — the
  agent runs the script if present, else regenerates by hand); and **only the
  output's shape is contract**, so the script may be reimplemented in any language or
  omitted, with adopters lacking the runtime falling through to the prose path.
  Landed in `starter/docs/working-method.md` (an "Optional regeneration script"
  paragraph + `docs/scripts/` layout entry), this repo's `AGENTS.md` derived body,
  and the **"Keep `overview.md` current"** guidance bullet in both `AGENTS.md`
  renderings.

### Changed
- All three `starter/` renderings bump their provenance citation to **v2.18**
  (`working-method.md`, `guide.md`, and `AGENTS.md`).

## [2.17.0] - 2026-07-16

**Adopter migration:** If your repo already uses folders named `docs/deliverables/`
and/or `docs/derived/` (the pre-promotion names from josyn-builder), **rename them**
to the parallel form: `docs/deliverables/` → `docs/delivered-artifacts/` and
`docs/derived/` → `docs/derived-artifacts/` (move the contents, keep git history with
`git mv`), and update any links that point at the old paths. Repos that never had
these folders need do **nothing** — the empty documented starter folders arrive
automatically via the copy-driven "bring me current" update.

### Added
- ADR-0039 — **`delivered-artifacts/` and `derived-artifacts/` as two optional
  companion folders** (idea 0034, promoted). Completes a visibly-parallel
  `*-artifacts/` family with the existing `intermediate-artifacts/` (ADR-0020), the
  three split by the **origin** of what they hold: `intermediate-artifacts/` holds
  *gathered* scratch, `delivered-artifacts/` is the home for content a plan *creates*
  (a report, a spec, a diagram — authored fresh, not distilled), and
  `derived-artifacts/` holds human-facing projections *distilled* from the ADRs
  (regenerable on request, **never a source of truth**, distinct from the
  always-present `overview.md` status index). `delivered-artifacts/` is defined by
  *origin*, not authority — deliberately **not** a fourth lifecycle family or a new
  source of truth — so no new status, verb, or cross-link field is added. **Guard
  split:** folder *mechanics* (creating the folder, dropping a README, filing/moving
  files) are guard-free like `intermediate-artifacts/`; but *creating deliverable
  content* follows the normal confirmation guard as real plan work, and regenerating
  a `derived-artifacts/` document is user-triggered like `overview.md`. A derived
  document *should* link back to the artifacts it distills (recommended, no mandated
  format). Landed in `starter/docs/working-method.md` (two new companion sections +
  layout entries), this repo's `AGENTS.md` derived body and a new **"Delivered /
  derived artifacts"** guidance bullet in both `AGENTS.md` renderings, a note in both
  guides, and two documented-but-empty `starter/docs/…-artifacts/README.md` starter
  folders (mirrored by this home repo's own seeded folders).

### Changed
- All three `starter/` renderings bump their provenance citation to **v2.17**
  (`working-method.md`, `guide.md`, and `AGENTS.md`).

## [2.16.0] - 2026-07-15

**Adopter migration:** After copying this version, **regenerate `docs/overview.md`**
so it gains the new derived **"ADR — stand-alone decision"** section (ADR-0038) —
the list of accepted ADRs that no plan carries out via `Implements:`. The three
family tables and the ADR → plans sub-index are unchanged; this section is only
produced by a regeneration. **No artifact back-migration** is required: the
**stub-plan-at-acceptance discipline** (write a one-line `draft` stub plan when you
accept an ADR that needs execution) is forward-looking agent-and-human guidance —
internalize it and apply it going forward; existing accepted ADRs need no change.

### Added
- ADR-0038 — **a stub-plan-at-acceptance discipline plus a derived
  "stand-alone decision" backstop** (idea 0032, promoted). An accepted ADR is
  sometimes only a *spec* that comes alive when a plan carries it out (ADR-0037),
  and such a decision could silently sit undone with nothing in the rendered trail
  surfacing it. Two halves that complete each other, reusing only existing verbs
  and the existing `draft` plan status — **no new field, status, or cross-link**:
  (1) a **discipline** — when accepting an ADR that needs execution, write its plan
  then and there, at minimum a one-line `draft` stub that `Implements:` it, so a
  *plan-less* accepted ADR reads as "self-standing," not "forgotten"; and (2) a
  **derived backstop** — a new `overview.md` section listing every accepted ADR that
  no plan points at via `Implements:`, regenerated in the same header scan as the
  ADR → plans sub-index. The discipline is the classifier; the derived list is a
  review-queue *backstop*, not a classifier — a human periodically clears it. This
  **amends ADR-0011** (extends the overview's shape with a third derived view) and
  **ADR-0034** (adds the blind-complement view alongside the sub-index); both gain
  reciprocal `Amended by:` back-links. ADR-0012 (no ADR→plan back-link) stands
  untouched. Landed in `starter/docs/working-method.md` (§ *The lifecycle* and the
  refresh procedure), this repo's `AGENTS.md` derived body and a new
  **"Stub plan at acceptance"** checklist bullet in both `AGENTS.md` renderings, a
  note in both guides, and the `overview.md` templates.

### Changed
- The derived overview section is titled **"ADR — stand-alone decision"** with a
  plain-English blurb that leads with *these decisions stand on their own*, and only
  gently notes to check now and then in case a decision here accidentally needs a
  plan. (The working title during ADR-0038's development read "Accepted — no plan
  yet", which came across as an accusation rather than a neutral list.) Synced across
  both `overview.md`s, both guides, both `AGENTS.md`s, and the canonical spec.
- Two title-line conformance fixes: ADR-0016 and ADR-0035 H1s aligned to the pinned
  `# ADR-NNNN:` form (ADR-0028).
- All three `starter/` renderings bump their provenance citation to **v2.16**
  (`working-method.md`, `guide.md`, and `AGENTS.md`).

## [2.15.0] - 2026-07-12

**Adopter migration:** The **plans rule is tightened** (ADR-0037) — internalize
it and apply it going forward; there is **no artifact back-migration**. A plan is
now explicitly **mechanical execution only**: a plan **never contains a
decision-making task** ("decide X" / "clarify open question Y"). If a question
surfaces while executing, do **not** fold the decision into the plan — **return to
the decision stage**: clarify / patch / amend the governing ADR (or open a new
one), then resume. Re-copy the method-owned set (`starter/` → your `docs/`) to
pick up the sharpened spec bullet, the new agent-checklist bullet, and the guide
note; existing plans need no rewrite. Then **regenerate `docs/overview.md`** as
usual.

### Changed
- ADR-0037 — **plans are mechanical execution; a surfaced question returns to the
  decision stage** (idea 0031, promoted): an incident in a consumer repo saw an
  agent derive a plan whose tasks included *deciding undecided things* ("decide X"
  / "clarify Y") — collapsing the **decision** and **plan** lifecycle stages and
  letting decisions slip through as unreviewed plan steps, bypassing the
  confirmation guard. ADR-0004's soft wording ("the ADR is the spec, the plan is
  the *how*") did not prevent it. This **amends ADR-0004** to state plainly that a
  plan is for mechanical execution only and never holds a decision-making task,
  and to fix the mid-execution escalation: a surfaced question returns to the
  decision stage (clarify / patch / amend the ADR, or open a new one), then
  execution resumes — *that* it returns is fixed, *which* form the return takes is
  judgment sized to the question. Landed in `starter/docs/working-method.md`
  (§ *The lifecycle*, Plans bullet), this repo's `AGENTS.md` derived body, a new
  **"Plans are mechanical execution"** bullet in both `AGENTS.md` checklists
  (adopter rendering carries no ADR citation, method-home one cites ADR-0037), and
  a brief note in both guides. ADR-0004 stands (amended, not rewritten) with an
  `Amended by:` back-link.
- All three `starter/` renderings bump their provenance citation to **v2.15**
  (`working-method.md`, `guide.md`, and `AGENTS.md`).

## [2.14.0] - 2026-07-11

**Adopter migration:** After copying this version, **regenerate `docs/overview.md`**
so it gains the new derived **ADR → plans sub-index** (ADR-0034) — the three family
tables are unchanged, but the sub-index section is only produced by a regeneration.
No other behavioral changes: the proposal-heading convention (ADR-0033) requires
**no back-migration** — existing accepted ADRs already carry `## Decision` and
existing proposals already use `## Proposed decision`; the new agent-guidance
checklist bullets (ADR-0033, ADR-0035) and the sync-model refinement (ADR-0032)
reach adopters automatically via the copy-driven update and need no manual step.

### Added
- ADR-0034 — **a derived ADR → plans sub-index in `overview.md`** (idea 0028,
  promoted): a human reading an accepted ADR had no one-click path to the plan(s)
  implementing it — the `Implements:` cross-link is forward-only (plan → ADR) and
  ADR-0012 deliberately declined a reciprocal ADR→plan back-link. This closes the
  human-discoverability gap the *method-consistent* way: `overview.md` gains a
  second, **derived** view — for each ADR, the plan(s) whose `Implements:` field
  points to it, each with its current status (`draft` / `active` / `done` /
  `abandoned`), grouped by target ADR and built from the same header scan during
  the normal wholesale regeneration. Each ADR row renders as `ADR-000n – Title`.
  **No new hand-maintained field and no back-link on the settled ADR** — it amends
  ADR-0011's overview shape only and leaves ADR-0012 untouched. The spec
  (`working-method.md` §*The lifecycle* + refresh procedure), this repo's `AGENTS.md`
  derived body, and the `starter/docs/overview.md` scaffold all carry the new view.
- ADR-0035 — **enumerate two missing "lookup, not judgment call" rules in the agent
  operating checklist** (idea 0029, promoted): dogfooding ADR-0033 surfaced that its
  heading-transition rule, though stated plainly in the spec, was **absent from the
  enumerated checklist** an agent scans before acting — so it was skipped in favor of
  a sibling's observed form. A quick audit found one more gap of the same shape (the
  reciprocal cross-link rule). Two bullets are added to the "Follow the spec's
  mechanics" checklist in both `starter/AGENTS.md` and this repo's `AGENTS.md`:
  **decision heading transition** (`## Proposed decision` → `## Decision` on
  acceptance; ADR-0033) and **reciprocal cross-links** (forward link always, add the
  reciprocal back-link on amend/supersede/promotion; ADR-0012). No underlying rule
  changes — a pure discoverability/placement fix respecting the audience-fork delta
  (adopter rendering carries no ADR citations; the method-home one does).

### Changed
- ADR-0032 — **audience-forked sections are a declared delta class in the sync
  model** (idea 0026, promoted): the guide's sync note claimed a "paths-only" delta
  while two sections had quietly forked by *audience*. A new **audience-forked**
  delta class is introduced so the derived-rendering sync model can hold sections
  that legitimately differ between the home repo and adopter renderings, instead of
  pretending they are identical. (Committed in `38e7a43`, released here.)
- ADR-0033 — **author new artifacts from the spec, not from a sibling as a
  template** (idea 0027, promoted): copying a sibling artifact as a fill-in-the-blanks
  scaffold imports incidental reality (a wrong status, the wrong cross-links). A new
  agent-guidance rule pins **author from the spec, never from a sibling** (reading a
  sibling to *check* format conformance is fine; using one as a scaffold is not), and
  a **spec sharpening** pins the proposal-heading convention: a proposal uses
  `## Proposed decision` while `Status: proposed`, renamed to `## Decision` on
  acceptance — status and heading move together. Landed in `starter/AGENTS.md`, this
  repo's `AGENTS.md`, and `starter/docs/working-method.md`.
- All three `starter/` renderings bump their provenance citation to **v2.14**
  (`starter/docs/working-method.md`, `starter/docs/guide.md`, `starter/AGENTS.md`).

## [2.13.0] - 2026-07-11

### Added
- ADR-0030 — **resume economy as a human-facing discipline in the guide** (idea
  0023, the third and final axis of decomposed idea 0020): Economy (#2) promises
  the method is cheap to *resume*, but nothing named the discipline that makes
  that real for the human driving the work. The mechanics already exist (derived
  `overview.md`, travel diary, greppable header fields) and the agent already
  exploits them — so the missing piece is advice aimed at the levers only the
  human controls. Per the accepted decision, a short **"Working with an agent:
  resuming cheaply"** section is added to `guide.md` (both this repo's and
  `starter/docs/guide.md`), carrying five human levers: how you re-open the
  session, name the artifact not the topic, ask narrow, invest at pause-time not
  resume-time, and terseness as a write/approve discipline. It is **purely
  advisory** — no mechanism, no new artifact family, no cross-link vocabulary. It
  lands **only in the human-facing `guide.md` register** (never the always-loaded
  spec `working-method.md` / `AGENTS.md`), so it adds **zero per-session weight**
  and preserves ADR-0029's shrink; agent-facing mechanics (grep headers, header-
  only overview regeneration, already owned by ADR-0011 / idea 0008) are
  cross-referenced by concept rather than restated.
- All three `starter/` renderings bump their provenance citation to **v2.13**
  (`starter/docs/working-method.md`, `starter/docs/guide.md`, `starter/AGENTS.md`).
- ADR-0031 — **the adopter update path is human intent, agent execution** (idea
  0025, promoted): the update path (`adopting.md` §3) read as an overcomplicated,
  deterrent human checklist even though the ADR-0022 mechanics are sound — because
  it mixed audiences, handing a present-by-definition agent's mechanical steps to
  the human. Per the accepted decision, the two audiences are split into two
  artifacts. The **human** trigger shrinks to one plain intent that names the
  **source and the how-to file** — *"update the method from `<source>`; the how-to
  is `<source>/updating.agent.md`"* — run as **one transparent batch under the
  confirmation guard**; the human must supply the source (the agent never guesses a
  target). The **agent** procedure moves into a new terse, self-contained,
  tool-agnostic **[`updating.agent.md`](updating.agent.md)** (standard-repo-only,
  *not* copied into adopters), the single operational source of truth for the
  copy-driven "bring me current" steps and the conformance check. Naming the how-to
  file in the prompt closes the **bootstrap** (hen-and-egg): an adopter on an older
  version needs no prior in-repo knowledge of the mechanism. **ADR-0022's mechanics
  are unchanged** — this amends it in *presentation and audience framing* only; a
  deterministic conformance *linter* stays a deferred option (ADR-0008), no tool
  ships.

### Changed
- **Human-facing on-ramp clarity (informal patches, no contract change).** Two
  small documentation improvements folded into this release: (a) `guide.md`'s
  "How to start" now opens with a short adoption lead-in — clone/pull the standard
  repo and follow [`adopting.md`](adopting.md) — before the everyday lifecycle
  steps (home-repo `guide.md` only; the adopter's `starter/docs/guide.md` keeps the
  lifecycle steps); (b) `adopting.md` §2 ("Inject into an existing repo") is
  collapsed from a near-duplicate of §1 down to the two real deltas (copy
  `starter/docs/`, and the `AGENTS.md` create-vs-append difference). No mechanic or
  contract changed — ADR-0021/ADR-0022 remain in force.
- **Captured, then reworked (idea 0025 → ADR-0031 → plan 0021).** The confusing
  update path was first recorded as idea 0025 and has now been reworked
  decision-trail: `adopting.md` §3 is slimmed from an 8-step human procedure to a
  single human trigger (intent + source + how-to pointer) that points at the new
  [`updating.agent.md`](updating.agent.md); the standalone "Conformance check"
  section is collapsed to a pointer at the same file (the six-point checklist now
  lives there); and this repo's `AGENTS.md` "Agent operating guidance" bullet on the
  copy-driven update is updated to name the human/agent split and `updating.agent.md`
  as the executable source of truth. `guide.md`'s existing `adopting.md` pointer is
  left unchanged (the agent-facing file stays out of the human narrative). ADR-0022
  is cross-linked `Amended by: ADR-0031` (mechanics unchanged).
- **Small on-the-fly `guide.md` wording patches (no contract change):** the opening
  sentence now reads *"This is the narrative introduction to decision-trail"*, and
  the closing "quick reference" line acknowledges that some human-facing advice
  lives only in the guide (both the canonical `starter/docs/guide.md` and this
  repo's derived `guide.md`).
- **Human-facing on-ramp clarity (informal patches, no contract change).** Two
  small documentation improvements folded into this release: (a) `guide.md`'s
  "How to start" now opens with a short adoption lead-in — clone/pull the standard
  repo and follow [`adopting.md`](adopting.md) — before the everyday lifecycle
  steps (home-repo `guide.md` only; the adopter's `starter/docs/guide.md` keeps the
  lifecycle steps); (b) `adopting.md` §2 ("Inject into an existing repo") is
  collapsed from a near-duplicate of §1 down to the two real deltas (copy
  `starter/docs/`, and the `AGENTS.md` create-vs-append difference). No mechanic or
  contract changed — ADR-0021/ADR-0022 remain in force.

**Adopter migration:** none. This release adds human-facing advisory prose to
`guide.md` and re-presents the (unchanged) update path; the new `updating.agent.md`
is standard-repo-facing (an adopter's agent is *pointed at* it during an update, it
is not copied in), and the copied method text reaches adopters automatically via the
"bring me current" update (ADR-0022). No hand-done step is required.

## [2.12.0] - 2026-07-11

### Changed
- ADR-0029 — **shrink the always-loaded agent instruction weight** (idea 0021,
  amends ADR-0014): `AGENTS.md` is injected as custom instructions before every
  task, and it re-stated each normative rule ~twice — once in the derived spec
  body (lifecycle / dedicated sections) and again in full in the non-derived
  `## Agent operating guidance` block (the Refresh procedure was duplicated
  verbatim). Per the accepted **A + C** decision, the canonical spec
  (`starter/docs/working-method.md`) is compacted to state each rule **once**, and
  the non-derived guidance block is hand-tightened to **principle + pointer** form
  (each mechanic bullet now flags the trap and points to the owning spec section,
  rather than restating it); the duplicated Refresh-procedure block is removed from
  guidance and kept only in the spec. The spec register is optimized **agent-first**
  — no repetition retained for human skimmability, since `guide.md` (which the agent
  never loads) already narrates every concept. This repo's derived `AGENTS.md` body
  was regenerated from the compacted spec, which also reconciled two drifts: the
  Refresh procedure now sits in the lifecycle section, and the overview-regeneration
  wording matches ADR-0016 ("whenever the user explicitly asks", not "after any
  work"). Net size: spec ~15.3 KB → ~13.7 KB; `AGENTS.md` ~21.9 KB → ~18.6 KB
  (~2k tokens saved per session), with **no behavioral or mechanism change** and no
  rule, status, or field name dropped.
- All three `starter/` renderings bump their provenance citation to **v2.12**
  (`starter/docs/working-method.md`, `starter/docs/guide.md`, `starter/AGENTS.md`).

**Adopter migration:** none. This is a prose-compaction release with no behavioral
change; the tightened method text and guidance reach adopters automatically via the
copy-driven "bring me current" update (ADR-0022). No hand-done step is required.

## [2.11.0] - 2026-07-11

### Added
- ADR-0028 — **pin the title-line format: ordinal in H1** (idea 0024, amends
  ADR-0026): ADR-0026 pinned the header-block bullet format but left the H1
  title-line rendering unpinned, and the same drift class recurred — ideas,
  decisions, and plans split between a numbered `# N. Title` form and a bare
  `# Idea: Title` / descriptive form. The decisive argument: the ordinal is the
  **spoken handle** ("promote idea 17") used constantly in conversation, so
  forcing a filename lookup after reading content in the editor is bad UX. The
  method texts now state a **canonical title-line template** — typed and
  zero-padded, family named — `# Idea 0017: Title` / `# ADR-0017: Title` / `# Plan
  0017: Title`, filename remains authoritative (ADR-0015) and the title is its
  visible echo. The **refresh procedure is hardened** to treat a title↔filename
  ordinal mismatch as a conformance failure, and a **title-line match** step is
  added to the conformance check (`adopting.md`). Applied to both renderings
  (`starter/docs/working-method.md` + `AGENTS.md`), the starter hand-off file
  (`starter/AGENTS.md`), and the starter exemplar
  (`starter/docs/decisions/0001-adopt-decision-trail.md`). This repo's own 56
  artifact files (ideas, decisions, plans) were swept to the canonical title-line
  form (text preserved exactly, only the ordinal prefix added/normalized).

### Changed
- All three `starter/` renderings bump their provenance citation to **v2.11**
  (`starter/docs/working-method.md`, `starter/docs/guide.md`, `starter/AGENTS.md`).

**Adopter migration:** backfill each existing artifact's H1 to the canonical
`# Idea NNNN: Title` / `# ADR-NNNN: Title` / `# Plan NNNN: Title` form (ordinal
zero-padded to match the filename slot, text otherwise preserved), then
regenerate `overview.md`. The new wording itself reaches adopters automatically
via the copy-driven "bring me current" update (ADR-0022); only the backfill of
already-existing artifact titles is a required, hand-done step. (Adopters may
optionally run the new title-line-match conformance check to confirm their
existing artifacts are clean.)

## [2.10.0] - 2026-07-10

### Added
- ADR-0025 — **collision-proof slot numbering** (idea 0018, amends ADR-0015): the
  ordinal-numbering rule gains a reliable **procedure** so duplicate numbers
  (two `0010` ideas were created independently in two repos) can't recur. The
  method texts now tell the agent to enumerate the whole family and take
  **`max(existing number) + 1`** — never the first apparent gap a glob surfaces —
  and **verify the target filename is unused** before writing. The
  timeline-preserving **insert-and-shift** repair (renumber the intruder into
  place, shift every later artifact, rewire cross-links, regenerate the overview)
  is documented as the sanctioned way to slot an out-of-order artifact. A
  **duplicate-number detection** step is added to the conformance check
  (`adopting.md`). Applied to both renderings (`starter/docs/working-method.md` +
  `AGENTS.md`) and the starter hand-off file (`starter/AGENTS.md`).
- ADR-0026 — **canonical artifact-header format** (idea 0019): the header block
  had drifted into two forms that parse the same but look different — bulleted
  (`- Status:`) and bare (`Status:`) — and because the overview **refresh
  procedure** greps the bulleted form, a bare header was **silently missed**,
  leaving a stale row in `overview.md`. The method texts now state a **canonical
  header template** (a `# Title` line, a blank line, then a bulleted block —
  `- Date:`, `- Status:`, any cross-link fields, optional `- Tags:` — each on its
  own `-`-prefixed line), the **refresh procedure is hardened** so a mis-rendered
  header is treated as a conformance failure rather than an invisible skip, and a
  **header-format detection** step is added to the conformance check
  (`adopting.md`). Applied to both renderings (`starter/docs/working-method.md` +
  `AGENTS.md`) and the starter hand-off file (`starter/AGENTS.md`).
- ADR-0027 — **a `decomposed` idea status for a budded parent map** (idea 0017,
  amends ADR-0024): the **idea** family's status vocabulary gains `decomposed` —
  a rare, *alternative finalized* state (alongside `promoted`) for a large idea
  that has been broken apart by **budding** into child ideas, its own content
  moved out. `seed` is reframed as *"not yet promoted,"* so a still-budding parent
  map sits there honestly; `decomposed` is hand-curated and reversible and says
  nothing about the children's fate. A fixed **disentangling procedure** is stated
  (parent → `decomposed`; each axis buds 1:1 to its own ADR — never
  multi-promotion; reasons documented in the parent; one status per idea) while
  the *strategy* stays a free judgment call the agent proposes and the human
  decides. The per-family status guard is extended to fence `decomposed` as
  idea-only. Applied to both renderings (`starter/docs/working-method.md` +
  `AGENTS.md`), the starter hand-off file (`starter/AGENTS.md`), and both guide
  renderings (`guide.md` + `starter/docs/guide.md`). The concept is also raised in
  the human guide to a first-class **"Budding: when one idea is really several"**
  section.

### Changed
- All three `starter/` renderings bump their provenance citation to **v2.10**
  (`starter/docs/working-method.md`, `starter/docs/guide.md`, `starter/AGENTS.md`).

**Adopter migration: none.** ADR-0025, ADR-0026, and ADR-0027 are
guardrail/vocabulary clarifications with no behavioral change to any state
machine, and no existing artifact is reinterpreted (no `seed` idea becomes
`decomposed` retroactively); the new wording and the extra permitted status reach
adopters automatically via the copy-driven "bring me current" update (ADR-0022).
(Adopters may optionally run the new duplicate-number and header-format
conformance checks to confirm their existing artifacts are clean.)

## [2.9.0] - 2026-07-10

### Added
- ADR-0024 — **per-family status vocabulary guard** (idea 0016): the method texts
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
- ADR-0023 — **promote and teach the method** (idea 0015): the guide is reworked
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
- ADR-0022 — **copy-driven "bring me current"** (idea 0014): updating an adopter to
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
- ADR-0020 — **intermediate artifacts** (idea 0013): an optional, informal
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
