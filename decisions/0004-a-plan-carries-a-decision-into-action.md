# ADR-0004: A plan carries a decision into action; execution is the plan in motion

- Status: accepted
- Date: 2026-06-28
- Amended by: [ADR-0037](0037-plans-are-mechanical-execution-questions-return-to-the-decision-stage.md)

## Context

The lifecycle runs idea → proposal → decision → plan → execution (promise #4).
ADR-0001 to ADR-0003 settled the first three stages, all sharing one ADR family
under `decisions/`. The last two — **plan** and **execution** — still have no
mechanism.

Promise #8 names *spec-driven stages* as a standard to borrow. Modern
spec-driven flows (e.g. spec-kit, Kiro) separate **spec** (what / why) →
**plan** (how) → **tasks** (the steps) → **implement**. We want to borrow this,
but without importing weight we do not need:

- **Economy** (#2): the *what / why* of any work already lives in the accepted
  ADR that authorized it. A separate spec file would duplicate that.
- **Lifecycle** (#4): the hand-off decision → plan → execution must stay
  continuous and traceable back to the decision.
- **Agility** (#5): a plan must be revisable — tasks added or removed, the whole
  plan abandoned — without erasing the trail.
- **Transparency** (#3): progress must be visible in plain markdown, not inside
  an external tracker.

ADR-0003 set a precedent worth reusing: rather than invent a separate artifact
for an adjacent stage, it folded the *proposal* into the *decision* file as a
status. We apply the same economy to *execution* and the *plan*.

## Decision

A **plan** is a markdown file that carries an accepted decision into action.
**Execution** is that plan being worked — not a separate artifact.

- Plans live in the top-level `plans/` directory, one file per plan named
  `NNNN-kebab-case-title.md` (same numbering convention as ideas and ADRs).
- The accepted **ADR is the spec**: a plan does not restate what or why, it only
  records *how*. A plan carries:
  - **Status**: one of `draft`, `active`, `done`, `abandoned`,
  - **Implements**: a link to the ADR (or ADRs) it carries out,
  - a **task checklist** written in GitHub's portable task-list markdown
    (`- [ ]` / `- [x]`) — a borrowed, tool-independent format (#8).
- **Execution is the plan in motion.** Just as a proposal *becomes* a decision
  in place (ADR-0003), a plan is executed by moving `draft` → `active` → `done`
  while its checkboxes are ticked. There is no fifth-stage artifact.
- A plan that is dropped before completion is marked `abandoned` and left in
  place; plans are append-only (Agility #5). Tasks may be added or struck
  through as the plan evolves.

## Consequences

- All five lifecycle stages now have a mechanism, spread across just three
  artifact families: `ideas/` (idea), `decisions/` (proposal + decision), and
  `plans/` (plan + execution). idea → proposal → decision → plan → execution is
  fully walkable in plain markdown.
- Every plan links back to the decision it implements, so a returning session
  can trace any piece of work to the reason it exists (Continuity #1).
- Collapsing the spec into the ADR keeps the borrow from spec-driven development
  without duplicating intent — the template scales down to a generic,
  non-code project (Genericity #7).
- Progress lives in checkbox state inside the plan file, visible to any reader
  with no tooling (Transparency #3). The cost is that we do not get a tracker's
  automation; an acceptable trade for promises #3 and #8.
- With the lifecycle now fully assigned, the next open questions are no longer
  *which mechanism* but *how the repo is laid out* to hold these families, and
  how the parts cross-link. Those are future ADRs.
