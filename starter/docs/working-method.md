# Working method — the-way

> This project works **the-way** — a generic, reusable method for carrying a
> thought through its whole life (idea → proposal → decision → plan →
> execution) in plain markdown.
>
> Based on **the-way vX.Y** — https://github.com/ckluth/the-way

This file is the full description of *how we work*. The repository's root
`AGENTS.md` only points here. What the project *is* belongs in its own README.

## The contract — eight promises

1. **Continuity** — pick up cheaply after the session ends and context is gone.
2. **Economy** — minimize the cost of re-gathering; cheap to write, cheap to resume.
3. **Transparency** — everything in plain, human-readable markdown; nothing hidden in a tool.
4. **Lifecycle for thoughts** — a thought can travel: idea → proposal → decision → plan → execution.
5. **Agility** — any thread can be refined or overthrown at any time; nothing is locked.
6. **Budding** — one idea can spawn another; the parent-child link is kept.
7. **Genericity** — none of this is bound to a particular project.
8. **Borrow, don't invent** — lean on existing portable standards (ADRs,
   spec-driven stages, agent hand-off files); invent nothing we can borrow.

## The lifecycle

A thought travels: **idea → proposal → decision → plan → execution.** Each stage
has a home, across three artifact families:

| Stage | Where it lives | Status values |
|-------|----------------|---------------|
| idea | `docs/ideas/NNNN-*.md` | `seed` → `promoted` / `dropped` |
| proposal | `docs/decisions/NNNN-*.md` | `proposed` |
| decision | `docs/decisions/NNNN-*.md` (same file) | `accepted` / `rejected` |
| plan | `docs/plans/NNNN-*.md` | `draft` → `active` → `done` / `abandoned` |
| execution | `docs/plans/NNNN-*.md` (same file) | the plan ticking its checkboxes |

- **Ideas** are cheap to write; a matured idea is *promoted* to a proposal.
- **Decisions** are ADRs — a proposal *becomes* a decision in place when accepted.
  Use the classic template (Status / Context / Decision / Consequences); add the
  optional **Decision Drivers** / **Considered Options** sections when weighing
  alternatives.
- **Plans** carry an accepted decision into action; the ADR is the spec, the plan
  is the *how*, and execution is the plan in motion. Tasks use GitHub task-list
  markdown (`- [ ]` / `- [x]`).

## Layout

```
AGENTS.md             repo root — points here (the "How we work" pointer)
docs/working-method.md  this file — the full method
docs/ideas/           idea artifacts
docs/decisions/       proposal + decision artifacts (ADRs)
docs/plans/           plan + execution artifacts
```

The decision records use `docs/decisions/` — the conventional location for
ADRs — so the structure reads as a normal, well-organized repo, with no
project-specific folders imposed.

## Cross-link vocabulary

Artifacts reference each other with relative markdown links and fixed, greppable
field names in their headers:

| From | Field | To | Meaning |
|------|-------|----|---------|
| idea | `Parent:` | idea | budded from another idea |
| idea | `Promoted to:` | ADR | matured into a proposal |
| ADR | `Amends:` / `Amended by:` | ADR | part of a decision changed |
| ADR | `Supersedes:` / `Superseded by:` | ADR | one decision replaces another |
| plan | `Implements:` | ADR | carries out a decision |

Forward link always; add the reciprocal back-link for amend/supersede so the
trail is walkable from either end.

## How to start working

1. Capture a thought as an idea in `docs/ideas/`.
2. When it matures, open an ADR in `docs/decisions/` with `Status: proposed`.
3. Accept or reject it; an accepted ADR is a decision.
4. Write a `docs/plans/` file that `Implements:` the decision and lists tasks.
5. Execute by moving the plan `active` → `done`, ticking checkboxes.

This repo's own `docs/decisions/0001-adopt-the-way.md` records the decision to
adopt the-way. Everything else starts from there.
