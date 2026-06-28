# 1. Record decisions as ADRs

- Status: accepted
- Date: 2026-06-28
- Amended by: ADR-0003 (status vocabulary extended)

## Context

`the-way` is a generic method for working on projects. Its *contract* — the
eight promises in `.github/copilot-instructions.md` — is settled, but its
concrete mechanics (lifecycle file shapes, repo layout) are deliberately
undecided. We will make those decisions one at a time, step by step.

Several of the eight promises bear directly on *how* we make and keep decisions:

- **Continuity & Economy** (#1, #2): a future session, with no memory of this
  one, must be able to pick up cheaply. Decisions therefore have to be written
  down in a durable, low-cost form.
- **Transparency** (#3): the record must be plain, human-readable markdown,
  nothing hidden inside a tool.
- **Borrow, don't invent** (#8): we must lean on an existing portable standard
  rather than design a bespoke decision format.

Architecture Decision Records (ADRs), introduced by Michael Nygard, are exactly
such a standard: small, numbered, append-only markdown files that capture the
context and consequences of a single decision. They are widely adopted and
tool-agnostic.

This is the first decision we make, so it must also bootstrap *the way we record
decisions*. ADR-0001 records its own mechanism.

## Decision

We record every non-trivial decision about `the-way` as an ADR.

- ADRs live in the top-level `decisions/` directory.
- Each ADR is one markdown file named `NNNN-kebab-case-title.md`, where `NNNN`
  is a zero-padded sequence number starting at `0001` (adr-tools / MADR
  naming convention).
- Each ADR follows Nygard's lightweight template: a title, a **Status**, a
  **Context**, the **Decision**, and its **Consequences**.
- `Status` is one of `proposed`, `accepted`, `superseded`, or `deprecated`. A
  superseded ADR is left in place and links to the ADR that replaces it; ADRs
  are append-only, never edited away. This realizes the **Agility** promise (#5):
  any decision can be overthrown later without erasing the trail.

## Consequences

- From now on, choices about lifecycle mechanics, file shapes, and repo layout
  are captured here as numbered ADRs — the method begins to eat its own dog
  food.
- A returning session can reconstruct *why* the project looks the way it does by
  reading `decisions/` in order, at near-zero cost.
- We have committed to a borrowed standard, not a proprietary harness, keeping
  promise #8 intact.
- ADRs cover the **decision** stage of the lifecycle (idea → proposal →
  decision → plan → execution). The other stages are not yet assigned a
  mechanism; those are future ADRs.
