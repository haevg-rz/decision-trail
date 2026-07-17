# Plan 0030: Harden updating.agent.md step 2 and ship the 2.18.1 bugfix release

- Date: 2026-07-17
- Status: done
- Implements: [ADR-0041](../decisions/0041-harden-the-copy-driven-recopy-against-missed-scaffolds.md)

Mechanical execution of ADR-0041: reframe `updating.agent.md` step 2's example list
as explicitly non-exhaustive (so no list can be read as a closed set and drop a
shipped scaffold like `docs/scripts/regen-overview.ps1`), then ship it as the
**2.18.1** patch release whose `CHANGELOG` migration note remediates the already-
stranded v2.18 adopter. `starter/` stays the single source of truth; no manifest is
introduced; ADR-0022's mechanics are unchanged (execution-detail amendment only).

## Tasks

- [x] Edit `updating.agent.md` step 2: reframe the parenthetical as *"copy
      **everything** under `starter/`, including but not limited to
      `working-method.md`, `guide.md`, `travel-diary.md`, `intermediate-artifacts/`,
      and `scripts/`"* — examples, not a closed set.
- [x] Add a `CHANGELOG.md` `[2.18.1]` entry with a **non-"none" `Adopter migration:`**
      note: re-run the step-2 copy (or minimally confirm
      `docs/scripts/regen-overview.ps1` is present, copying it if absent); record that
      the omission surfaced from a real adopter update.
- [x] Bump the three `starter/` provenance citations v2.18 → **v2.18.1**
      (`starter/AGENTS.md`, `starter/docs/working-method.md`, `starter/docs/guide.md`).
- [x] Verify the reciprocal `Amended by: ADR-0041` is present on ADR-0022 (added at
      acceptance).

