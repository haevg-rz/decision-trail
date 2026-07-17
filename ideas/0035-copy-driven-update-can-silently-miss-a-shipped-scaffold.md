# Idea 0035: The copy-driven "bring me current" update can silently miss a shipped scaffold

- Date: 2026-07-17
- Status: promoted
- Promoted to: [ADR-0041](../decisions/0041-harden-the-copy-driven-recopy-against-missed-scaffolds.md)

## The itch — a real adopter miss

`updating.agent.md` step 2 ("Re-copy the method-owned set") tells the agent to copy
`starter/`'s **own contents** into the adopter's `docs/`. That normative instruction
is correct and complete. But it is immediately followed by a *parenthetical example
list* — `working-method.md`, `guide.md`, `travel-diary.md`,
`intermediate-artifacts/` — and that list omits `scripts/`.

A real downstream update to **v2.18** anchored on the example list rather than the
normative "copy `starter/`'s contents": it bumped the citation and applied the
(empty) `Adopter migration:` note, but **never copied the new
`docs/scripts/regen-overview.ps1`** that v2.18 introduced in
`starter/docs/scripts/`. Result: an adopter cited as v2.18 but **missing a scaffold
that v2.18 ships** — a silent conformance gap.

## Why the safety nets did not catch it

This gap is invisible on purpose to two of the three mechanisms:

- The **`Adopter migration:` note is "none"** — and correctly so. Per the ADR-0021 /
  ADR-0022 contract, *new optional scaffolds are deliberately not enumerated in
  migration notes*; they are supposed to arrive **automatically via the step-2
  re-copy**. So the migration note is doing exactly what it should — it is step 2
  that failed to deliver.
- The **conformance check** verifies headers, numbering, overview sync, and the
  citation — but has **no item asserting the shipped scaffolds are present**. So a
  missing `regen-overview.ps1` passes conformance clean.

The only mechanism that *should* have caught it — step 2's re-copy — is where the
bug lives.

## Root cause

Step 2's **normative** instruction is right ("copy `starter/`'s own contents — the
single source of truth; there is no separate manifest"). The **illustrative** list
beside it is wrong-by-omission: it reads as exhaustive to an executing agent, who
then narrows the copy scope to the named items and skips the unlisted `docs/scripts/`
subtree. A list that *looks* complete quietly overrides the instruction that says
"copy everything."

## Directions to weigh (for the proposal, not this seed)

Three levers, not mutually exclusive — the real-world miss argues for defence in
depth, but each has a cost:

1. **Fix the list.** Add `scripts/` and reframe the list as *explicitly
   non-exhaustive* ("copy everything under `starter/`, including but not limited
   to …"), so no future scaffold can be dropped by anchoring on the examples.
   Cheapest; removes *this* class of miss but relies on the agent still honouring
   "everything."
2. **Verify after copying — tree parity.** After the copy, assert that every file
   under `<source>/starter/` now exists at the adopter's mirrored `docs/` path, and
   flag any gap. Turns a silent drop into a caught one for *any* scaffold, present or
   future — at the cost of an enumerate-both-trees step every update.
3. **Add a conformance-check item.** "If the cited version ships
   `docs/scripts/regen-overview.ps1`, the adopter has it too" — so the end-of-update
   check (and any standalone conformance run) catches a missing shipped scaffold even
   if steps 1–2 were skipped. A backstop, keyed to the one scaffold we know shipped.

## Boundaries this must respect

- **Copy-driven contract (ADR-0022).** `starter/`'s contents stay the single source
  of truth; no separate manifest is introduced. Any fix reinforces "copy everything
  under `starter/`", it does not replace it with an enumerated list.
- **Human-intent / agent-execution split (ADR-0031).** The human trigger stays the
  one plain intent; all of this is agent-executed procedure in `updating.agent.md`.
  No new human step.

## Not yet decided

Which of the three levers to adopt (the miss argues for all three, but the proposal
must weigh the tree-parity step's per-update cost); whether this is recorded as an
ADR amending ADR-0022 and shipped as a version whose migration note remediates the
already-stranded v2.18 adopter. That belongs to the proposal, not this seed.
