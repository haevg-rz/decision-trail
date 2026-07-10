# Idea: artifact numbering is ordinal only — always use the next free slot

- Date: 2026-06-29
- Status: promoted
- Promoted to: [ADR-0015](../decisions/0015-artifact-numbering-is-ordinal-only.md)

## Observation

In a consuming repo an agent derived a plan from ADR-0004 and numbered it
`plan-0004`, mirroring the ADR number. The plan was in fact the first plan ever
written — its correct number was `0001`.

This reveals a gap in the guidance: the method never explicitly states that
numbers carry **no semantic meaning** beyond ordering. An agent (or human) can
mistakenly read a number as a reference to the artifact it implements and copy
it, breaking the "next free slot" invariant.

## Desired clarification

Add an explicit rule — visible in both AGENTS.md and working-method.md — stating:

- Numbers are **purely ordinal**: they exist only to give artifacts a stable,
  sortable identity.
- They carry **no relational meaning**: a plan numbered 0004 does not imply it
  implements ADR-0004.
- The only correct rule for assigning a number is **next free slot in that
  family** (ideas, decisions, plans are independent sequences).
- Relationships between artifacts are expressed exclusively through the
  cross-link fields (`Implements:`, `Promoted to:`, etc.), never through
  matching numbers.
