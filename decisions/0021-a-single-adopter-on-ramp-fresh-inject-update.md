# ADR-0021: A single adopter on-ramp covering fresh, inject, and update

- Date: 2026-07-03
- Status: accepted
- Promoted from: [Idea-0004](../ideas/0004-using-decision-trail-in-your-own-repo-should-be-easy.md)
- Amended by: [ADR-0022](0022-every-release-ships-reliable-update-instructions.md)

## Context

Idea 0004 asks that using decision-trail in your own repo be **as easy as can
be** — from first adoption through every later upgrade — resting on two
preconditions (a git repo; an agentic setup that understands `AGENTS.md`) and
spanning three scenarios: **fresh** repo, **inject** into an existing repo, and
**update** `X.Y → X.Y+n`.

Pieces of the answer already exist but are scattered and incomplete:

- **ADR-0008** decided adoption happens by **copying the `starter/` skeleton**,
  and that this repo is the versioned standard.
- **ADR-0010** gave the exact **"How we work" pointer block** and made the method
  body live in `docs/working-method.md`, explicitly designed so a fresh adopter's
  `AGENTS.md` *is* the block and an existing-`AGENTS.md` adopter *appends* it.
- **ADR-0014** split the body into `docs/guide.md` (didactic) and
  `docs/working-method.md` (lean spec).

What is still missing, and what idea 0004 surfaces:

1. **No single place tells an adopter how to do any of the three scenarios.** The
   mechanics are implied across ADR-0008/0010/0014 but never written as steps an
   agent can follow.
2. **The update path has teeth and no contract.** 1.2.0 → 1.3.0 was not a no-op
   (it made `Date:` mandatory, added `overview.md`, added `Promoted from:`).
   Nothing tells an adopter what migration a release entails, and no rule forces a
   release author to state it.
3. **Guidance vs tooling is unresolved.** The idea proposes "a mix"; we must
   decide how much is plain do-guidance and whether any tooling is justified
   without violating Economy (#2) and Borrow (#8).

### Considered options

- **A — Leave it implicit.** Adopters infer the steps from the ADRs. Cheapest
  now, but fails idea 0004's whole point: the on-ramp stays an archaeology
  exercise (against Economy #2, Continuity #1).
- **B — One adopter-facing on-ramp document + a release-migration contract, pure
  do-guidance.** A single doc in *this* repo walks an agent through all three
  scenarios as explicit steps, and every release must state its adopter migration
  (even "none"). No bespoke tooling. Leans entirely on borrowed pieces (starter
  copy, the pointer block, the version citation, `CHANGELOG.md`).
- **C — B plus bespoke scaffolding/migration tooling** (a script or
  copier/cookiecutter template that stamps a repo and auto-migrates). Most
  turnkey, but adds a runtime/tooling dependency to a plain-markdown method —
  the exact thing ADR-0008 rejected, and premature before real adoption exists.
- **D — B, plus *optional* helper tooling documented as a non-method give-away.**
  The method stays pure do-guidance and defines no tool. On top of that, the
  on-ramp doc *describes* what a helpful tool could do, and the standard repo
  *may* offer a convenience script (or template) clearly marked **not part of the
  method** — a give-away an adopter can take, ignore, or replace. Nothing in the
  method depends on it, so it adds no dependency and can rot or be dropped without
  touching the contract.

### Decision drivers

Idea 0004's own promises point at **D**: a single, discoverable on-ramp gives
Economy (#2) and Continuity (#1); pure do-guidance driven by the existing agentic
precondition keeps Borrow (#8) intact and adds no dependency; the version citation
already in every adopting repo is a ready-made anchor for "which steps apply."
Option D adds the pragmatic upside of C — a convenience script an adopter *can*
reach for — without C's cost, because the give-away sits **outside** the method
and nothing depends on it. Making the tool a non-method member (rather than
omitting it, B, or absorbing it, C) is what keeps the contract plain-markdown
while still handing adopters something runnable.

## Decision

Adopting and upgrading decision-trail is delivered as **one adopter-facing on-ramp
document plus a release-migration contract, as pure do-guidance** — with any
tooling offered only as an **optional, non-method give-away**.

- **One on-ramp doc in this repo.** A single top-level file (proposed name:
  `adopting.md`) covers all three scenarios as explicit, agent-followable steps.
  It is *adopter-facing guidance about the standard*, so it lives here (the
  standard), not in the copied `starter/`.

- **Fresh repo.** Copy the contents of `starter/` into the new repo. The repo now
  owns its artifacts and its ADR log from `0001-adopt-decision-trail.md` (per
  ADR-0008). `AGENTS.md` *is* the "How we work" pointer block (per ADR-0010).

- **Inject into an existing repo.** Non-destructive drop-in:
  1. Copy `starter/docs/` into the repo's `docs/` (adds `working-method.md`,
     `guide.md`, and the `docs/decisions/` etc. families) without touching
     existing files.
  2. If the repo has no `AGENTS.md`, create it from the pointer block; if it
     already has one, **append** the pointer block (exact wording from ADR-0010).
  3. Seed `docs/decisions/0001-adopt-decision-trail.md`. The repo's pre-existing
     history and any prior decisions coexist untouched; the decision-trail ADR log
     simply starts fresh at 0001 and never inherits this repo's construction ADRs.

- **Update `X.Y → X.Y+n`.** A clean, file-level operation:
  1. Read the repo's current version from the **"Based on decision-trail vX.Y"**
     citation (the anchor).
  2. Replace `docs/working-method.md` and `docs/guide.md` with the target
     version's copies and bump the citation.
  3. Apply, in order, the **adopter migration** stated by each release between the
     current and target version.

- **Release-migration contract (release-author rule).** Every release **must**
  state its adopter-facing migration in `CHANGELOG.md` under a fixed
  **`Adopter migration:`** heading — **even when it is "none."** Migration notes
  live in the `CHANGELOG` (borrowing an existing artifact) rather than a new
  `MIGRATING.md` or `migrations/` family (Borrow #8, Economy #2). A migration is
  written as steps an agent can execute (e.g. "backfill missing `Date:` fields,
  then regenerate `overview.md`").

- **Tooling is an optional non-method give-away.** The method itself defines no
  tool; all three scenarios are do-guidance the agentic precondition already
  covers. On top of that, the on-ramp doc **describes** what a helper could
  automate (e.g. stamping a fresh repo, or running a release's migration), and the
  standard repo **may** ship a convenience script (or, later, a GitHub template)
  clearly labelled **not part of the method** — a give-away an adopter can take,
  ignore, or replace. Nothing in the contract depends on it, so it adds no
  dependency and may be dropped without a method change.

## Consequences

- Adopters get one discoverable entry point for every scenario; the on-ramp stops
  being implicit archaeology across ADR-0008/0010/0014 (Economy #2,
  Continuity #1).
- The inject path is finally written down as a non-destructive procedure, and the
  coexistence rule (existing history untouched, decision-trail log from 0001) is
  explicit (Genericity #7).
- Upgrading becomes a bounded, mechanical operation anchored on the version
  citation, with a per-release migration the author is *contractually required* to
  provide — closing idea 0004's "nothing tells the adopter what the work is" gap.
- `CHANGELOG.md` gains a mandatory `Adopter migration:` section per release, and
  release discipline in this repo grows by one checklist item.
- Keeping any tool a non-method give-away preserves the plain-markdown,
  dependency-free contract (Borrow #8) while still handing adopters something
  runnable: guidance always works on its own, and the optional script is pure
  upside that can rot or be replaced without touching the method.
- A new top-level `adopting.md` will need writing (a follow-up plan once this is
  accepted).
