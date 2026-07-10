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
  is the *how*, execution is the plan in motion. Tasks use portable task-list
  markdown (`- [ ]` / `- [x]`).

**Each family's status vocabulary is its own — never borrow another family's
status.** A newly created idea starts at `seed`, a new proposal at `proposed`, and
a new plan at `draft`; decision and execution are in-place continuations (of a
proposal and a plan) and add no separate entry status. Name the artifact family
first, then pick a status from *that* family's row above only — an idea is never
`proposed`, `draft`, or `accepted`; a plan is never `proposed` or `seed`; a
proposal/decision is never `seed` or `draft`. (ADR-0024)

Every idea, decision, and plan carries a `Date:` (creation date) in its header —
**mandatory**. It may also carry an optional `Tags:` line — comma-separated theme
words, omitted when empty (see **Tags** below). `overview.md` is a derived status
index over all three families: a
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
travel-diary.md optional human-facing logbook (companion, not a source of truth)
intermediate-artifacts/ optional scratch persistence layer for execution (not a source of truth)
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

## Tags (optional)

Any idea, decision, or plan may carry an optional `Tags:` header line — a
comma-separated list of theme words that re-slice the artifacts along a
shared-theme axis, so cross-cutting threads become findable without reading every
artifact in order. Tags surface as a `Tags` column in the derived `overview.md`.

Governance is deliberately light: the vocabulary is **recommended, not enforced**,
and **curated per repo**. Off-list tags are always allowed and nothing rejects
them; over-tagging or vague tags only make a tag less useful — they never break or
spoil the trail. A repo defines its own vocabulary below; the method ships none,
because tags name a *project's* recurring themes (Genericity #7). See ADR-0017.

**Recommended tags for this repo:** _(none yet — decision-trail's home repo needs
no tags of its own; adopting repos list their recurring themes here.)_

## Travel diary (optional companion)

The travel diary is an optional, **human-facing** companion to the machine-facing
`overview.md`. Where the overview is *derived, terse, and state-oriented*, the
diary is *authored, prose, and narrative* — a single growing logbook, newest entry
first, that a colleague can skim after a break to learn *where we are, what changed
last session, what is left, and what is next* without synthesizing across every
artifact.

- **One file, `travel-diary.md`.** Newest entry first. Each entry is headed with
  the date in brackets — `## [YYYY-MM-DD]` — with same-day entries disambiguated by
  a counter: `## [YYYY-MM-DD-(2)]`, `-(3)`, and so on.
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
  cross-link vocabulary, and may drift harmlessly. It is optional. See ADR-0018.

## Intermediate artifacts (optional companion)

Intermediate artifacts are an optional, informal **scratch persistence layer for
the execution stage**. Executing a plan sometimes means *gathering* material first
— pulling data together, extracting or transcribing findings, capturing
intermediate outputs — and working on it later, across steps or sessions. That
working material has no home among the authoritative artifacts (which would pollute
a plan) and dies with the session's context if left unsaved. Intermediate artifacts
give it a cheap, conventional place to live (ADR-0020).

- **A folder, `intermediate-artifacts/`.** A scratch space for material gathered
  while executing a plan.
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
  "execution parked material in `intermediate-artifacts/…`" for findability — plain
  prose, **not** a formal cross-link field, with no reciprocal back-link.
- **Left to rot harmlessly.** When a plan is `done`, its intermediate artifacts are
  simply left in place; a repo may prune them, but the method requires no cleanup.
- **Optional.** A repo that does not need intermediate artifacts simply has none.

## How to start working
1. Capture a thought as an idea in `ideas/`.
2. When it matures, open an ADR in `decisions/` with `Status: proposed`.
3. Accept or reject it; an accepted ADR is a decision.
4. Write a `plans/` file that `Implements:` the decision and lists tasks.
5. Execute by moving the plan `active` → `done`, ticking checkboxes.

## Agent operating guidance

These rules are for an AI agent working in this repo:

- **`AGENTS.md` has a derived method body.** When `starter/docs/working-method.md`
  changes, regenerate only the section from `## The contract` through `## How to
  start working` — applying the enumerated deltas (repo-root paths instead of
  `docs/`-prefixed ones, construction-ADR cross-references added, no provenance
  citation, entry-point framing adjusted). The preamble above that section and
  this `## Agent operating guidance` section below it are **not derived and must
  not be touched**.
