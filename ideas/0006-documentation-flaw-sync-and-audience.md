# Idea: documentation flaw — sync and audience

- Date: 2026-06-28
- Status: promoted
- Promoted to: [ADR-0014](../decisions/0014-sync-method-renderings-and-separate-audiences.md)

## Observation

Two related problems noticed in the current documentation:

### 1. AGENTS.md and starter/docs/working-method.md are out of sync

`AGENTS.md` (the method's own home) and `starter/docs/working-method.md` (the
template an adopter copies) cover overlapping ground but have drifted apart.
Examples of divergence:

- The lifecycle table uses bare paths (`ideas/`, `decisions/`) in `AGENTS.md`
  but `docs/`-prefixed paths (`docs/ideas/`, `docs/decisions/`) in
  `working-method.md` — correct per context, but the surrounding prose is not
  always consistent.
- `working-method.md` has a richer ADR bullet (mentions the classic template,
  Decision Drivers, Considered Options); `AGENTS.md` does not.
- `working-method.md` describes `docs/overview.md` in the lifecycle section
  with more detail than `AGENTS.md` does.
- `AGENTS.md` references ADR numbers (ADR-0011, ADR-0012) inline; `working-method.md`
  intentionally omits them (correct for an adopter's copy, but the gap is implicit).
- The "How to start working" paths differ (`ideas/` vs `docs/ideas/` etc.).

There is no single statement of *which file is authoritative for what*, and no
process to keep them aligned when one changes.

### 2. Audience separation: agent guidance vs. human user manual

Both files mix two distinct concerns:

- **Agent guidance** — instructions to an AI agent (confirmation guard, keep
  overview.md current, method is settled, etc.)
- **Human user manual** — how a person reads and uses the method

Currently `AGENTS.md` carries agent guidance in a dedicated section at the end,
but the bulk of both files is method description that serves both audiences.
The question is: is a mixed file acceptable, or should the two concerns be
clearly separated — and if so, where?

## Open questions

- Should `AGENTS.md` remain the single source of truth for the method in this
  repo, with `working-method.md` being a *derived/stripped* copy for adopters?
- Or should there be an explicit sync rule / shared excerpt that both files
  include verbatim?
- Is the audience question (agent vs. human) a reason to split files, or just
  a reason to add a clear section header?
- Does the agent-guidance section belong only in `AGENTS.md` (this repo) and
  the adopter's `AGENTS.md`, or also in `working-method.md`?
