# ADR-0015: Artifact numbering is ordinal only — always use the next free slot

Date: 2026-06-29
Status: accepted
Promoted from: [Idea-0007](../ideas/0007-artifact-numbering-is-ordinal-only.md)

## Context

In a consuming repo an agent numbered a plan `0004` because it implemented
ADR-0004 — mirroring the ADR number rather than taking the next free slot in
the plans family. The plan was in fact the first plan ever written; its correct
number was `0001`.

The method never explicitly stated that numbers have no semantic meaning, which
left room for this misinterpretation.

## Decision

Artifact numbers are **purely ordinal**: they give an artifact a stable,
sortable identity within its family and nothing more.

Rules:

1. **No relational meaning.** A plan numbered `0004` does not imply it
   implements ADR-0004. Matching numbers across families is coincidence, never
   intent.
2. **Next free slot, always.** When creating an artifact, scan the target family
   (`ideas/`, `decisions/`, `plans/`) and assign the next unused four-digit
   number — regardless of the numbers of any artifacts it relates to.
3. **Relationships live in cross-link fields only.** The connection between a
   plan and the decision it implements is expressed via `Implements:`, not via a
   shared number.

## Consequences

- Agents and humans have an unambiguous rule: look at the family folder, find
  the highest existing number, add one.
- The cross-link fields (`Implements:`, `Promoted to:`, etc.) remain the sole
  authoritative record of relationships between artifacts.
- This rule must be stated explicitly in both `AGENTS.md` and
  `starter/docs/working-method.md` so it is visible to agents in every context.
