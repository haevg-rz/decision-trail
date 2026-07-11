# ADR-0030: Resume economy as a human-facing discipline in the guide

- Status: accepted
- Date: 2026-07-11
- Promoted from: [idea 0023](../ideas/0023-name-the-resume-time-economy-practices-as-a-discipline.md)

## Context

Idea 0020 asked how to operate the method economically; decomposed (ADR-0027)
into three axes, this is the **resume-time economy** axis — the cost an operator
pays *only when it reads the trail*, and can already avoid, because the artifacts
are deliberately structured for cheap resume.

**Observation.** Economy (promise #2) is a promise the method makes about
*itself* — cheap to write, cheap to resume — but it offers no guidance on how to
*operate* it cheaply. The mechanics that make cheap resume possible already exist
(greppable fixed field names, the derived `overview.md`, the travel diary); what
is missing is advice that names the discipline for the person driving the work.

**Two registers, two audiences (per ADR-0014).** The always-loaded spec register
(`working-method.md` / `AGENTS.md`) serves the agent every session; the
human-narrative register (`guide.md`) is read on demand and never loaded by the
agent. Sibling ADR-0029 exists specifically to *shrink* the always-loaded weight.
Any resume-economy advice therefore must not land in the spec register: advice
about saving tokens that itself costs tokens on every session would be
self-defeating and would directly work against ADR-0029.

**Scope test.** Half the practices first sketched for this axis are *agent*
mechanics — grep headers not bodies, regenerate `overview.md` from headers only —
already stated in ADR-0011 / idea 0008. Restating them in a human guide would be
filler, and telling a human to "grep headers" is a raised finger, not advice. The
content that earns its place is the set of levers the **human** controls.

### Considered options (where the guidance lives)

- **A — `guide.md` only**, human-facing, read on demand. Costs nothing at session
  start; consistent with ADR-0014's register split and with ADR-0029's shrink
  goal.
- **B — `## Agent operating guidance` in `AGENTS.md`**, always loaded. Rejected:
  adds unconditional per-session weight, directly contradicting sibling ADR-0029.
- **C — The canonical `working-method.md`** so adopters inherit it in the spec.
  Rejected for the same weight reason; adopters inherit the guide too, so the
  advice still reaches them through register A.

### Decision drivers

- **Economy (#2), honestly applied:** resume-economy advice must not add
  write-time-every-session cost; it belongs in the register the agent never
  loads.
- **Consistency with ADR-0029 and ADR-0014:** keep the always-loaded spec lean;
  put human narrative in `guide.md`.
- **Signal over noise:** include only levers the human controls; exclude
  agent-mechanic restatements already owned by ADR-0011 / idea 0008 and
  cross-reference them instead.

## Decision

Add a short **"resuming cheaply"** discipline to `guide.md` (register A only),
scoped to the human-controlled levers and explicitly excluding agent-mechanic
restatements (cross-reference ADR-0011 / idea 0008 for those). The levers:

1. **How you re-open the session is the biggest lever.** "Resume plan 0007 — read
   its file and `overview.md`" costs a few reads; "catch me up on the project"
   invites reading the whole corpus.
2. **Name the artifact, not the topic.** "What does ADR-0021 decide?" opens one
   file; "what did we decide about token weight?" searches across bodies.
3. **Ask narrow.** A scoped question maps to a header grep, not a synthesis over
   everything.
4. **Invest at pause-time, not resume-time.** A regenerated `overview.md` and a
   one-paragraph travel-diary chapter (ADR-0018), written while context is fresh,
   make every future resume cheap.
5. **Terseness is a human write/approve discipline.** You author and green-light
   artifacts; terse ones are cheaper to write *and* to resume — Economy #2
   compounds on both ends.

This is **purely advisory**: no mechanism change, no new artifact family, no
cross-link vocabulary. It cross-references the travel diary (ADR-0018) and the
economical-overview mechanics (ADR-0011 / idea 0008) rather than restating them.

## Consequences

- `guide.md` gains a short, human-facing "resuming cheaply" section; the
  always-loaded spec register is untouched, so no per-session cost is added and
  ADR-0029's shrink is preserved.
- The advice reaches adopters through their copied `guide.md` without touching
  the canonical spec.
- Being advisory and outside the lifecycle, the guidance may be ignored with no
  harm to the trail; it only ever helps an operator spend fewer tokens.
- Carry-out work (authoring the `guide.md` section and confirming the
  cross-references) belongs to a follow-up plan that `Implements:` this ADR, not
  to this decision.
