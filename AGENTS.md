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
| idea | `ideas/NNNN-*.md` | `seed` → `promoted` / `dropped` / `decomposed` |
| proposal | `decisions/NNNN-*.md` | `proposed` |
| decision | `decisions/NNNN-*.md` (same file) | `accepted` / `rejected` |
| plan | `plans/NNNN-*.md` | `draft` → `active` → `done` / `abandoned` |
| execution | `plans/NNNN-*.md` (same file) | the plan ticking its checkboxes |

- **Ideas** are cheap; a matured idea is *promoted* to a proposal. A fresh idea is
  `seed` (*"not yet promoted"* — legitimately including a deliberately-kept parent
  map still budding children). `decomposed` is an *alternative finalized* state: the
  idea budded into children and its own content moved out — it says nothing about
  the children's fate (told by *their* statuses) and is hand-curated and reversible
  (flip back to `seed` to bud one more child). (ADR-0027)
- **Decisions** are [ADRs](decisions/) — a proposal *becomes* a decision in place
  when accepted. Use the classic template (Status / Context / Decision /
  Consequences); add **Decision Drivers** / **Considered Options** when weighing
  alternatives.
- **Plans** carry an accepted decision into action: the ADR is the spec, the plan
  is the *how*, execution is the plan in motion. Tasks use portable task-list
  markdown (`- [ ]` / `- [x]`).

**Each family's status vocabulary is its own — never borrow another family's.** New
idea → `seed`, new proposal → `proposed`, new plan → `draft`; decision and execution
are in-place continuations that add no separate entry status. Pick a status only
from the target family's row above: an idea is never `proposed`/`draft`/`accepted`;
a plan is never `proposed`/`seed`/`decomposed`; a proposal/decision is never
`seed`/`draft`/`decomposed` (`decomposed` is idea-only). (ADR-0024, ADR-0027)

Every idea, decision, and plan carries a **mandatory** `Date:` (creation date) in
its header, and may carry an optional `Tags:` line (comma-separated theme words,
omitted when empty — see **Tags**).

**Canonical header rendering:** a `# Title` line, a blank line, then a **bulleted
block** — `- Date:` and `- Status:` first, then any cross-link fields
(`- Promoted to:`, `- Implements:`, `- Amends:`, …) and the optional `- Tags:`,
each on its own `-`-prefixed line. The bullets matter: the refresh procedure greps
them, so a bare (bullet-less) header line is silently missed. (ADR-0026)

**Title line** is pinned: typed, zero-padded, ordinal echoing the filename slot,
family named — `# Idea 0017: Title`, `# ADR-0017: Title`, `# Plan 0017: Title`. The
filename stays authoritative; the H1 ordinal is a *visible echo*, so the two must
always agree. (ADR-0028)

Artifact numbers are **ordinal only**: assign the next unused number in that family
(`ideas/`, `decisions/`, `plans/` are independent sequences). Never derive a number
from a related artifact — a plan implementing ADR-0004 is not `0004`; it takes the
next free plan slot. Relationships live in cross-link fields (`Implements:`,
`Promoted to:`, …), never in matching numbers. To pick the slot **reliably**,
enumerate the family and take **`max(number) + 1`** (never the first gap a glob
surfaces), then **verify the filename is unused** before writing. To slot out of
order, use **insert-and-shift**: renumber the intruder into place, shift every later
artifact, rewire reciprocal cross-links and prose references, and regenerate
`overview.md`. (ADR-0015, ADR-0025)

`overview.md` is a derived status index over all three families — a single dated
snapshot of each artifact's name, creation date, and state. It is **regenerated
wholesale from the artifact headers** (never hand-patched) and stamped "as of
<date>" (ADR-0011). Regenerate it whenever the user explicitly asks (ADR-0016).

**Refresh procedure:** scan each family for its typed title line (`# Idea NNNN:`,
`# ADR-NNNN:`, or `# Plan NNNN:`) and `- Status:` / `- Date:` / `- Tags:` (header
block) → rewrite the three tables in `overview.md`. If an artifact's header fields
carry no leading `-` bullet, or its title-line ordinal doesn't match its filename
slot, do **not** silently skip or trust it — both are non-conformant; fix the header
to the canonical bulleted form and align the ordinals before regenerating, so no
artifact is dropped or misfiled in the index.

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
disentangling; the **responsible unit is the human.** See ADR-0027.

## Tags (optional)

