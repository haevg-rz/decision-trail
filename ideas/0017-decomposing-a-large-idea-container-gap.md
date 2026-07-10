# Idea: a large idea has no home to decompose into — is a "container" idea missing?

- Date: 2026-07-10
- Status: promoted
- Promoted to: [ADR-0027](../decisions/0027-a-decomposed-status-for-a-budded-parent-idea.md)

## Observation

While working in an adopter repo, a genuinely large idea appeared: it braided
roughly five *orthogonal* axes (substance, canonical form, per-layer placement,
cross-vendor projection, enforcement) that only have weight **together**, as a
map — none was yet ripe enough to carry its own file. The natural decomposition
felt clear: promote one narrow **decidable core** to an ADR now, and keep the
rest for later.

Trying to make that method-conformant surfaced a friction. **Promotion is
strictly one-to-one:** the cross-link rules state a promotion link is reciprocal
precisely because *"both ends are single and write-once (promotion: one idea ↔
one ADR)."* So a single big idea **cannot** fan out into several ADRs. The
method's tool for "the rest" is instead **budding** (contract promise #6): the
large idea is a *parent* that spawns child ideas via `Parent:`, and each child
matures and promotes 1:1 to its own ADR.

That works mechanically — but it exposes a gap. The idea status vocabulary is
only `seed → promoted / dropped`. There is **no first-class notion of a
long-lived "container" / "map" / "epic" idea** — a parent whose *job* is to hold
a set of axes and bud children, and which may intentionally never promote itself.
Such a parent has nowhere honest to sit:

- it lingers at `seed` indefinitely, even though it is not an unexamined seed but
  a deliberately-kept index;
- or it becomes `dropped` once hollowed out by budding, even though nothing was
  rejected — its content simply *moved* into children;
- or it is force-fit into `promoted` by pointing at the one narrow core ADR,
  which misdescribes the parent (only one slice matured, not the whole map).

There is also no stated **guidance for the decomposition itself**: when you hold
a big idea, should you (a) promote it to one narrow ADR and bud the remaining
axes off it, or (b) keep it as a pure never-promoted parent map and bud
*everything*, including the core, into children? The method is silent, so two
reasonable agents will decompose the same large idea differently.

## Desired clarification

- **A stated pattern for decomposing a large idea** into method-conformant
  pieces: parent (map) idea + budded child ideas, each child promoting 1:1 to its
  own ADR, with the narrow "decidable core" going first. Make explicit that
  budding — not multi-promotion — is the intended answer, since promotion is 1:1.
- **A decision on the "container" idea's lifecycle honesty:** whether a
  deliberately long-lived parent map deserves any first-class recognition (a
  status annotation, a naming/`Parent:` convention, or simply explicit permission
  for a `seed` to remain a never-promoted parent whose role is to hold axes and
  bud children), and what its **end-state** is once decomposed (`dropped` as
  "fully budded", or left at `seed` as a standing index).
- Ideally all of this as *guidance only* — prose in the working method — rather
  than new machinery, respecting "borrow, don't invent" (#8).

## Open questions

- Does this warrant a new status word (e.g. `epic` / `map`) or a new artifact
  concept? Likely **no** — that risks violating economy (#2) and borrow-don't-
  invent (#8). Can it be solved purely as decomposition *guidance* plus a note
  that a parent idea may legitimately remain unpromoted?
- Can one idea be **both** `promoted` (to the narrow core ADR) **and** a parent
  of budded children at once? Budding is `Parent:`-forward-only and independent
  of promotion, so mechanically yes — but is it clean, or does it conflate two
  roles?
- How does a "container/parent-map" idea relate to the **Tags spine** (idea 0009
  / ADR-0017)? Is a map idea just a locally-scoped spine, or genuinely a distinct
  thing (an authored parent that *owns* children vs. a derived cross-cut)?
- Is "the decidable core goes first" a real method rule, or adopter-specific
  strategy that does not belong in the generic method?
- Should any of this reach adopters via the copy-driven method body, or is it
  agent-guidance only?
