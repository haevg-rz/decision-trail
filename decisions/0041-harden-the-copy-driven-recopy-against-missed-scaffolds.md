# ADR-0041: Harden the copy-driven re-copy against a silently missed scaffold

- Date: 2026-07-17
- Status: accepted
- Promoted from: [idea 0035](../ideas/0035-copy-driven-update-can-silently-miss-a-shipped-scaffold.md)
- Amends: [ADR-0022](0022-every-release-ships-reliable-update-instructions.md)

## Context

`updating.agent.md` step 2 tells the agent to copy `starter/`'s **own contents**
into the adopter's `docs/` — `starter/` is the single source of truth, no manifest
(ADR-0022). But the instruction is followed by an *example list*
(`working-method.md`, `guide.md`, `travel-diary.md`, `intermediate-artifacts/`) that
omits `scripts/` and reads as if it were the whole set.

A real update to **v2.18** anchored on that list: it bumped the citation and applied
the (empty) migration note, but never copied `docs/scripts/regen-overview.ps1` (the
script v2.18 ships in `starter/docs/scripts/`, ADR-0040). The adopter now cites v2.18
while missing a scaffold v2.18 ships. The migration note was correctly "none" — new
scaffolds are meant to arrive automatically via the step-2 copy (ADR-0021/0022) — so
the sole failure is step 2: a list that *looks* complete overrode "copy everything."

## Considered Options

1. **Hardcode the missing file** — add `scripts/` to the list. Fixes this scaffold,
   but the next new subtree repeats the identical bug; it patches the symptom.
2. **Make the list explicitly non-exhaustive (chosen)** — reframe it as *examples*
   of a "copy everything under `starter/`" rule, so no list can ever again be read as
   a closed set. Fixes the whole class at the cause.

## Decision

Adopt option 2. In `updating.agent.md` step 2, reframe the parenthetical as
explicitly non-exhaustive — *"copy **everything** under `starter/`, including but not
limited to `working-method.md`, `guide.md`, `travel-diary.md`,
`intermediate-artifacts/`, and `scripts/`"* — so the examples can no longer override
the "copy everything" instruction. `starter/` stays the single source of truth; no
manifest is introduced. This **amends ADR-0022** in execution detail only — the
copy-driven mechanics are unchanged.

Ship it as a **patch release (2.18.1)** — a pure bugfix, no new behavior — whose
`CHANGELOG` migration note is **not "none"**: it
tells existing adopters to re-run the step-2 copy (or minimally confirm
`docs/scripts/regen-overview.ps1` is present, copying it if absent) — the only
channel that reaches an adopter already stranded on v2.18-without-script — and records
that the omission surfaced from a real adopter update. This remediates a *past
delivery failure*; it does **not** start enumerating scaffolds in migration notes
(that contract is unchanged).

## Consequences

- **The class is fixed at the cause** — no example list can be read as exhaustive
  again, so a future scaffold in any subtree is covered, not just `scripts/`.
- **ADR-0022 untouched in substance** — this is an execution-detail amendment; on
  acceptance add the reciprocal `Amended by: ADR-0041` to ADR-0022.
- **The stranded adopter is fixed** via the non-"none" migration note; the
  `updating.agent.md` edit alone could not reach a past adopter.
- **Audience split preserved (ADR-0031)** — the change is agent-facing procedure
  only; the human trigger and `adopting.md` are untouched.
- **Deliberately not added:** a post-copy tree-parity check and a conformance-check
  item were weighed as belt-and-suspenders and dropped as over-engineering for a
  misleading-list bug; the non-exhaustive rule addresses the cause directly.
- **Follow-on:** on acceptance, a `draft` stub plan `Implements:` this ADR to edit
  step 2, add the `CHANGELOG` **2.18.1** entry with the remediating note, bump the
  three `starter/` citations to **v2.18.1**, and add the reciprocal
  `Amended by: ADR-0041` to ADR-0022.
