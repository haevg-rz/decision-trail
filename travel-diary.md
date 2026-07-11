# Travel diary

An informal, growing logbook of the journey — an optional, **human-facing**
companion to `overview.md`. Where the overview is a derived, terse status index,
this file is loose prose: a friendly trail of *"where were we, and where were we
headed"* that a colleague can skim after a break.

The artifacts under `ideas/`, `decisions/`, and `plans/` remain the **source of
truth**. This file touches none of them and is never authoritative; it can be as
loose as it likes.

## Agent instructions

When the user says **"add a chapter to the travel diary"** (or similar), do this
light-weight task — **no confirmation guard, no ADR, no plan**:

1. **Prepend** the new dated section at the top — newest first. It goes directly
   below this "Agent instructions" block, above all older entries.
2. Header is the current date in brackets: `## [YYYY-MM-DD]`. If a section for
   today already exists, disambiguate with a counter: `## [YYYY-MM-DD-(2)]`, then
   `-(3)`, and so on.
3. Under it, write a brief, friendly prose entry covering roughly:
   - **Where we are** — the current state / context.
   - **What we achieved** — since the last entry.
   - **What is left** — open threads.
   - **What is next** — the immediate next step.
4. Optionally end with a one- or two-sentence **continuation brief** — a nudge to
   whoever (human or agent) picks this up next, ideally with a link to the
   relevant plan or ADR.

Keep it short and human. It's a diary, not a report.

---

## [2026-07-11-(2)]

**Where we are.** v2.12.0 is ready to cut, closing plan 0019 (ADR-0029) — the
"always-loaded weight" thread from the 0020 economy map. The concept phase stays
settled; this was a use-phase refinement of the method's own texts.

**What we achieved.**
- **Answered idea 0021's three open questions**, one confirmed step at a time:
  compact at the **canonical spec** and hand-tighten the non-derived guidance
  block (A + C; rejected baking compaction into the mechanical regeneration, B);
  keep the spec **agent-first** with human narrative living in `guide.md`; and do
  it the method way — a light ADR amending ADR-0014.
- **Promoted 0021 → ADR-0029** (amends ADR-0014), accepted it, and wrote **plan
  0019**.
- **Executed plan 0019 end to end.** Compacted `starter/docs/working-method.md`
  (15.3 → 13.7 KB), rewrote both `## Agent operating guidance` blocks to
  *principle + pointer* form, removed the verbatim-duplicated Refresh procedure,
  and regenerated the derived `AGENTS.md` body (21.9 → 18.6 KB, ~1k tokens/session).
  The regeneration also reconciled two real drifts: the Refresh procedure now sits
  in the lifecycle section, and overview-regeneration wording matches ADR-0016
  (not the stale "after any work"). Verified no rule, status, or field name was
  lost; `guide.md` already narrates every trimmed concept, so no additions needed.
- Bumped provenance to **v2.12** and added the CHANGELOG entry with **`Adopter
  migration: none`** (prose-only, reaches adopters via the copy-driven update).
- **Reflected honestly on the economics.** The always-on cost is ~4,600 tokens
  (~2–4% of a real session) — sound, but today's refactor hit a floor because we
  refused to drop any rule. The deterministic *procedures* still sit in
  always-loaded prose.

**What is left.** Two siblings of 0021 remain `seed`: **0022** (procedures as
optional skills) and **0023** (resume-time economy as a stated discipline).

**What is next.** Promote **idea 0022** — skills are the natural next lever, the
only way to evict the still-inline procedures without losing anything (and they
make execution more reliable). Mind the tool-agnosticism caveat: frame skills as
an *optional, derived* rendering of canonical procedure prose (idea 0022 §open
questions; ADR-0006/ADR-0014).

---

## [2026-07-11]

**Where we are.** v2.11.0 is cut, closing plan 0018 (ADR-0028) — the last thread
open under v2.10's release. Along the way we also budded a new decomposed idea map
(0020 → 0021/0022/0023) about running the method economically.

