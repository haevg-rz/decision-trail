# the-way

A generic, reusable way to work on projects — economic, transparent, agile.
This is the **single source of truth** and the entry point: read it first, then
navigate from here. Tool-specific files (e.g.
[`.github/copilot-instructions.md`](.github/copilot-instructions.md)) only point
back to this file.

> **Status: settled (not frozen).** The concept phase is logically complete —
> the contract and all mechanics below are decided and recorded as ADRs in
> [`decisions/`](decisions/). The method now exists to be *used*; real use will
> bring improvements, and any such change is made *the-way* — as a new ADR.

## What this is

`the-way` is a method for carrying a thought through its whole life, in plain
markdown, borrowing existing standards rather than inventing new ones.

### How it arose (two shifts)

1. Started on a concrete project (**my-second-brain**) and wanted a *reasonable,
   structured, reproducible, economic way to work* on it.
2. Realized that way-of-working should be **generic** — reusable for any project.

So the subject became *"a generic way to work on projects,"* developed
concept-first. my-second-brain becomes simply the first project that will adopt
the method. A quiet irony: this method, fully formed, is exactly the thing that
would tell us how to develop ideas like itself. It is its own first subject.

### The contract — eight promises

1. **Continuity** — pick up cheaply after the session ends and context is gone.
2. **Economy** — minimize the cost of re-gathering; cheap to write, cheap to resume.
3. **Transparency** — everything in plain, human-readable markdown; nothing hidden in a tool.
4. **Lifecycle for thoughts** — a thought can travel: idea → proposal → decision → plan → execution.
5. **Agility** — any thread can be refined or overthrown at any time; nothing is locked.
6. **Budding** — one idea can spawn another; the parent-child link is kept.
7. **Genericity** — none of this is bound to a particular project.
8. **Borrow, don't invent** — lean on existing portable standards (ADRs,
   spec-driven stages, agent hand-off files like `AGENTS.md` /
   `copilot-instructions.md`); invent nothing we can borrow. Guards against
   building a proprietary harness.

## The lifecycle

A thought travels: **idea → proposal → decision → plan → execution.** Each stage
has a home, across three artifact families:

| Stage | Where it lives | Status values |
|-------|----------------|---------------|
| idea | `ideas/NNNN-*.md` | `seed` → `promoted` / `dropped` |
| proposal | `decisions/NNNN-*.md` | `proposed` |
| decision | `decisions/NNNN-*.md` (same file) | `accepted` / `rejected` |
| plan | `plans/NNNN-*.md` | `draft` → `active` → `done` / `abandoned` |
| execution | `plans/NNNN-*.md` (same file) | the plan ticking its checkboxes |

- **Ideas** are cheap to write; a matured idea is *promoted* to a proposal.
- **Decisions** are [ADRs](decisions/) — a proposal *becomes* a decision in
  place when accepted.
- **Plans** carry an accepted decision into action; the ADR is the spec, the
  plan is the *how*, and execution is the plan in motion. Tasks use GitHub
  task-list markdown (`- [ ]` / `- [x]`).

## Layout

```
ideas/        idea artifacts
decisions/    proposal + decision artifacts (ADRs)
plans/        plan + execution artifacts
.github/      the contract and agent hand-off files
AGENTS.md     this entry point
```

When the method is adopted into another project, these families nest under a
single `the-way/` root to avoid colliding with the host project's folders. In
*this* repository, the repo root itself is that root.

## Cross-link vocabulary

Artifacts reference each other with relative markdown links and fixed,
greppable field names in their headers:

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

1. Capture a thought as an idea in `ideas/`.
2. When it matures, open an ADR in `decisions/` with `Status: proposed`.
3. Accept or reject it; an accepted ADR is a decision.
4. Write a `plans/` file that `Implements:` the decision and lists tasks.
5. Execute by moving the plan `active` → `done`, ticking checkboxes.

## Why it is this way

Every mechanic above was decided one step at a time, each recorded as an ADR.
Read [`decisions/`](decisions/) in order to see the reasoning — the method
documents its own construction.

## Working in this repo (agent guidance)

- **The method is settled.** Use it; don't redesign it casually. Any change to
  the-way itself is made the-way — proposed and recorded as a new ADR, with
  amended or superseded ADRs cross-linked (never edited away).
- **Confirmation guard.** Never rush into writing, editing, or implementing.
  First briefly explain what you intend to do, then wait for explicit approval.
  Discussing and proposing is always fine — acting requires a green light.
