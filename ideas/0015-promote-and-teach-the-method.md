# 15. Promote and teach the method — a didactical guide, and a German translation

- Status: promoted
- Date: 2026-07-05
- Promoted to: [ADR-0023](../decisions/0023-promote-and-teach-the-method.md)

## Idea

The method is settled and usable, but it is barely *taught*. `guide.md` exists as a
narrative introduction, yet it falls short of being genuinely **educational and
didactical**: it explains what the method is more than it teaches a newcomer how to
*learn and adopt* it — no gentle on-ramp, worked example, motivation-before-mechanics,
or progressive build-up from a first idea to a full lifecycle.

This idea has two threads:

1. **Promote & teach.** Make the method something people can *learn*, not just
   reference. Rework/extend `guide.md` (or add companion material) into a didactical
   piece: motivate the problem first, walk a concrete end-to-end example, introduce
   the eight promises and the lifecycle progressively, and lower the barrier to first
   use.
2. **German translation.** Once the teaching material is solid, provide a German
   translation so the method reaches a German-speaking audience.

## Why it matters

- **Economy (#2) / Continuity (#1):** a method that is hard to learn is expensive to
  adopt; good teaching lowers that cost.
- **Genericity (#7):** promotion and translation widen who can pick it up.
- Teaching material and translations are companions to the method, not changes to the
  contract — but reworking `guide.md`'s role may touch the documentation-audience
  concerns already noted in idea 0006.

## Open questions (for a future proposal)

- Rework `guide.md` in place, or add a separate tutorial/onboarding artifact alongside
  it?
- What is the canonical worked example to teach with?
- Is the German translation of `guide.md` only, or also `working-method.md` /
  `AGENTS.md`? How is translation drift kept in sync with the (derived) English canon?
- Should translations live in-repo (e.g. `guide.de.md`) or elsewhere?