An optional `Tags:` header line (comma-separated theme words) re-slices artifacts
along a shared-theme axis, so cross-cutting threads are findable without reading
every artifact in order; tags surface as a `Tags` column in `overview.md`.
Governance is light: the vocabulary is **recommended, not enforced**, and **curated
per repo**. Off-list tags are allowed; over-tagging or vague tags only make a tag
less useful — they never break or spoil the trail. The method ships no vocabulary
(tags name a *project's* recurring themes, Genericity #7); a repo defines its own
below. See ADR-0017.

**Recommended tags for this repo:** _(none yet — decision-trail's home repo needs
no tags of its own; adopting repos list their recurring themes here.)_

## Travel diary (optional companion)

An optional, **human-facing** companion to the machine-facing `overview.md`: an
authored, newest-first prose logbook a colleague can skim after a break to learn
*where we are, what changed, what is left, and what is next* — without synthesizing
across every artifact.

- **One file, `travel-diary.md`**, newest entry first; each entry headed
  `## [YYYY-MM-DD]` (same-day entries disambiguated `-(2)`, `-(3)`, …).
- **Each entry** is brief prose — *where we are / what we achieved / what is left /
  what is next* — optionally closing with a **continuation brief** linking the
  relevant plan or ADR.
- **Self-describing** — carries its own short agent-instructions header, so the
  mechanism travels with the artifact.
- **Guard-free** — adding a chapter needs no ADR, no plan, and **no confirmation
  guard**; it touches nothing authoritative.
- **Not a source of truth** — prose narration over the artifacts, outside the
  lifecycle and cross-link vocabulary; may drift harmlessly. Optional. See ADR-0018.

## Intermediate artifacts (optional companion)

An optional, informal **scratch persistence layer for the execution stage**
(ADR-0020). Executing a plan sometimes means *gathering* material first (data,
findings, intermediate outputs) to work on later, across steps or sessions; that
material has no home among the authoritative artifacts (it would pollute a plan) and
dies with the session if left unsaved. Intermediate artifacts give it a cheap,
conventional place to live.

- **A folder, `intermediate-artifacts/`** — scratch space for material gathered
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
  ("execution parked material in `intermediate-artifacts/…`") for findability —
  plain prose, **not** a formal cross-link field, with no reciprocal back-link.
- **Left to rot harmlessly** when a plan is `done` (pruning is optional). The whole
  mechanism is optional — a repo that does not need it simply has none.

## How to start working
1. Capture a thought as an idea in `ideas/`.
2. When it matures, open an ADR in `decisions/` with `Status: proposed`.
3. Accept or reject it; an accepted ADR is a decision.
4. Write a `plans/` file that `Implements:` the decision and lists tasks.
5. Execute by moving the plan `active` → `done`, ticking checkboxes.

## Agent operating guidance

These rules are for an AI agent working in this repo. Beyond the derived-body
rule, they **complement, not restate** the spec above (`## The contract` …
`## How to start working`): where a mechanic is fully specified there, this list
only flags the trap to avoid and points to it.

- **`AGENTS.md` has a derived method body.** When `starter/docs/working-method.md`
  changes, regenerate only the section from `## The contract` through `## How to
  start working` — applying the enumerated deltas (repo-root paths instead of
  `docs/`-prefixed ones, construction-ADR cross-references added, no provenance
  citation, entry-point framing adjusted). The preamble above that section and
  this `## Agent operating guidance` section below it are **not derived and must
  not be touched**.
- **Follow the spec's mechanics above** (`## The contract` … `## How to start
  working`) exactly — they are lookups, not judgment calls:
  - **Ordinal numbering** — next free slot per family via `max(number)+1`, verify
    the filename is unused; never reuse a related artifact's number; renumber
    out-of-order inserts with insert-and-shift (§ *The lifecycle*; ADR-0015,
    ADR-0025).
  - **Per-family status** — a new idea is `seed`, a proposal `proposed`, a plan
    `draft`; never borrow another family's status (§ *The lifecycle*; ADR-0024).
  - **Canonical header + title line** — a bulleted header block, and a typed,
    zero-padded H1 ordinal matching the filename slot; a bare (bullet-less) header
    is silently missed by the refresh, and a title/filename ordinal mismatch is a
    conformance failure (§ *The lifecycle*; ADR-0026, ADR-0028).
  - **Disentangling a large idea** — bud into children, mark the parent
    `decomposed`, document the reasons in the parent; never multi-promote, never
    stack `promoted` and `decomposed`. **Propose** the split; the human decides
    (§ *Disentangling a large idea*; ADR-0027).
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
  (ADR-0011) — the refresh procedure is specified in the spec above
  (§ *The lifecycle*). Regenerate it whenever the user explicitly asks (ADR-0016).
  A user may flip a state directly in an artifact; the next regeneration reconciles
  the index.
- **Travel diary — guard-free.** When the user says *"add a chapter to the travel
  diary"* (or similar), prepend a new dated `## [YYYY-MM-DD]` section to
  `travel-diary.md` (same-day entries disambiguated `-(2)`, `-(3)`, …) — where we
  are / what we achieved / what is left / what is next, with an optional
  continuation brief. Light-weight: **no ADR, no plan, no confirmation guard**
  (§ *Travel diary*; ADR-0018).
- **Intermediate artifacts — guard-free.** Creating, populating, and deleting
  files under `intermediate-artifacts/` is light-weight — **no ADR, no plan, no
  confirmation guard** — because it touches nothing authoritative
  (§ *Intermediate artifacts*; ADR-0020).
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
- **Copy-driven "bring me current" + conformance check (ADR-0022; audience split
  ADR-0031).** Updating an adopter to a target version means **re-copying the
  method-owned set** (exactly `starter/`'s contents) into the adopter's `docs/`,
  overwriting method text and scaffolds while **preserving project content** (the
  artifact families, a populated `travel-diary.md`, `intermediate-artifacts/`,
  `overview.md`) — so additive scaffolds arrive without per-release bookkeeping.
  After an update (or on request), run the **conformance check** (do-guidance, no
  tool): mandatory `Date:` headers present, `overview.md` in sync with headers, and
  the `Based on decision-trail vX.Y` citation consistent across
  `docs/working-method.md` and the `AGENTS.md` "How we work" block. Per ADR-0031 the
  two audiences are separated: the **human** trigger is one intent naming the source
  **and** the how-to file — *"update the method from `<source>`; the how-to is
  `<source>/updating.agent.md`"* — and the **agent** executes the full procedure
  (the executable, self-contained steps live in
  [`updating.agent.md`](updating.agent.md), the single operational source of truth,
  run as one transparent batch under the confirmation guard). `adopting.md` carries
  only the human intent + pointer; never duplicate the steps back into it.
