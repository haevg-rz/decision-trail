# ADR-0029: Shrink the always-loaded agent instruction weight

- Status: accepted
- Date: 2026-07-11
- Amends: ADR-0014 (refines how its canonical/derived method text is written,
  not reversing it)
- Promoted from: [idea 0021](../ideas/0021-shrink-the-always-loaded-agent-instruction-weight.md)

## Context

Idea 0020 asked how to operate the method economically; decomposed (ADR-0027)
into three axes, this is the "always-loaded weight" axis — the cost an agent
pays *every session, unconditionally*, because `AGENTS.md` is injected as
custom instructions before any task begins.

**Observation.** `AGENTS.md` states its rules ~3×. The same normative content
(ordinal numbering, per-family status, canonical header format, disentangling
procedure, etc.) appears in `## The lifecycle`, again inline in prose, and
again in full in `## Agent operating guidance`. Every session pays for all
copies. A rough audit suggests ~30–40% could go with zero loss of meaning by
stating each rule once and cross-referencing.

This repetition spans two different layers established by ADR-0014:

- Two of the three copies live in the **canonical spec**
  (`starter/docs/working-method.md`), regenerated wholesale (never hand-patched)
  into this repo's `AGENTS.md` via a fixed, enumerated set of deltas (paths,
  construction-ADR cross-references, the provenance citation, entry-point
  framing).
- The third copy lives in **`## Agent operating guidance`**, a block that is
  explicitly **not** derived from `working-method.md` — it is hand-maintained
  directly in `AGENTS.md`, and separately carried in `starter/AGENTS.md`.

Any compaction has to land in the right layer, or the next regeneration of
`AGENTS.md` from `working-method.md` silently undoes a hand-patch.

### Considered options (for *which layer* absorbs the compaction)

- **A — Compact the canonical spec (`working-method.md`).** State each rule
  once there; both derived restatements (the lifecycle section and the inline
  prose) collapse in a single edit, and the fix propagates to `AGENTS.md` on
  next regeneration.
- **B — Push the compaction into the derivation rules themselves** (i.e. make
  regeneration "smart" — collapse repeated rules on the fly while turning
  `working-method.md` into `AGENTS.md`). Rejected: ADR-0011/ADR-0014 already
  commit regeneration to being a dumb, deterministic, mechanical
  delta-application, never an editorial rewrite step. Baking compaction logic
  into that step reintroduces judgment calls into what must stay mechanical.
- **C — Hand-tighten the non-derived `## Agent operating guidance` block**
  (in both `AGENTS.md` and `starter/AGENTS.md`), since it isn't sourced from
  `working-method.md` at all and untouched by regeneration.

### Decision drivers

- **Economy (#2):** ~2k tokens saved on every session by removing redundant
  restatement, with zero behavioral change.
- **Consistency with ADR-0011/ADR-0014:** regeneration must stay mechanical;
  compaction logic does not belong inside the derivation rules.
- **Agent-first audience for the spec register:** `working-method.md` /
  `AGENTS.md`'s method body is loaded by the agent every session; a curious
  human *can* read it, but it is not the register ADR-0014 assigned to serve
  human narrative needs — that is `guide.md`'s job. Optimizing the spec purely
  for compactness and unambiguous precision does not conflict with ADR-0014;
  it fulfills it.
- **No information loss for the human reader:** collapsing repetition in the
  spec must not silently drop a nuance that a human reader relied on finding
  there. `guide.md` is the register meant to carry that narrative weight.

## Decision

Adopt **A + C** (reject B).

1. **Compact the canonical spec, `starter/docs/working-method.md`.** State each
   rule once; let other sections cross-reference rather than restate. Keep the
   spec to principles and the terse, greppable tables (contract, lifecycle,
   layout, cross-link vocabulary, how to start) — long how-to step lists become
   pointers to procedures rather than inline repetition, where that dovetails
   with sibling idea 0022 (procedures as skills) without depending on it.
   Regenerate this repo's `AGENTS.md` from the compacted source per the
   existing derivation rules (delta-application only, unchanged).
2. **Hand-tighten `## Agent operating guidance`** in both `AGENTS.md` and
   `starter/AGENTS.md` — the same de-duplication goal, applied directly since
   this block is not derived.
3. **Audit `guide.md`** as part of the same pass: for every rule whose
   restatement is being collapsed in the spec, confirm the nuance is already
   narrated there in prose for the human reader; add prose where it is
   currently only implied by the spec's repetition.
4. **Optimize the spec register agent-first.** No repetition is retained in
   `working-method.md` / `AGENTS.md` for the sake of human skimmability; that
   need is met by `guide.md`, which the agent never loads.

## Consequences

- `AGENTS.md`'s always-loaded method body shrinks (~21 KB → ~13 KB estimated),
  saving roughly 2k tokens on every session, with no behavioral or mechanism
  change.
- The canonical/derived relationship from ADR-0014 is preserved and reinforced:
  the fix is made once at the canonical source and propagates by regeneration;
  regeneration itself stays mechanical.
- `guide.md` may grow slightly to absorb any nuance no longer redundantly
  stated in the spec — a deliberate, bounded move of content to the register
  meant to carry it, not a net loss.
- Carry-out work (the actual line-by-line compaction of `working-method.md`,
  the `## Agent operating guidance` tightening, the `guide.md` audit, and
  regenerating `AGENTS.md`/`overview.md`) belongs to a follow-up plan that
  `Implements:` this ADR, not to this decision.
