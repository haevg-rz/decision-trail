# Working method — decision-trail (reference)

> This project works **decision-trail** — carrying a thought through its whole life
> (idea → proposal → decision → plan → execution) in plain markdown.
>
> Based on **decision-trail v2.12** — https://github.com/haevg-rz/decision-trail

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
| idea | `docs/ideas/NNNN-*.md` | `seed` → `promoted` / `dropped` / `decomposed` |
| proposal | `docs/decisions/NNNN-*.md` | `proposed` |
| decision | `docs/decisions/NNNN-*.md` (same file) | `accepted` / `rejected` |
| plan | `docs/plans/NNNN-*.md` | `draft` → `active` → `done` / `abandoned` |
| execution | `docs/plans/NNNN-*.md` (same file) | the plan ticking its checkboxes |

- **Ideas** are cheap; a matured idea is *promoted* to a proposal. A fresh idea is
  `seed` (*"not yet promoted"* — legitimately including a deliberately-kept parent
  map still budding children). `decomposed` is an *alternative finalized* state: the
  idea budded into children and its own content moved out — it says nothing about
  the children's fate (told by *their* statuses) and is hand-curated and reversible
  (flip back to `seed` to bud one more child).
- **Decisions** are ADRs — a proposal *becomes* a decision in place when accepted.
  Use the classic template (Status / Context / Decision / Consequences); add
  **Decision Drivers** / **Considered Options** when weighing alternatives.
- **Plans** carry an accepted decision into action: the ADR is the spec, the plan
  is the *how*, execution is the plan in motion. Tasks use portable task-list
  markdown (`- [ ]` / `- [x]`).

**Each family's status vocabulary is its own — never borrow another family's.** New
idea → `seed`, new proposal → `proposed`, new plan → `draft`; decision and execution
are in-place continuations that add no separate entry status. Pick a status only
from the target family's row above: an idea is never `proposed`/`draft`/`accepted`;
a plan is never `proposed`/`seed`/`decomposed`; a proposal/decision is never
`seed`/`draft`/`decomposed` (`decomposed` is idea-only).

Every idea, decision, and plan carries a **mandatory** `Date:` (creation date) in
its header, and may carry an optional `Tags:` line (comma-separated theme words,
omitted when empty — see **Tags**).

**Canonical header rendering:** a `# Title` line, a blank line, then a **bulleted
block** — `- Date:` and `- Status:` first, then any cross-link fields
(`- Promoted to:`, `- Implements:`, `- Amends:`, …) and the optional `- Tags:`,
each on its own `-`-prefixed line. The bullets matter: the refresh procedure greps
them, so a bare (bullet-less) header line is silently missed.

**Title line** is pinned: typed, zero-padded, ordinal echoing the filename slot,
family named — `# Idea 0017: Title`, `# ADR-0017: Title`, `# Plan 0017: Title`. The
filename stays authoritative; the H1 ordinal is a *visible echo*, so the two must
always agree.

Artifact numbers are **ordinal only**: assign the next unused number in that family
(`docs/ideas/`, `docs/decisions/`, `docs/plans/` are independent sequences). Never
derive a number from a related artifact — a plan implementing ADR-0004 is not
`0004`; it takes the next free plan slot. Relationships live in cross-link fields
(`Implements:`, `Promoted to:`, …), never in matching numbers. To pick the slot
**reliably**, enumerate the family and take **`max(number) + 1`** (never the first
gap a glob surfaces), then **verify the filename is unused** before writing. To slot
out of order, use **insert-and-shift**: renumber the intruder into place, shift
every later artifact, rewire reciprocal cross-links and prose references, and
regenerate `docs/overview.md`.

`docs/overview.md` is a derived status index over all three families — a single
dated snapshot of each artifact's name, creation date, and state. It is
**regenerated wholesale from the artifact headers** (never hand-patched) and stamped
"as of <date>". Regenerate it whenever the user explicitly asks.

  **Refresh procedure:** scan each family for its typed title line
  (`# Idea NNNN:`, `# ADR-NNNN:`, or `# Plan NNNN:`) and `- Status:` / `- Date:` /
  `- Tags:` (header block) → rewrite the three tables in `docs/overview.md`. If
  an artifact's header fields carry no leading `-` bullet, or its title-line
  ordinal doesn't match its filename slot, do **not** silently skip or trust it —
  both are non-conformant; fix the header to the canonical bulleted form and
  align the ordinals (see the header template above) before regenerating, so no
  artifact is dropped or misfiled in the index.

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
## Disentangling a large idea

