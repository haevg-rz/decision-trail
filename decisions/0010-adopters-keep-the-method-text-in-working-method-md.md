# 10. Adopters keep the method text in `docs/working-method.md`; `AGENTS.md` only points to it

- Status: accepted
- Date: 2026-06-28
- Amends: ADR-0009 (pins down the merge text; relocates the method body out of the adopter's `AGENTS.md`)

## Context

ADR-0009 said the working-method description "lives in the repository's root
`AGENTS.md`", and that an adopter who already has an `AGENTS.md` should "merge a
short 'How we work' pointer (to `docs/decisions/`) into it" rather than add a
second file. Two problems surfaced when this met a real adoption:

- **The pointer had no defined target and no defined wording.** "A short pointer
  to `docs/decisions/`" never said *what line* to paste, and `docs/decisions/`
  holds decision records, not the method itself.
- **A circular reference with the method text nowhere.** The full method body
  (the eight promises, the lifecycle, the cross-link vocabulary, how to work)
  lived *only* inside the starter's `AGENTS.md`. The seed
  `0001-adopt-the-way.md` points back to `AGENTS.md` for the method. So an
  adopter who reduces their existing `AGENTS.md` to "see `0001`" gets
  `AGENTS.md` → `0001` → `AGENTS.md`, with the actual method text living
  nowhere. That breaks the copy-not-reference, self-containedness rule ADR-0008
  was built on (Continuity #1, Transparency #3).

Underneath sat an inconsistency ADR-0009 left in place: a fresh adopter carried
the full method *in* `AGENTS.md`, while an existing-`AGENTS.md` adopter was told
to keep only a pointer — **two different adoption shapes**, contradicting
ADR-0009's own goal that "there is one way to adopt."

### Considered options

- **A — Existing `AGENTS.md` absorbs the full method section.** Keeps the method
  body in `AGENTS.md` everywhere. But it preserves the two-shapes problem
  (appended-into vs. is-the-file), and taking a newer the-way means surgically
  re-merging a section inside a possibly heavily-customized `AGENTS.md` — messy
  and error-prone against Economy (#2).
- **B — Move the method body to a dedicated file; `AGENTS.md` only points.**
  One uniform adoption path; taking a newer version is replacing one
  self-contained file (a clean diff). The cost is an extra file, and naming it
  must not reintroduce a brand footprint (#7, #8) — `the-way.md` would partly
  undo ADR-0009.

### Decision drivers

A single adoption path and a clean, file-level version re-copy (Economy #2,
Continuity #1) outweigh the cost of one extra file — provided the filename
carries no brand. An unbranded, self-descriptive `working-method.md` satisfies
that.

## Decision

The borrowed method text lives in its own conventional file, and `AGENTS.md`
carries only a fixed pointer — the same in every adopting repo.

- **The method body lives in `docs/working-method.md`** — an unbranded,
  self-descriptive filename that carries the *"Based on the-way vX.Y"*
  provenance citation. It holds the contract, lifecycle, layout, cross-link
  vocabulary, and how-to-work text.
- **`AGENTS.md` carries only a fixed "How we work" pointer block**, identical
  whether the repo is fresh or already had an `AGENTS.md`. A fresh adopter's
  `AGENTS.md` *is* this block; an existing-`AGENTS.md` adopter **appends** this
  block. This is the single, precise text the merge step was missing:

  ```markdown
  ## How we work

  This project follows **the-way** — a generic method for carrying a thought
  through its whole life (idea → proposal → decision → plan → execution) in plain
  markdown. The full method is in [`docs/working-method.md`](docs/working-method.md);
  decision records live in [`docs/decisions/`](docs/decisions/), starting with
  [`0001-adopt-the-way.md`](docs/decisions/0001-adopt-the-way.md).

  Based on the-way vX.Y — https://github.com/ckluth/the-way
  ```

- **The circular reference is closed.** `0001-adopt-the-way.md` points to
  `docs/working-method.md` for the method text, not back to `AGENTS.md`.
- **One adoption path.** Copy the starter into the repo root; `docs/` (including
  `docs/working-method.md`) merges cleanly, and `AGENTS.md` is either created
  from the pointer block or has the pointer block appended. No file ever needs a
  hand-merge of the method body.

## Consequences

- An adopting repo is fully self-contained again: the method text physically
  lives in `docs/working-method.md`, readable offline, with no pointer that
  dead-ends (Continuity #1, Transparency #3).
- Taking a newer the-way is now a clean, file-level operation: replace
  `docs/working-method.md` and bump the citation, instead of re-merging prose
  inside a customized `AGENTS.md` (Economy #2).
- One uniform adoption shape replaces ADR-0009's implicit two, and the merge
  step finally has exact, copy-pasteable wording.
- The `starter/` skeleton is restructured: `AGENTS.md` becomes the pointer block,
  and the method body moves to `starter/docs/working-method.md`.
- `working-method.md` is unbranded, so it adds no brand footprint — the name
  "the-way" still survives only as the method's name and a provenance citation
  (Genericity #7, Borrow #8).
- This is a post-v1.0.0 refinement; it ships in the next version (see
  `CHANGELOG.md`).