- **Artifact numbers are ordinal only.** When creating an artifact, assign the
  next unused number in that family (`ideas/`, `decisions/`, `plans/` are
  independent sequences). Never derive a number from a related artifact — a plan
  that implements ADR-0004 is not named `0004`; it gets the next free plan slot.
  Relationships are expressed via cross-link fields (`Implements:`, `Promoted
  to:`, etc.), never via matching numbers. (ADR-0015)
- **Status values are per-family — never mix them.** A new idea starts `seed`, a
  new proposal `proposed`, a new plan `draft`. Pick a status only from the target
  artifact's own family: an idea is never `proposed`/`draft`/`accepted`; a plan is
  never `proposed`/`seed`; a proposal/decision is never `seed`/`draft`. (ADR-0024)
- **The method is settled.** Use it; don't redesign decision-trail casually. Any
  change to the method itself is made decision-trail — proposed and recorded as a
  new ADR, with amended or superseded ADRs cross-linked (never edited away).
- **Confirmation guard.** Never rush into writing, editing, or implementing. First
  briefly explain what you intend to do, then wait for explicit approval.
  Discussing and proposing is always fine — acting requires a green light. Before
  acting, name your intended scope explicitly — especially when a bare "yes"/"ok"
  could be read as approving a larger batch rather than just the single next step.
- **Keep `overview.md` current.** It is a derived snapshot, regenerated wholesale
  from the artifact headers (never hand-patched) and stamped "as of <date>"
  (ADR-0011). Regenerate it whenever the user explicitly asks. A user may flip a
  state directly in an artifact; the next regeneration reconciles the index.

  **Refresh procedure:** scan each family for `# N. Title` (line 1) and
  `- Status:` / `- Date:` / `- Tags:` (header block) → rewrite the three tables
  in `overview.md`. Nothing else is needed.
- **Travel diary — guard-free.** `travel-diary.md` is an optional, informal
  human-facing logbook, outside the lifecycle and **not a source of truth**
  (ADR-0018). When the user says *"add a chapter to the travel diary"* (or
  similar), prepend a new dated `## [YYYY-MM-DD]` section (same-day entries
  disambiguated `-(2)`, `-(3)`, …) covering where we are / what we achieved / what
  is left / what is next, with an optional continuation brief. This is a
  light-weight task — **no ADR, no plan, and no confirmation guard**. Full
  instructions live in the diary's own header.
- **Intermediate artifacts — guard-free.** `intermediate-artifacts/` is an
  optional, informal scratch persistence layer for material gathered during plan
  execution, outside the lifecycle and **not a source of truth** (ADR-0020).
  Creating, populating, and deleting files there is a light-weight task — **no ADR,
  no plan, and no confirmation guard** — because it touches nothing authoritative.
  Its internal organization is the project's business; it is committed by default
  (a repo may gitignore it) and left to rot harmlessly once a plan is done.
- **Release-migration contract (release-author rule, ADR-0021, refined by
  ADR-0022).** When cutting a new release of decision-trail, every `CHANGELOG.md`
  entry **must** carry an **`Adopter migration:`** line — **even when it is
  "none"** — written as agent-executable steps. Its scope is **required behavioral
  changes only** (e.g. "backfill missing `Date:` headers, then regenerate
  `overview.md`"); **new optional scaffolds are not enumerated here** — they reach
  adopters automatically via the copy-driven update. Adopters follow these, in
  version order, via the update path in [`adopting.md`](adopting.md), the
  adopter-facing on-ramp. No adoption *tool* ships: adopting/updating is plain
  do-guidance the agent executes directly.
- **Copy-driven "bring me current" + conformance check (ADR-0022).** Updating an
  adopter to a target version means **re-copying the method-owned set** (exactly
  `starter/`'s contents) into the adopter's `docs/`, overwriting method text and
  scaffolds while **preserving project content** (the artifact families, a
  populated `travel-diary.md`, `intermediate-artifacts/`, `overview.md`) — so
  additive scaffolds arrive without per-release bookkeeping. After an update (or on
  request), run the **conformance check** (do-guidance, no tool): mandatory `Date:`
  headers present, `overview.md` in sync with headers, and the `Based on
  decision-trail vX.Y` citation consistent across `docs/working-method.md` and the
  `AGENTS.md` "How we work" block. Full steps live in [`adopting.md`](adopting.md).
