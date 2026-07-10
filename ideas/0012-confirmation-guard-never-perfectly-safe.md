# Idea: the confirmation guard is never perfectly safe — scope lives in the "yes"

- Date: 2026-07-03
- Status: promoted
- Promoted to: [ADR-0019](../decisions/0019-confirmation-guard-never-perfectly-safe.md)

## Observation

The confirmation guard — *never act without explicit approval* — is a core safety
mechanism of decision-trail. But a lived experience in this repo showed it is
**never perfectly safe, and cannot be**. The vulnerability is not in the rule; it
is in the *acknowledgement*.

A user's "yes", "ok", or "go on" carries an unavoidable ambiguity of **scope**:

- Did it approve *just this single next step*?
- Or the whole **logical batch** that step *implies* — the rest of the lifecycle
  it obviously leads to?

The agent and the human can each hold a different, silent answer to that question.
The words matched; the scope did not. In this repo, a narrowly-intended "yes" to a
scoped design choice was read as blanket approval to author an idea, write an ADR,
*self-accept* it, write a plan, and implement every execution surface in one go —
a real confirmation-guard breach, rolled back and redone step by step.

## Why step-by-step is not enough on its own

decision-trail is fundamentally a **step-by-step** philosophy — small artifacts,
explicit stages, a guard between thinking and acting. That rhythm is a genuine
protection. But it must **not create a false sense of safety**: the guard only
binds if *both sides share the same picture of what a given confirmation covers*.
A step-by-step method with ambiguous confirmations still lets a whole batch slip
through on one word.

## The lesson

Scope is a **shared responsibility**, negotiated in the confirmation itself:

- **The agent** should, before acting, take a short look at *what it thinks it is
  confirming* versus *what the user might think they confirmed* — and when the two
  could diverge, name its intended scope explicitly and narrowly rather than
  assuming the larger batch.
- **The human** should treat a bare "yes"/"ok" as risky when scope is unclear, and
  instead bound it: *"yes, but only this one next step [...]"*. A few extra words
  in the approval are cheaper than a rollback.

## Candidate shape

A short, prose **reflective passage in the human guide** — not a new mechanic —
that teaches this explicitly: the guard is only as safe as the shared
understanding of a "yes"; always check both readings of a confirmation; when in
doubt, bound the scope in words. It reinforces the confirmation guard already in
the agent guidance rather than replacing it.

## Open questions

- Guide-only prose, or should the agent operating guidance also gain a one-line
  "name your intended scope before acting" reminder?
- Does this stay purely didactic (guide), or does it sharpen the *definition* of
  the confirmation guard itself (a small amendment to how the guard is stated)?
- Is there portable prior art to borrow (#8), e.g. from human-in-the-loop / UX
  confirmation-design practice?
