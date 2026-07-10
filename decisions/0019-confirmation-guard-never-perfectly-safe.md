# ADR-0019: Teach that the confirmation guard is never perfectly safe

- Date: 2026-07-03
- Status: accepted
- Promoted from: [Idea-0012](../ideas/0012-confirmation-guard-never-perfectly-safe.md)

## Context

Idea 0012 recorded a lived lesson from this repo: the **confirmation guard** —
*never act without explicit approval* — is never perfectly safe, and cannot be.
The weakness is not the rule but the **acknowledgement**. A user's "yes" / "ok" /
"go on" carries an unavoidable ambiguity of *scope*: did it approve just this one
next step, or the whole logical batch that step implies? Agent and human can hold
different silent answers; the words match while the scope does not. In this repo a
narrowly-intended "yes" was read as blanket approval to run an entire lifecycle
(idea → ADR → self-accept → plan → full implementation) in one go — a real breach,
rolled back and redone step by step.

decision-trail is already a step-by-step philosophy, and that rhythm genuinely
helps. But it must not create a *false* sense of safety: the guard only binds if
both sides share the same picture of what a given confirmation covers.

The natural home for this is the **human guide** — the didactic register (ADR-0014)
— which today explains the guard's *existence* but not its *fragility*.

## Decision drivers

- **Transparency (#3) / honesty:** name a real limitation of the method rather
  than implying the guard is airtight.
- **Continuity (#1):** a lesson learned in one session should be captured so it is
  not re-learned the hard way.
- **Economy (#2):** prefer the lightest form that teaches the lesson — prose in the
  guide, not a new mechanic or artifact type.
- **Register discipline (ADR-0014):** didactic reflection belongs in the guide;
  the terse operating rule belongs in the agent guidance. Keep each where it fits.
- **Borrow, don't invent (#8):** this mirrors human-in-the-loop / confirmation-UX
  practice (bounded, unambiguous confirmations); we lean on that intuition rather
  than inventing a formalism.

## Considered options

1. **Do nothing — the breach was a one-off.** Rejected: the ambiguity is
   structural, not incidental; leaving it untaught invites recurrence.
2. **A reflective prose passage in the guide (chosen).** Teaches that a "yes" has
   scope, that step-by-step is not self-securing, and that scope is a shared
   responsibility — with the concrete habit of bounding a confirmation in words.
3. **Redefine/harden the guard itself into a new mechanic** (e.g. mandatory
   scope-echo before every action). Rejected for now as over-engineering and a
   friction tax on every interaction; the lesson is better taught than enforced.
   Left open as a future decision if prose proves insufficient.

### Sub-choice: guide-only, or also a one-line agent reminder?

The idea asked whether the agent operating guidance should also gain a short
reminder. The guard already lives there. This ADR adds **one sentence** to the
existing confirmation-guard bullet — "before acting, name your intended scope
explicitly, especially when a 'yes' could be read as approving a larger batch" —
so the agent side of the shared responsibility is stated where the agent reads it,
while the full teaching lives in the guide. This stays within register discipline:
the guide teaches, the guidance instructs, neither duplicates the other at length.

## Decision

Add a short **reflective prose passage** to the canonical human guide
(`starter/docs/guide.md`), regenerated wholesale into this repo's derived
`guide.md` (ADR-0014, paths-only delta), near where the confirmation guard / how
the method is used is discussed. The passage teaches:

- the confirmation guard is a core safety mechanism but is **never perfectly
  safe**, because a "yes" carries ambiguous **scope** — this one step, or the batch
  it implies;
- step-by-step working helps but must **not** give a false sense of safety; the
  guard binds only when both sides share the same picture of what was confirmed;
- **scope is a shared responsibility**: the agent should check both readings and
  name its intended scope before acting; the human, when in doubt, should bound the
  approval in words — e.g. *"yes, but only this single next step [...]"* rather than
  a bare "yes" or "ok".

Additionally, extend the existing **confirmation-guard bullet** in the agent
operating guidance (this repo's `AGENTS.md` and `starter/AGENTS.md`) with **one
sentence**: before acting, name the intended scope explicitly, especially when a
bare approval could be read as covering a larger batch.

**Version stays v2.4** — no bump and no `CHANGELOG.md` entry as part of this ADR;
this change is batched with further ideas already anticipated, and the release is
cut when that batch lands.

This is additive and purely documentary: no lifecycle, artifact family, or
cross-link vocabulary changes.

## Consequences

- The guide honestly documents a real limit of the guard, and gives both human and
  agent a concrete habit (bound the scope in words; echo intended scope) that makes
  the guard materially safer without new machinery (Transparency #3, Economy #2).
- The lesson is captured once and travels to adopters via the canonical guide, so
  it need not be re-learned per project (Continuity #1, Genericity #7).
- Register discipline (ADR-0014) is preserved: the guide carries the teaching; the
  agent guidance carries a single instructing sentence; no long duplication.
- The guard is **not** turned into a heavier mechanic; hardening it into an
  enforced scope-echo remains an open future decision if prose proves insufficient.
- Because v2.4 is held, `CHANGELOG.md` is untouched now; the next release note will
  cover this ADR together with the anticipated follow-on ideas.
- On acceptance, a plan will: add the reflective passage to `starter/docs/guide.md`;
  regenerate this repo's `guide.md`; append the one-sentence scope reminder to the
  confirmation-guard bullet in `AGENTS.md` and `starter/AGENTS.md`; and regenerate
  `overview.md`. No version bump, no CHANGELOG entry.