An idea that grows too big — braiding several *orthogonal* axes that only have
weight together as a map — is taken apart by **budding** (#6), not multi-promotion
(promotion is strictly 1:1, one idea ↔ one ADR). The **procedure is fixed** — the
*how* is a lookup, not a debate:

1. The parent idea **stays** and its status becomes `decomposed`.
2. Each axis **buds** into a child idea via `Parent:`.
3. Each child matures and **promotes 1:1** to its own ADR.
4. The **reasons for the branching are documented in the parent idea.**
5. One status per idea — never stack `promoted` and `decomposed`.

What is **not** prescribed is the *strategy* (promote an already-decidable core
first, or bud everything and let the parent stand as a pure map) — a judgment call
decided in conversation. The agent may (and a good one will) **propose** the
disentangling; the **responsible unit is the human.**

## Tags (optional)

An optional `Tags:` header line (comma-separated theme words) re-slices artifacts
along a shared-theme axis, so cross-cutting threads are findable without reading
every artifact in order; tags surface as a `Tags` column in `docs/overview.md`.
Governance is light: the vocabulary is **recommended, not enforced**, and **curated
per repo**. Off-list tags are allowed; over-tagging or vague tags only make a tag
less useful — they never break or spoil the trail. The method ships no vocabulary
(tags name a *project's* recurring themes, Genericity #7); a repo defines its own
below.

**Recommended tags for this repo:** _(none yet — list your project's recurring
themes here, e.g. `auth`, `api`, `docs`)_

## Travel diary (optional companion)

An optional, **human-facing** companion to the machine-facing `docs/overview.md`:
an authored, newest-first prose logbook a colleague can skim after a break to learn
*where we are, what changed, what is left, and what is next* — without synthesizing
across every artifact.

- **One file, `docs/travel-diary.md`**, newest entry first; each entry headed
  `## [YYYY-MM-DD]` (same-day entries disambiguated `-(2)`, `-(3)`, …).
- **Each entry** is brief prose — *where we are / what we achieved / what is left /
  what is next* — optionally closing with a **continuation brief** linking the
  relevant plan or ADR.
- **Self-describing** — carries its own short agent-instructions header, so the
  mechanism travels with the artifact.
- **Guard-free** — adding a chapter needs no ADR, no plan, and **no confirmation
  guard**; it touches nothing authoritative.
- **Not a source of truth** — prose narration over the artifacts, outside the
  lifecycle and cross-link vocabulary; may drift harmlessly. Optional — a repo that
  does not want one simply has none.

## Intermediate artifacts (optional companion)

An optional, informal **scratch persistence layer for the execution stage**.
Executing a plan sometimes means *gathering* material first (data, findings,
intermediate outputs) to work on later, across steps or sessions; that material has
no home among the authoritative artifacts (it would pollute a plan) and dies with
the session if left unsaved. Intermediate artifacts give it a cheap, conventional
place to live.

- **A folder, `docs/intermediate-artifacts/`** — scratch space for material gathered
  while executing a plan.
- **Not a source of truth** — disposable working material, outside the lifecycle and
  cross-link vocabulary; may drift or go stale harmlessly because nothing
  authoritative depends on it.
- **Internally unstructured** — the method defines only *where* it lives and *what it
  is not*; how its contents are organized is the project's business (one subfolder
  per plan is a fine option, not a rule).
- **Guard-free** — creating, populating, and removing files needs **no ADR, no plan,
  and no confirmation guard**.
- **Committed by default**, so material survives across machines and sessions
  (Continuity #1); a repo preferring purely-local scratch may gitignore it instead.
- **Optional forward-only pointer** — a plan *may* carry an informal prose note
  ("execution parked material in `docs/intermediate-artifacts/…`") for findability —
  plain prose, **not** a formal cross-link field, with no reciprocal back-link.
- **Left to rot harmlessly** when a plan is `done` (pruning is optional). The whole
  mechanism is optional — a repo that does not need it simply has none.

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
https://github.com/haevg-rz/decision-trail/blob/main/adopting.md. This pointer travels
with every copied version, so your repo always carries a breadcrumb back to the
update on-ramp.