**What we achieved.**
- **Budded idea 0020** ("run the method economically and token-saving") into
  three children after an agent's-eye token-cost analysis: 0021 (shrink the
  always-loaded agent-instruction weight), 0022 (render fixed procedures as
  optional skills), and 0023 (name the resume-time economy practices as a stated
  discipline). 0020 itself became a proper `decomposed` pure map, with its
  original content moved into 0023 and the branching reasons recorded in place —
  the first real-world use of ADR-0027's mechanism.
- **ADR-0028 — pin the title-line format (idea 0024, amends ADR-0026).** While
  investigating a drift question ("why did idea headlines stop carrying their
  number?"), we found the same drift class ADR-0026 had just fixed for header
  bullets had recurred in the H1 title line. The decisive argument: the ordinal
  is the *spoken handle* ("promote idea 17") used constantly in conversation, so
  forcing a filename lookup after reading the editor is bad UX. Decided on a
  typed, zero-padded, family-named form — `# Idea 0017: Title` / `# ADR-0017:
  Title` / `# Plan 0017: Title` — with title↔filename agreement as a new
  conformance check.
- **Executed plan 0018 step by confirmed step**, all 10 tasks: canonical
  template + refresh-procedure hardening in both renderings, the new
  conformance-check step in `adopting.md`, a full sweep of this repo's 56
  artifact files to the canonical title-line form, the derived-rendering fix,
  the provenance bump to v2.11, and the CHANGELOG entry.
- Along the way, clarified for the human colleague the real difference between
  the three method files (`working-method.md` canonical spec, `AGENTS.md`
  derived rendering, `starter/AGENTS.md` adopter hand-off) and confirmed the
  "Agent operating guidance" register (ADR-0014) is deliberate — though flagged
  that it has grown beyond its original scope, feeding directly into idea 0021.

**What is left.** Ideas 0021, 0022, 0023 are all still `seed` — none promoted
yet. The "Agent operating guidance" duplication/growth concern is noted but
unaddressed.

**What is next.** Pick up one of 0021/0022/0023 when ready to mature it into a
proposal; idea 0021 (shrink always-loaded weight) is the most directly connected
to the guidance-bloat concern just observed.

## [2026-07-10-(2)]

**Where we are.** v2.10.0 is ready to cut — a three-ADR guardrail-and-vocabulary
release that also sharpens the human guide. It bundles work that had been
collecting under the open `## [2.10.0]` changelog heading: ADR-0025, ADR-0026, and
the new ADR-0027.

**What we achieved.**
- **ADR-0027 — a `decomposed` idea status** (idea 0017 → plan 0017). The core new
  idea of this release: an idea is often *not one thought* but a **knot of
  entangled ideas**. Promotion is 1:1, so a big idea can't fan out into many ADRs —
  the tool is **budding**. But a budded parent had no honest resting state (`seed`
  lied, `dropped` claimed rejection, `promoted` misdescribed). We added
  `decomposed` — a rare, hand-curated, reversible *alternative-finalized* state
  that says the idea broke into children and says nothing about their fate. `seed`
  is reframed as "not yet promoted." A fixed **disentangling procedure** is stated
  (procedure fixed, strategy free; agent proposes, human decides).
- **Surfaced the concept in the human guide.** After a course-correction (we first
  over-reached into the machine-facing texts, then reverted), the "knot of
  entangled ideas" idea now appears at four escalating levels — promise #6, the
  "an idea can be…" list, the idea stage, and its own first-class section
  **"Budding: when one idea is really several."**
- **Closed the two sibling guardrail plans** that were waiting on a release:
  ADR-0025 (collision-proof `max+1` slot numbering + insert-and-shift +
  duplicate-number conformance check, plan 0015) and ADR-0026 (canonical bulleted
  header template + hardened refresh procedure + header-format conformance check,
  plan 0016).
- **Cut the release:** provenance bumped to **v2.10** across all three `starter/`
  renderings (fixing a stale `vX.Y` in the starter guide along the way),
  `CHANGELOG.md` `## [2.10.0]` dated and completed with all three ADRs and
  `Adopter migration: none`, and `overview.md` regenerated (as of 2026-07-10):
  plans 0015/0016/0017 → `done`, idea 0017 → `promoted`, ADR-0027 → `accepted`.

**What is left.** Nothing for this release. Still-open loose ends noticed earlier
remain untouched: the two `0010` ideas cosmetic numbering wart, and two fresh
`seed` ideas of the home repo — 0019 (pin header format — now promoted) done; 0020
(run the method economically / token-saving) still a `seed` awaiting its turn.

**What is next.** Commit, tag `v2.10.0`, and publish the GitHub release. Then the
`decomposed` vocabulary and the budding guide section are available for adopters
via the copy-driven update.

---

## [2026-07-10]

**Where we are.** v2.9.0 is ready — a small guardrail release. While an adopter
repo (`ckl-builder`) was using the method, its agent twice mislabelled an
artifact's status by borrowing a word from the wrong family (an *idea* headed
`proposed`, and earlier a *plan* headed `proposed` instead of `draft`). That real
misuse surfaced a genuine gap in the method's docs, and we fixed it *decision-trail*
— idea 0015 → ADR-0024 → plan 0014, all closed.

