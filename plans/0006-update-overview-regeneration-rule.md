# Plan: update overview regeneration rule to explicit-request only

- Date: 2026-06-29
- Status: done
- Implements: [ADR-0016](../decisions/0016-overview-regeneration-on-explicit-request-only.md)

## Goal

Replace the "regenerate after every artifact change" rule with "regenerate only
when the user explicitly asks" in every location where the old rule is stated.

## Tasks

- [x] Update the `overview.md` bullet in `AGENTS.md` (agent operating guidance):
      remove "after any work that creates an artifact or changes a state";
      replace with "whenever the user asks".
- [x] Apply the same change to `starter/docs/working-method.md` (lifecycle
      section, where the overview rule is stated).
- [x] Apply the same change to `starter/AGENTS.md` (agent operating guidance
      bullet for `docs/overview.md`).
- [x] Regenerate `overview.md`.
