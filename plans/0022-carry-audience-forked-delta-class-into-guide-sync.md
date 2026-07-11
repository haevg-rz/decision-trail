# Plan 0022: Carry the audience-forked delta class into the guide sync model

- Date: 2026-07-11
- Status: done
- Implements: [ADR-0032](../decisions/0032-audience-forked-sections-are-a-declared-delta-class.md)

## Goal

Make the guide renderings honest and safely regenerable, per
[ADR-0032](../decisions/0032-audience-forked-sections-are-a-declared-delta-class.md):
declare "audience-forked section" as a delta class, enumerate the guide's forked
sections ({How to start, Where to go next}), stop the derived home guide's sync note
from lying, and give a regeneration a mechanical lookup so a faithful regen no
longer clobbers the home-only content.

## Context the executor needs

- **Canonical source:** [`starter/docs/guide.md`](../starter/docs/guide.md). It has
  **no sync note** (it is the source); it carries the `Based on decision-trail v2.13`
  provenance citation instead. Its "How to start" / "Where to go next" are written
  in the **adopter** voice.
- **Derived rendering:** this repo's [`guide.md`](../guide.md). Its header carries
  the sync note that currently claims *"The only delta is paths"* (the false claim).
  Its "How to start" / "Where to go next" are written in the **home-repo** voice
  (adoption lead-in; construction-log further-reading).
- The two forked sections' current wording is already correct per audience — the
  work is to **declare and mechanize** the fork, not to rewrite the prose meaning.
- ADR-0032 keeps the derived model, single-source direction (canonical = the
  `starter/` copy), and never-hand-patch rule intact.

### Carrier design (task 1 outcome) — Design B: preserve-in-place

The audience-forked sections are handled by the **existing `AGENTS.md`
non-derived-span pattern**, not by embedding variants in the canonical guide:

- The home-repo variant of each forked section lives **only in the derived home
  [`guide.md`](../guide.md)** — where it already is.
- The **derived guide's sync note is the carrier**: it names the forked sections
  and instructs a regeneration to **preserve the home file's existing text** for
  them (path-substitute + copy every other section from canonical; leave forked
  sections untouched).
- Lightweight HTML-comment **boundary markers** bracket each forked section **in the
  home `guide.md` only**, making the preserve-span unambiguous.
- The canonical [`starter/docs/guide.md`](../starter/docs/guide.md) stays **clean
  adopter text** — no home-variant embedding, so adopters copying it inherit **zero
  home-only clutter** (Genericity #7).

Rationale: embedding variants in the canonical guide (the ADR's literal sketch)
would pollute every adopter, since `starter/docs/guide.md` is copied verbatim into
adopter repos (ADR-0022/0031). Design B fits ADR-0032's allowed alternative — *"an
explicit marker of what each audience gets"* — located in the derived file, and
reuses the settled `AGENTS.md` preserve-on-regen pattern instead of inventing a
comment-embedding mechanism.

## Tasks

- [x] **Design the per-audience variant carrier.** → **Design B (preserve-in-place)**,
  recorded above.
- [x] **Mark the two forked sections in the derived home guide.** Bracketed "How to
  start" (lines 268/289) and "Where to go next" (lines 397/412) in
  [`guide.md`](../guide.md) with `AUDIENCE-FORKED SECTION … BEGIN/END` HTML-comment
  markers pointing at the header sync note + ADR-0032. Canonical
  `starter/docs/guide.md` left untouched.
- [x] **Rewrite the derived home guide's sync note to tell the truth.** Replaced
  *"The only delta is paths"* with the closed delta set — (1) paths, (2) named
  audience-forked sections ("How to start", "Where to go next") preserved from
  clobbering — citing ADR-0032/ADR-0014, and naming the forked sections explicitly.
- [x] **State the mechanical regeneration rule in the sync note.** Added a
  `Regeneration rule` comment block after the sync note: unmarked sections are
  copied from canonical with the path delta only; `AUDIENCE-FORKED` spans are
  preserved verbatim, never flattened to canonical — the `AGENTS.md` derived-span
  pattern.
- [x] **Verify the home guide's forked sections match their intended home variant.**
  Confirmed: "How to start" carries the clone/`adopting.md` lead-in; "Where to go
  next" points at `AGENTS.md` / `decisions/` / `adopting.md`. No drift between the
  declared home variant and the rendered text.
- [x] **Audit the spec rendering pair for undeclared audience deltas.** Audit
  complete: **one spec-side fork FOUND** — canonical `working-method.md` "How to
  start working" carries an adopter-only tail (the `0001-adopt-decision-trail.md`
  note + the `adopting.md` (re)adopt/update pointer) that home `AGENTS.md` omits,
  not covered by ADR-0014's four deltas. **Remediation applied** (see next task).
- [x] **Reconcile the enumerated-delta wording with ADR-0032.** Guide sync note
  enumerates the class. Canonical `working-method.md` sync note gained a fifth
  delta declaring the audience-forked "How to start working" adopter-only tail;
  home `AGENTS.md` derived-body rule now lists that tail as omitted-on-regen per
  ADR-0032.
- [x] **Dry-run a regeneration of the derived guide** from the annotated canonical
  source. Confirmed: unmarked sections copy + path-substitute; the two
  `AUDIENCE-FORKED` spans are preserved, so the home adoption lead-in and
  construction-log further-reading survive and the adopter's 2.13 close is not
  pulled in.

## Done when

- The derived home guide's sync note states the true delta set (paths + named
  audience-forked sections) and carries the mechanical regen rule.
- The derived home guide marks its two forked sections with `AUDIENCE-FORKED`
  BEGIN/END markers and holds the home variant in place; the canonical guide stays
  clean adopter text (Design B — no adopter pollution).
- A dry-run regeneration preserves the home-only adoption lead-in and construction-
  log further-reading (the 2.13 patch is no longer a latent casualty).
- The spec-pair audit is recorded (one fork found and folded into the
  audience-forked class across `working-method.md` + `AGENTS.md`).