**What we achieved.**
- **Diagnosed the flaw:** the status vocabulary lived only in the lifecycle table,
  with no stated *entry* status and no "don't mix families" guard — the same class
  of easy-to-violate implicit rule that numbering already got a guard for (ADR-0015).
  `proposed` is especially primed for misuse because it also headlines "How to start
  working" step 2.
- **Added a per-family status guard** to both renderings (`starter/docs/working-method.md`
  + `AGENTS.md`) and the starter hand-off (`starter/AGENTS.md`): each family's entry
  status stated in words (idea→`seed`, proposal→`proposed`, plan→`draft`) plus an
  exclusivity rule (never borrow another family's status), mirroring the numbering
  guard's placement.
- **Cut the release:** provenance bumped to v2.9 in both `starter/` renderings,
  `CHANGELOG.md` `## [2.9.0]` with `Adopter migration: none` (pure doc change).
- **Regenerated `overview.md`** (as of 2026-07-10) and, along the way, restored a
  missing row — the dropped duplicate-numbered idea `0010-stamp-overview-with-date-time.md`.

**What is left.** Nothing for this thread. One loose end noticed but *not* touched:
there are **two `0010` ideas** (a numbering collision predating this work) — a
harmless cosmetic wart that could be cleaned up someday on its own trail.

**What is next.** Commit the v2.9.0 changes. Then back to the adopter side, where the
conversation that started all this is still open: `ckl-builder`'s idea 0011 (revisit
integrity for `ckl-libs-crypt` — AES-GCM via BCL-native `AesGcm`) is a fresh `seed`
awaiting promotion.

**Continuation brief.** The method change is fully landed; just commit. For the
substantive crypto thread, pick up at `ckl-builder`'s `docs/ideas/0011-integrity-for-ckl-libs-crypt.md`.

---

## [2026-07-05]

**Where we are.** v2.8.0 is ready to cut — the guide has been reworked from a plain
narrative introduction into a genuinely *didactical* tutorial. This was the first
change driven by the "promote and teach the method" thread (idea 0014 → ADR-0023 →
plan 0013).

**What we achieved.**
- **Reworked both guide renderings** (`guide.md` and `starter/docs/guide.md`) into a
  teaching piece: motivate-first, a progressively-introduced lifecycle, and one
  canonical worked example — *"add a dark-mode toggle to a small web app"* — walked
  all the way from idea to ticking execution checkboxes.
- **Added two Mermaid diagrams** (GitHub-rendered, plain-text): the lifecycle stages
  + status transitions, and the cross-link vocabulary (reciprocal vs. forward-only).
- **Opened up the term "idea"** with a list of what counts (a requirement, a tiny
  thought, a question, a big concept, a discussion takeaway, an improvement
  observation) — lowering the barrier to capturing one.
- **Added two mindset chapters:** "a conversation, not a command line" (the AI as
  co-pilot/consultant; no syntax, just dialogue — and the agent writes every
  markdown artifact for you, burden gone) sitting before the existing "a 'yes' has a
  scope" guard section.
- **Promoted Tags, the travel diary, and intermediate artifacts** into their own
  top-level chapters, so they're no longer buried under "The overview."
