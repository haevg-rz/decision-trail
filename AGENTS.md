# decision-trail

A generic, reusable way to work on projects — economic, transparent, agile.

<!--
Sync note — this file is a DERIVED rendering.
The canonical method spec is `starter/docs/working-method.md`. This file's method
text is regenerated wholesale from it, never hand-patched. The only legitimate
differences (deltas) from the canonical text are:
  - paths: this repo uses repo-root families (`ideas/`, `decisions/`, `plans/`);
    adopters use `docs/`-prefixed ones;
  - construction-ADR cross-references (ADR-00NN) appear here, not in the canonical
    text;
  - no `Based on decision-trail vX.Y` provenance citation (this repo IS the method);
  - entry-point framing: here `AGENTS.md` carries the method text; an adopter's
    `AGENTS.md` points to `docs/working-method.md`.
Edit the method in `starter/docs/working-method.md`; regenerate this file.
-->

This file is the terse **reference** for *how we work* — the contract, lifecycle,
layout, cross-link vocabulary, and how to start. For a narrative introduction that
teaches the method, read [`guide.md`](guide.md). For *why* the method is the way it
is, read [`decisions/`](decisions/) in order — it documents its own construction.

> **Status: settled (not frozen).** The concept phase is logically complete — the
> contract and all mechanics below are decided and recorded as ADRs in
> [`decisions/`](decisions/). The method now exists to be *used*; real use will
> bring improvements, and any such change is made *decision-trail* — as a new ADR.

## The contract — eight promises

1. **Continuity** — pick up cheaply after the session ends.
2. **Economy** — cheap to write, cheap to resume.
3. **Transparency** — plain, human-readable markdown; nothing hidden in a tool.
4. **Lifecycle for thoughts** — idea → proposal → decision → plan → execution.
5. **Agility** — any thread can be refined or overthrown; nothing is locked.
6. **Budding** — one idea can spawn another; the parent-child link is kept.
7. **Genericity** — nothing is bound to a particular project.
8. **Borrow, don't invent** — lean on existing portable standards (ADRs,
   spec-driven stages, agent hand-off files); invent nothing we can borrow.

## The lifecycle

A thought travels **idea → proposal → decision → plan → execution**, across three
artifact families:

| Stage | Where it lives | Status values |
|-------|----------------|---------------|
| idea | `ideas/NNNN-*.md` | `seed` → `promoted` / `dropped` |
| proposal | `decisions/NNNN-*.md` | `proposed` |
| decision | `decisions/NNNN-*.md` (same file) | `accepted` / `rejected` |
| plan | `plans/NNNN-*.md` | `draft` → `active` → `done` / `abandoned` |
| execution | `plans/NNNN-*.md` (same file) | the plan ticking its checkboxes |

- **Ideas** are cheap to write; a matured idea is *promoted* to a proposal.
- **Decisions** are [ADRs](decisions/) — a proposal *becomes* a decision in place
  when accepted. Use the classic template (Status / Context / Decision /
  Consequences); add **Decision Drivers** / **Considered Options** when weighing
  alternatives.
- **Plans** carry an accepted decision into action: the ADR is the spec, the plan
  is the *how*, execution is the plan in motion. Tasks use GitHub task-list
  markdown (`- [ ]` / `- [x]`).

Every idea, decision, and plan carries a `Date:` (creation date) in its header —
**mandatory**. `overview.md` is a derived status index over all three families: a
single dated snapshot of each artifact's name, creation date, and state. It is
**regenerated wholesale from the artifact headers** (never hand-patched) and
stamped "as of <date>" (ADR-0011). Keeping it current is the **agent's**
responsibility — regenerated after any work that creates an artifact or changes a
state, and whenever asked.

## Layout

```
guide.md      narrative introduction (read this first)
AGENTS.md     this file — the terse reference + agent guidance
overview.md   derived status index (regenerated dated snapshot, see ADR-0011)
ideas/        idea artifacts
decisions/    proposal + decision artifacts (ADRs)
plans/        plan + execution artifacts
starter/      clean skeleton an adopting project copies (see ADR-0008)
.github/      tool-specific agent hand-off files
CHANGELOG.md  released versions of the method
```

This layout is for *this* repository — the method's own home, where the families
sit at the repo root. An **adopting project does not copy this layout**; it uses
conventional `docs/` locations instead (see ADR-0009). To adopt decision-trail in
another project, copy the [`starter/`](starter/) skeleton — see its `AGENTS.md`,
`docs/guide.md`, and `docs/working-method.md`.

## Cross-link vocabulary

Artifacts reference each other with relative markdown links and fixed, greppable
field names in their headers:

| From | Field | To | Meaning |
|------|-------|----|---------|
| idea | `Parent:` | idea | budded from another idea |
| idea | `Promoted to:` / ADR `Promoted from:` | ADR | matured into a proposal (reciprocal) |
| ADR | `Amends:` / `Amended by:` | ADR | part of a decision changed |
| ADR | `Supersedes:` / `Superseded by:` | ADR | one decision replaces another |
| plan | `Implements:` | ADR | carries out a decision |

Forward link always; add the reciprocal back-link for amend/supersede **and
promotion**. A link is reciprocal only when *both* ends are single and write-once
(promotion: one idea ↔ one ADR); `Parent` and `Implements` stay forward-only
because their reverse side accumulates (one parent → many children; one ADR → many
plans). See ADR-0012.

## How to start working

1. Capture a thought as an idea in `ideas/`.
2. When it matures, open an ADR in `decisions/` with `Status: proposed`.
3. Accept or reject it; an accepted ADR is a decision.
4. Write a `plans/` file that `Implements:` the decision and lists tasks.
5. Execute by moving the plan `active` → `done`, ticking checkboxes.

## Agent operating guidance

These rules are for an AI agent working in this repo:

- **Artifact numbers are ordinal only.** When creating an artifact, assign the
  next unused number in that family (`ideas/`, `decisions/`, `plans/` are
  independent sequences). Never derive a number from a related artifact — a plan
  that implements ADR-0004 is not named `0004`; it gets the next free plan slot.
  Relationships are expressed via cross-link fields (`Implements:`, `Promoted
  to:`, etc.), never via matching numbers. (ADR-0015)
- **The method is settled.** Use it; don't redesign decision-trail casually. Any
  change to the method itself is made decision-trail — proposed and recorded as a
  new ADR, with amended or superseded ADRs cross-linked (never edited away).
- **Confirmation guard.** Never rush into writing, editing, or implementing. First
  briefly explain what you intend to do, then wait for explicit approval.
  Discussing and proposing is always fine — acting requires a green light.
- **Keep `overview.md` current.** It is a derived snapshot, regenerated wholesale
  from the artifact headers (never hand-patched) and stamped "as of <date>"
  (ADR-0011). Regenerate it — and update the stamp — whenever the user explicitly
  asks. A user may flip a state directly in an artifact; the next regeneration
  reconciles the index.
