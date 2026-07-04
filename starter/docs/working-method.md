# Working method — decision-trail (reference)

> This project works **decision-trail** — carrying a thought through its whole life
> (idea → proposal → decision → plan → execution) in plain markdown.
>
> Based on **decision-trail v2.7** — https://github.com/ckluth/decision-trail

<!--
Sync note — this file is CANONICAL.
This is the single source of truth for the method spec. This repo's `AGENTS.md`
(in the decision-trail repo) is a DERIVED rendering of this file; it is regenerated
wholesale, never hand-patched. The only legitimate differences (deltas) between
the two renderings are:
  - paths: adopters use `docs/`-prefixed families (`docs/ideas/`, `docs/decisions/`,
    `docs/plans/`); the decision-trail repo uses repo-root families;
  - construction-ADR cross-references (ADR-00NN) appear only in the decision-trail
    repo's rendering, not here;
  - the `Based on decision-trail vX.Y` provenance citation is adopter-only (this file);
  - entry-point framing: here `AGENTS.md` points to this file; in the decision-trail
    repo `AGENTS.md` carries the text.
Edit the method here; regenerate the other rendering.
-->

This file is the terse **reference** for *how we work* — the contract, lifecycle,
layout, cross-link vocabulary, and how to start. For a narrative introduction that
teaches the method, read [`guide.md`](guide.md). The repository's root `AGENTS.md`
points here and carries the agent operating guidance. What the project *is* belongs
in its own README.

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
| idea | `docs/ideas/NNNN-*.md` | `seed` → `promoted` / `dropped` |
| proposal | `docs/decisions/NNNN-*.md` | `proposed` |
| decision | `docs/decisions/NNNN-*.md` (same file) | `accepted` / `rejected` |
| plan | `docs/plans/NNNN-*.md` | `draft` → `active` → `done` / `abandoned` |
| execution | `docs/plans/NNNN-*.md` (same file) | the plan ticking its checkboxes |

- **Ideas** are cheap to write; a matured idea is *promoted* to a proposal.
- **Decisions** are ADRs — a proposal *becomes* a decision in place when accepted.
  Use the classic template (Status / Context / Decision / Consequences); add
  **Decision Drivers** / **Considered Options** when weighing alternatives.
- **Plans** carry an accepted decision into action: the ADR is the spec, the plan
  is the *how*, execution is the plan in motion. Tasks use portable task-list
  markdown (`- [ ]` / `- [x]`).

Every idea, decision, and plan carries a `Date:` (creation date) in its header —
**mandatory**. It may also carry an optional `Tags:` line — comma-separated tag
words naming cross-cutting themes; omit the line when empty (see **Tags** below).
Artifact numbers are **ordinal only**: assign the next unused
number in that family (`docs/ideas/`, `docs/decisions/`, `docs/plans/` are
independent sequences). Never derive a number from a related artifact — a plan
implementing ADR-0004 is not named `0004`; it takes the next free plan slot.
Relationships are expressed via cross-link fields (`Implements:`, `Promoted
to:`, etc.), never via matching numbers. `docs/overview.md` is a derived status index over all three
families: a single dated snapshot of each artifact's name, creation date, and
state. It is **regenerated wholesale from the artifact headers** (never
hand-patched) and stamped "as of <date>". Regenerate it whenever the user
explicitly asks.

  **Refresh procedure:** scan each family for `# N. Title` (line 1) and
  `- Status:` / `- Date:` / `- Tags:` (header block) → rewrite the three tables
  in `docs/overview.md`. Nothing else is needed.

## Layout

```
AGENTS.md               repo root — points here; carries agent guidance
docs/guide.md           narrative introduction (read this first)
docs/working-method.md  this file — the terse reference
docs/overview.md        derived status index (regenerated dated snapshot)
docs/travel-diary.md    optional human-facing logbook (companion, not a source of truth)
docs/intermediate-artifacts/  optional scratch persistence layer for execution (not a source of truth)
docs/ideas/             idea artifacts
docs/decisions/         proposal + decision artifacts (ADRs)
docs/plans/             plan + execution artifacts
```

Decision records use `docs/decisions/` — the conventional location for ADRs — so
the structure reads as a normal, well-organized repo, with no project-specific
folders imposed.

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
plans).

## Tags (optional)

Any idea, decision, or plan may carry an optional `Tags:` header line — a
comma-separated list of theme words that re-slice the artifacts along a
shared-theme axis, so cross-cutting threads become findable without reading every
artifact in order. Tags surface as a `Tags` column in the derived `docs/overview.md`.

