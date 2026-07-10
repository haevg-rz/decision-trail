# Idea: harden next-slot numbering so it can't collide

- Date: 2026-07-10
- Status: promoted
- Promoted to: [ADR-0025](../decisions/0025-harden-slot-numbering-with-collision-proof-procedure.md)

## Observation

A real bug surfaced: when creating a new idea, the agent found "the next number"
with a lazy glob like `00*` and reused a number already in use — producing **two
`0010` ideas** in this repo. The *same* collision happened independently in a
consumer repo, so this is not a one-off slip but a repeatable failure mode.

[ADR-0015](../decisions/0015-artifact-numbering-is-ordinal-only.md) already
settles that artifact numbers are **ordinal only — always the next free slot**.
But it states the *rule* without a *reliable procedure*. A careless slot-scan
(e.g. globbing `00*` and eyeballing the first apparent gap, or trusting a glob's
ordering) silently violates the rule while looking like it obeys it.

A number collision is corrosive out of proportion to how trivial it looks:

- Duplicate numbers break the **one-number-one-artifact identity** that every
  cross-link field (`Promoted from:`, `Implements:`, `Parent:`, …) and the derived
  `overview.md` rely on.
- The mechanical repair is costly and error-prone: renumbering the intruder — or,
  to preserve the human-readable timeline, inserting at the right slot and
  **shifting every later artifact** — means rewiring reciprocal links, prose
  references across ADRs/plans/CHANGELOG, and regenerating `overview.md`.

## Candidate direction

Harden the ordinal-numbering guidance (amending ADR-0015) with a **collision-proof
slot procedure** the agent must follow when creating an artifact, rather than the
current bare rule:

- Enumerate the **whole family** (`ideas/`, `decisions/`, `plans/` independently).
- Take **`max(existing number) + 1`** — never the first apparent gap a glob
  surfaces, and never a number derived from a related artifact.
- **Verify the target filename is unused** before writing.

Consider expressing this as explicit agent steps in `AGENTS.md` and the `starter/`
hand-off, and possibly a lightweight **conformance check** that flags duplicate
numbers within a family (a natural companion to the existing conformance check
from ADR-0022).

## Framing

A use-phase refinement of the method, made decision-trail as an ADR that **amends
ADR-0015** (the numbering-is-ordinal decision), not a redesign.

## Open questions

- Amend ADR-0015 in place, or record a new standalone ADR that supersedes/amends
  its procedural half?
- Should a **duplicate-number detection** step join the conformance check, so the
  wart is caught even when it slips in?
- How prescriptive should the procedure be — spell out `max+1` and the
  existence check explicitly, without over-engineering a simple task?
- Is `max+1` always right, or should the timeline-preserving **insert-and-shift**
  case (used to repair this very collision) also be documented as the sanctioned
  way to slot an out-of-order artifact?