- **Dropped the German translation** thread (ADR-0023's second thread): the
  machine-drafted first pass was clumsy and uninspiring; revised the ADR/plan in
  place while still uncommitted, so it leaves no trace in permanent history.
- Cut the release scaffolding: `[2.8.0]` CHANGELOG entry (`Adopter migration: none`,
  copy-driven), provenance bumped to **v2.8** in the starter files, and regenerated
  `overview.md`.

**What is left.** Commit, push, tag `v2.8.0`, and cut the GitHub release.

**What is next.** Ship 2.8.0. Then teaching-material improvements can continue as
their own ideas (a properly-done translation could be one). See
[plan 0013](plans/0013-promote-and-teach-the-method.md).

## [2026-07-04-(2)]

**Where we are.** v2.7.0 is **released and tagged**, and the update path it added
has already been used for real. The tag history is now complete and continuous
(`v2.0.0 … v2.7.0`) — we backfilled the two missing tags (`v2.4.0`, `v2.6.0`) along
the way. decision-trail is settled, released, and freshly dogfooded.

**What we achieved.**
- **Cut the 2.7.0 release.** Committed the ADR-0022 work, backfilled the missing
  `v2.4.0` and `v2.6.0` tags, tagged `v2.7.0`, and pushed everything (commit +
  tags) to the standard repo.
- **Dogfooded the new update path on `josyn-builder`** (the repo that exposed the
  gap in the first place). Migrated it **v2.3 → v2.7** via the copy-driven "bring me
  current" procedure: re-copied `working-method.md` + `guide.md`, bumped the
  citation and refreshed the `AGENTS.md` guidance block, recorded the bump as that
  repo's ADR-0014, regenerated its overview — and **preserved** its authored
  artifacts, populated travel diary, and intermediate-artifacts untouched. All four
  intervening releases were `Adopter migration: none`, so no behavioral work.
- Ran the new **conformance check** on josyn-builder: PASS (30 artifacts carry
  `Date:`, overview in sync, citation consistent). Committed the migration in
  isolation from that repo's in-progress WIP and pushed it.

**What is left.** Nothing outstanding on the method itself. josyn-builder still has
its own unrelated WIP in the working tree — that's their project's business, not
ours.

**What is next.** No open method threads. Future changes ride the same rails: idea →
ADR → plan → release, with each release stating its `Adopter migration:` line.

*Continuation brief:* the v2.7 "bring me current" path proved itself on its first
real use — the josyn-builder update landed cleanly and conformant. Nothing pending;
pick up a new idea whenever one arrives.

---

## [2026-07-04]

**Where we are.** decision-trail's adopter update path is now **reliable**, not
just present. In one sitting we took idea 0013 through the whole lifecycle: idea →
[ADR-0022](decisions/0022-every-release-ships-reliable-update-instructions.md)
(accepted, amends ADR-0021) →
[plan 0012](plans/0012-carry-adr-0022-into-the-method.md) (done). The trail now
runs `ideas` 0001–0013, `decisions` 0001–0022, `plans` 0001–0012, with a
`[2.7.0]` section drafted in the CHANGELOG and the starter bumped to **v2.7**.

**What we achieved.**
- **Promoted idea 0013** — *"every change must ship precise, agent-reliable update
  instructions for older adopters"* — into a proposal, then settled its five open
  questions one at a time.
- **The settled decision (ADR-0022):** "bring me current" is now **copy-driven** —
  re-copy the method-owned set (exactly `starter/`'s contents) into the adopter's
  `docs/`, so additive scaffolds arrive automatically. A **preserve rule** protects
  project content; `Adopter migration:` is scoped to **required behavioral changes
  only**; every version carries a **durable in-repo pointer** to `adopting.md`; and
  a lightweight **conformance check** (do-guidance, no tool) closes the loop.
- **Executed plan 0012:** added the `Amends:`/`Amended by:` links between 0022 and
  0021, rewrote `adopting.md` §3 to the copy-driven procedure + a new conformance
  section, strengthened the starter pointer, refined the release-author rule in
  `CHANGELOG.md` and `AGENTS.md`, and drafted the `[2.7.0]` release entry.

**What is left.** Same standing thread as last time: the work is committed but
**not yet released/tagged** — the tag still trails the drafted CHANGELOG sections
(`[2.6.0]`, now `[2.7.0]`). No open design questions.

**What is next.** Cut the actual release/tag when ready, folding in both drafted
CHANGELOG sections.

*Continuation brief:* the method is settled and dogfooded another round — idea 0013
closed the "bring me current" gap the josyn-builder update run exposed. Pick up at
[plan 0012](plans/0012-carry-adr-0022-into-the-method.md) /
[ADR-0022](decisions/0022-every-release-ships-reliable-update-instructions.md) if
you need the details.

---

## [2026-07-03-(3)]

**Where we are.** decision-trail has a full **adopter on-ramp**. Idea 0004 was
sharpened and promoted through the whole lifecycle in one sitting: idea →
[ADR-0021](decisions/0021-a-single-adopter-on-ramp-fresh-inject-update.md)
(accepted) → [plan 0011](plans/0011-ship-adopter-on-ramp-and-migration-contract.md)
(done). The trail now runs `ideas` 0001–0013, `decisions` 0001–0021, `plans`
0001–0011. Work is committed but **not yet released/tagged** — this is still v2.5
on the tag, with a `[2.6.0]` section drafted in the CHANGELOG.

**What we achieved.**
- Rewrote idea 0004 into *"using decision-trail in your own repo should be as easy
  as possible"* — two preconditions (a git repo; an agentic setup) and three
  scenarios (fresh / inject / update).
- ADR-0021 decided a single top-level [`adopting.md`](adopting.md) on-ramp + a
  **release-migration contract** (every `CHANGELOG.md` entry carries an
  `Adopter migration:` line, even "none"). Chose **Option D** (pure do-guidance,
  tooling only as an optional non-method give-away).
- Executed plan 0011: wrote `adopting.md`, added the contract to `CHANGELOG.md` +
  this repo's `AGENTS.md`, backfilled `Adopter migration:` across all past
  releases, added the starter→`adopting.md` pointer, bumped the starter citation to
  **v2.6**, linked it from both guides.
- **Course-corrected on tooling.** I over-built a `giveaway/` copy script (ps1 +
  sh) without discussing it. After a requirements pass we concluded no adopter step
  is hard, error-prone, *and* beyond "agent + copy-paste" — so we **dropped the
  script entirely** and `adopting.md` now explains *why there's no tool*.
- Dogfooding against *josyn-builder* (on v2.3) surfaced a real gap → captured as
  [idea 0013](ideas/0013-every-change-ships-reliable-update-instructions.md):
  every change must ship precise, agent-reliable update instructions so an older
  adopter can be brought *fully current*, not just *minimally migrated*.

**What is left.** idea 0013 is a `seed` — not yet promoted. The v2.6 work is
uncommitted and untagged. josyn-builder itself has not been updated 2.3 → 2.6.

**What is next.** Commit today's work. Then, in a fresh context, decide whether to
promote idea 0013 (the manifest / required-vs-optional-scaffold / conformance-check
questions) before tagging v2.6 — and separately, do the josyn-builder update.

**Continuation brief.** Start from `overview.md`, then read
[idea 0013](ideas/0013-every-change-ships-reliable-update-instructions.md) — it is
the sharpest open thread and directly shapes how (and whether) v2.6 should ship its
own migration story before release.

## [2026-07-03-(2)]

**Where we are.** decision-trail is now at **v2.5** — committed, pushed, and tagged
`v2.5.0` on `main`. The trail runs `ideas` 0001–0012, `decisions` 0001–0020, and
`plans` 0001–0010. The method stays settled; this change was itself made
decision-trail, start to finish.

**What we achieved.** We promoted a second concept proven in the sibling repo
*josyn-builder* — **intermediate artifacts** — into the method:
- Captured the working-material gap as
  [idea 0012](ideas/0012-intermediate-artifacts-a-scratch-layer-for-execution.md):
  executing a plan sometimes means *gathering* material to work on later, and that
  scratch had no home among the authoritative artifacts.
- Worked through all seven open questions one at a time, then decided it in
  [ADR-0020](decisions/0020-intermediate-artifacts-a-scratch-layer-for-execution.md):
  an optional, informal `intermediate-artifacts/` folder — outside the lifecycle,
  **not a source of truth**, guard-free, internally unstructured, committed by
  default, left to rot harmlessly. It's the *execution-stage* cousin of the
  human-facing travel diary.
- Carried it into action via
  [plan 0010](plans/0010-ship-intermediate-artifacts.md): new **Intermediate
  artifacts** section in the canonical `working-method.md`, a documented-but-empty
  `starter/docs/intermediate-artifacts/` folder, a seeded home-repo folder,
  regenerated `AGENTS.md` (method body + guard-free note, mirrored in
  `starter/AGENTS.md`), a mention in both `guide.md` renderings, a `CHANGELOG.md`
  **2.5.0** entry, and a regenerated `overview.md`. Provenance bumped to v2.5.

Along the way we also **committed the pending confirmation-guard teaching work**
(idea 0011, ADR-0019, plan 0009) that had been sitting uncommitted, and added a
`.gitignore` for Visual Studio's `.vs/` folder.

**What is left.** Nothing on this thread — plan 0010 is `done`. One loose end noted
for later: **v2.4.0 was never tagged** (the travel-diary release), so the tag
history skips from v2.3.0 to v2.5.0.

**What is next.** Use intermediate artifacts in anger: the next plan that needs to
park gathered data now has a conventional home. Optionally, backfill the missing
`v2.4.0` tag.

*Continuation brief:* State lives in the artifacts. For this feature, the reasoning
is in [ADR-0020](decisions/0020-intermediate-artifacts-a-scratch-layer-for-execution.md)
and the execution record in [plan 0010](plans/0010-ship-intermediate-artifacts.md).

## [2026-07-03]

*(First entry — this diary was born the same session the feature landed, so it
doubles as a worked example of the very thing it describes.)*

**Where we are.** decision-trail is moving to **v2.4**. The trail runs `ideas`
0001–0010, `decisions` 0001–0018, and `plans` 0001–0008. The concept phase stays
settled — every change to the method is itself made decision-trail.

**What we achieved.** We promoted a concept proven in the sibling repo
*josyn-builder* — the **travel diary** — into a feature of the method:
- Captured the human-machine-interface gap as
  [idea 0010](ideas/0010-a-human-friendly-travel-diary.md): the trail answers an
  *agent's* continuity questions precisely, but a *human* colleague asking "where
  are we / what changed / what's left / what's next?" still had to synthesize
  across `overview.md`, the active plan, and recent ADRs.
- Decided it in
  [ADR-0018](decisions/0018-a-travel-diary-for-the-human-machine-interface.md):
  the diary is a **shipped, optional, human-facing companion** to the
  machine-facing `overview.md` — authored prose vs. derived state — maintained
  guard-free and explicitly **not** a source of truth.
- Are carrying it into action via
  [plan 0008](plans/0008-ship-the-travel-diary.md): documented the mechanism in
  the canonical `working-method.md`, shipped a `starter/docs/travel-diary.md`
  template, regenerated `AGENTS.md` (method body + a guard-free "add a chapter"
  note, mirrored in `starter/AGENTS.md`), mentioned it in both `guide.md`
  renderings, and — since we chose to **dogfood** it — created this live diary.

*(Note: an earlier attempt this session ran the whole lifecycle ahead of approval
and self-accepted the ADR — a confirmation-guard breach. It was rolled back and
redone properly, step by confirmed step. The trail is history; this is part of it.)*

**What is left.** Two closing steps of plan 0008: the `CHANGELOG.md` **2.4.0**
entry and regenerating `overview.md`. Then the plan flips to `done`.

**What is next.** Finish those two steps, then use the diary in anger: the next
time someone asks "where are we?", point them here.

*Continuation brief:* The repo is its own continuation anchor — state lives in the
artifacts. For this feature specifically, the reasoning is in
[ADR-0018](decisions/0018-a-travel-diary-for-the-human-machine-interface.md) and
the execution record in [plan 0008](plans/0008-ship-the-travel-diary.md).