Governance is deliberately light: the vocabulary is **recommended, not enforced**,
and **curated per repo**. Off-list tags are always allowed and nothing rejects
them; over-tagging or vague tags only make a tag less useful — they never break or
spoil the trail. A repo defines its own vocabulary below; the method ships none,
because tags name a *project's* recurring themes (Genericity #7).

**Recommended tags for this repo:** _(none yet — list your project's recurring
themes here, e.g. `auth`, `api`, `docs`)_

## Travel diary (optional companion)

The travel diary is an optional, **human-facing** companion to the machine-facing
`docs/overview.md`. Where the overview is *derived, terse, and state-oriented*, the
diary is *authored, prose, and narrative* — a single growing logbook, newest entry
first, that a colleague can skim after a break to learn *where we are, what changed
last session, what is left, and what is next* without synthesizing across every
artifact.

- **One file, `docs/travel-diary.md`.** Newest entry first. Each entry is headed
  with the date in brackets — `## [YYYY-MM-DD]` — with same-day entries
  disambiguated by a counter: `## [YYYY-MM-DD-(2)]`, `-(3)`, and so on.
- **Each entry** is brief friendly prose covering roughly **where we are**, **what
  we achieved** (since the last entry), **what is left**, and **what is next**,
  optionally closing with a one- or two-sentence **continuation brief** that links
  the relevant plan or ADR.
- **Self-describing.** The file carries its own short agent-instructions header, so
  the mechanism travels with the artifact.
- **Maintained guard-free.** Adding a chapter is a light-weight task — no ADR, no
  plan, and **no confirmation guard** — because the diary touches nothing
  authoritative.
- **Not a source of truth.** The ideas, decisions, and plans remain the only source
  of truth; the diary is prose narration over them, sits outside the lifecycle and
  cross-link vocabulary, and may drift harmlessly. It is optional — a repo that does
  not want one simply has none.

## Intermediate artifacts (optional companion)

Intermediate artifacts are an optional, informal **scratch persistence layer for
the execution stage**. Executing a plan sometimes means *gathering* material first
— pulling data together, extracting or transcribing findings, capturing
intermediate outputs — and working on it later, across steps or sessions. That
working material has no home among the authoritative artifacts (which would pollute
a plan) and dies with the session's context if left unsaved. Intermediate artifacts
give it a cheap, conventional place to live.

- **A folder, `docs/intermediate-artifacts/`.** A scratch space for material
  gathered while executing a plan.
- **Not a source of truth.** The ideas, decisions, and plans remain the only source
  of truth; intermediate artifacts hold disposable working material, sit outside the
  lifecycle and cross-link vocabulary, and may drift or go stale harmlessly because
  nothing authoritative depends on them.
- **Internally unstructured.** The method defines only *where* the folder lives and
  *what it is not*; how its contents are organized is entirely the project's business
  (one subfolder per plan is a fine option, not a rule).
- **Guard-free.** Creating, populating, and removing intermediate artifacts touches
  nothing authoritative, so it needs **no ADR, no plan, and no confirmation guard**.
- **Committed by default.** By default the folder is committed to git, so gathered
  material survives across machines and sessions (Continuity #1). A repo that prefers
  purely-local scratch may gitignore it instead.
- **Optional forward-only pointer.** A plan *may* carry an informal prose note like
  "execution parked material in `docs/intermediate-artifacts/…`" for findability —
  plain prose, **not** a formal cross-link field, with no reciprocal back-link.
- **Left to rot harmlessly.** When a plan is `done`, its intermediate artifacts are
  simply left in place; a repo may prune them, but the method requires no cleanup.
- **Optional.** A repo that does not need intermediate artifacts simply has none.

## How to start working
1. Capture a thought as an idea in `docs/ideas/`.
2. When it matures, open an ADR in `docs/decisions/` with `Status: proposed`.
3. Accept or reject it; an accepted ADR is a decision.
4. Write a `docs/plans/` file that `Implements:` the decision and lists tasks.
5. Execute by moving the plan `active` → `done`, ticking checkboxes.

This repo's own `docs/decisions/0001-adopt-decision-trail.md` records the decision
to adopt decision-trail. Everything else starts from there.

To **(re)adopt or update** decision-trail — including how to **bring an older
adopter fully current** (re-copy the method-owned set from the target's `starter/`),
apply each release's `Adopter migration:` steps, and run the **conformance check** —
see `adopting.md` in the standard repo:
https://github.com/ckluth/decision-trail/blob/main/adopting.md. This pointer travels
with every copied version, so your repo always carries a breadcrumb back to the
update on-ramp.
