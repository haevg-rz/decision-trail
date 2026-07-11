# ADR-0032: Audience-forked sections are a declared delta class in the sync model

- Date: 2026-07-11
- Status: accepted
- Promoted from: [Idea 0026](../ideas/0026-guide-sync-model-cant-hold-audience-deltas.md)
- Amends: [ADR-0014](0014-sync-method-renderings-and-separate-audiences.md)

## Context

[ADR-0014](0014-sync-method-renderings-and-separate-audiences.md) established that
the method's documents exist as **two renderings of one logical source**: a
canonical copy under `starter/docs/` and a derived copy in this repo, regenerated
wholesale and never hand-patched, differing only by a **closed, enumerated list of
deltas**. For the spec (`working-method.md` → `AGENTS.md`) that list is four items:
paths, construction-ADR cross-references, the provenance citation, and entry-point
framing. The [`guide.md`](../guide.md) sync note inherited the same shape but a
narrower claim: *"The only delta is paths."*

[Idea 0026](../ideas/0026-guide-sync-model-cant-hold-audience-deltas.md) found that
claim is no longer true. Surfaced while dogfooding the `updating.agent.md` path
(idea 0025 / ADR-0031 / plan 0021), two guide sections now diverge by **audience**,
not by path:

- **"How to start"** — the home guide opens with an adoption lead-in (*clone the
  standard repo, follow `adopting.md`*) before the lifecycle steps; the adopter
  guide skips that and closes with *"Your repo's
  `docs/decisions/0001-adopt-decision-trail.md` already records the decision to
  adopt"* (added in the 2.13 documentation patch).
- **"Where to go next"** — the two carry different further-reading lists (home
  points at its own `decisions/` construction log; the adopter points at
  `working-method.md` + `AGENTS.md` + the external `adopting.md` URL).

These deltas are **correct per audience** and must not be exchanged or flattened:
an adopter already has the method, so adoption instructions would misfire; and the
home repo has no `0001-adopt-decision-trail.md` (its `0001` is *"Record decisions as
ADRs"*). The content is right. The defect is that the **sync contract cannot
describe it**, which produces two concrete failures:

1. **The sync note lies** — it advertises a paths-only delta while real content
   deltas exist, so a reader or agent trusting it is misled (Transparency #3).
2. **An honest regeneration would clobber the home-only content** — "regenerate
   wholesale from `starter` with only path deltas" would silently delete the home
   guide's adoption lead-in and its construction-log further-reading. The 2.13
   patch is a latent casualty of the next faithful regen.

This is a question about ADR-0014's contract, not a wording typo, so it is decided
in the open rather than hand-patched into the note.

### Decision drivers

- **Transparency (#3):** a sync note must state the truth about how the renderings
  differ; a false "paths only" claim is the primary defect.
- **Economy (#2):** keep the single-source, regenerate-the-derived-view discipline
  (ADR-0011/0014) — do not fall back to two independently hand-maintained guides.
- **Regeneration must stay a lookup, not a judgment call:** whatever we decide, an
  agent regenerating the guide needs a mechanical rule, not open-ended discretion
  about what to preserve.
- **Right content per audience:** the adopter guide must not tell an adopter to
  re-adopt; the home guide must not cite an ADR it does not have. Convergence to
  one wording cannot satisfy both.

### Considered options

- **A — Converge the sections to one audience-neutral wording.** Rewrite "How to
  start" and "Where to go next" so a single text serves both, restoring the
  literal paths-only delta. *Rejected:* the deltas are semantic, not cosmetic — a
  neutral wording either tells adopters to re-adopt or drops the home
  construction-log pointer. It destroys correct content to save the contract.
- **B — Declare the two guides genuinely audience-forked and drop the derived
  model for the guide** (independent, hand-maintained files). *Rejected:*
  reintroduces exactly the drift ADR-0014 was written to kill; the guides share far
  more than they differ, so losing single-source is a bad trade (Economy #2).
- **C — Widen the enumerated delta list to admit a named, closed set of
  audience-forked sections, regenerated per audience from an enumerated override,
  and rewrite the sync notes to tell the truth.** Keeps the derived model and
  single-source; makes the real deltas explicit and mechanical. *Chosen.*

## Decision

Adopt **C**. Extend ADR-0014's enumerated-delta contract with a new, declared
**delta class** and apply it to the guide.

1. **Add "audience-forked section" as a legitimate delta class.** Alongside paths,
   construction-ADR references, provenance citation, and entry-point framing, a
   rendering may differ from the canonical text at a **named, closed set of
   sections whose content is audience-specific** (home repo vs adopter). This is an
   *enumerated* class, not open license: only the listed sections may fork, and the
   list lives in the sync note.

2. **Enumerate the guide's forked sections now:** **"How to start"** and **"Where
   to go next"**. Every other section stays 1:1-derived (path-substituted only).

3. **Rewrite both guides' sync notes to tell the truth.** Replace *"the only delta
   is paths"* with the real contract: *paths everywhere, plus these named sections
   which are regenerated per audience from their canonical override.* The note
   names the forked sections explicitly so the boundary is visible on sight.

4. **State the crisp regeneration rule — borrow the `AGENTS.md` derived-span
   pattern.** `AGENTS.md` already names an explicitly-derived span and declares the
   rest untouchable; apply the same move to the guide. Regenerating the derived
   guide:
   - **1:1-derived sections** — copy from canonical, apply the path delta, nothing
     else;
   - **audience-forked sections** — do **not** copy the canonical text over the
     local one; regenerate them from the **canonical's per-audience variant**,
     preserving the audience-correct content. The canonical guide carries both
     variants (or an explicit marker of what each audience gets) so this stays a
     lookup, not an authoring decision.

5. **Run a consistency audit across the other rendered pair.** Confirm the spec
   renderings (`working-method.md` → `AGENTS.md`) carry no *undeclared* audience
   deltas of the same kind; any found are brought under this same enumerated-delta
   discipline rather than left implicit.

6. **This `Amends:` ADR-0014** — it extends that ADR's closed delta list with a new
   class; it does **not** overturn the derived-rendering model, the single-source
   direction (canonical = the `starter/` copy), or the never-hand-patch rule.

The **carry-out work** — editing both guides' sync notes, marking the forked
sections and their canonical per-audience variants, and running the audit — belongs
to a follow-up **plan** that `Implements:` this ADR, not to this decision.

## Consequences

- The guide sync note states the truth: a reader or agent sees exactly how the two
  guides may differ, and the primary Transparency (#3) defect is closed.
- A faithful wholesale regeneration no longer clobbers the home guide's adoption
  lead-in or its construction-log further-reading; the 2.13 patch is safe because
  its sections are declared forked, not accidental.
- Single-source and regenerate-don't-patch survive (Economy #2, ADR-0011/0014); the
  guides do not decay into two hand-maintained files.
- Regeneration stays mechanical: an agent looks up which sections are 1:1-derived
  and which are audience-forked, and transforms each accordingly — no open-ended
  judgment about what to preserve.
- Cost: the canonical guide must now carry (or clearly mark) the per-audience
  variants of the forked sections, and the delta contract grows by one class — a
  small, bounded increase in the sync surface, paid once.
- The new delta class is generic: it is available to any future rendered pair that
  develops a legitimate audience fork, not a one-off patch for the guide.
- Open for acceptance: confirm the forked-section list is **exactly** {"How to
  start", "Where to go next"} and that no third guide section is silently forked;
  the step-5 audit may surface spec-side deltas that widen the scope of the
  follow-up plan.
