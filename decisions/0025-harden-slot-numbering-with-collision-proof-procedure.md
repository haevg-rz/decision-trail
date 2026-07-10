# ADR-0025: Harden next-slot numbering with a collision-proof procedure

- Date: 2026-07-10
- Status: accepted
- Promoted from: [Idea-0018](../ideas/0018-harden-slot-numbering-against-collisions.md)
- Amends: [ADR-0015](0015-artifact-numbering-is-ordinal-only.md)

## Context

[ADR-0015](0015-artifact-numbering-is-ordinal-only.md) settled that artifact
numbers are **ordinal only — always the next free slot**, with relationships
expressed via cross-link fields rather than matching numbers. But it states the
*rule* without a reliable *procedure* for finding that slot.

A real bug exposed the gap: creating a new idea, an agent found "the next number"
with a lazy `00*`-style glob and reused a number already in use — producing **two
`0010` ideas** in this repo. The **same** collision happened independently in an
adopter repo, so this is a repeatable failure mode, not a one-off slip.

A number collision is corrosive out of proportion to how trivial it looks:

- Duplicate numbers break the **one-number-one-artifact identity** that every
  cross-link field (`Promoted from:`, `Implements:`, `Parent:`, …) and the derived
  `overview.md` rely on.
- The repair is costly: renumbering the intruder — or, to preserve the
  human-readable timeline, inserting at the right slot and **shifting every later
  artifact** — means rewiring reciprocal links, prose references across
  ADRs/plans/CHANGELOG, and regenerating `overview.md`.

## Decision Drivers

- **Reliability** — the procedure must not be silently violable by a careless scan.
- **Economy (#2)** — a cheap, mechanical step, not added ceremony.
- **Borrow, don't invent (#8)** — reuse the plainest possible arithmetic (`max+1`).
- **Consistency** — fit the existing conformance check (ADR-0022) rather than add a
  parallel mechanism.

## Considered Options

1. **Amend ADR-0015** with an explicit collision-proof procedure carried into the
   method texts. *(Recommended.)*
2. **New standalone ADR** superseding ADR-0015's procedural half — heavier, splits
   one concern across two ADRs.
3. **Leave the rule as-is**, relying on agent care — rejected: it has already
   failed twice, in two repos.

## Decision

Take **Option 1** — amend ADR-0015. Add an agent-executable **slot procedure** to
`AGENTS.md` and the `starter/` hand-off:

- **Enumerate the whole family** (`ideas/`, `decisions/`, `plans/` are independent
  sequences).
- Take **`max(existing number) + 1`** — never the first apparent gap a glob
  surfaces, and never a number derived from a related artifact.
- **Verify the target filename is unused** before writing.

Additionally:

- Add a **duplicate-number detection** step to the conformance check (ADR-0022), so
  a collision is caught even if one slips in.
- Document the timeline-preserving **insert-and-shift** as the sanctioned way to
  slot an out-of-order artifact (renumber the intruder into place and shift later
  artifacts, rewiring cross-links and regenerating `overview.md`).

## Consequences

- Collisions become both **prevented** (the `max+1` + existence-check procedure)
  and **detectable** (the conformance step).
- Numbering guidance is slightly more prescriptive — a small, justified cost.
- ADR-0015's rule stands unchanged; only its *procedure* is sharpened, so no
  existing decision is overturned.
- On acceptance, the reciprocal `Amended by: ADR-0025` is added to ADR-0015, and a
  plan carries the method-text edits (Option 1's scope) into `AGENTS.md`,
  `starter/`, and the conformance check.
