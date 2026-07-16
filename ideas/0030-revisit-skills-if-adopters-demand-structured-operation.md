# Idea 0030: revisit optional skills if adopters demand structured operation

- Date: 2026-07-11
- Status: seed

## What this is

A deliberately-kept **revisit reminder**, not a fresh line of thought. It springs
from a *decision*, not from budding an idea, so it carries no `Parent:` — the prose
pointer below is enough.

[ADR-0036](../decisions/0036-render-fixed-procedures-as-optional-skills.md) rejected
rendering the method's fixed procedures as optional skills. The rejection was sound
on today's evidence: the cost saving is marginal (~1% of session cost, mostly
neutralized by prompt caching), and the one solid benefit — execution reliability —
is better served by sharpening/compacting the canonical prose (idea 0021 + the
ADR-0026 discipline) than by forking it into a tool-specific second artifact that
owes perpetual sync (ADR-0014).

## The reopen condition

One driver was left explicitly open: **structured, guided operation for users
uncomfortable with the conversational method.** That benefit is real but was
*speculative* at rejection time — no concrete adopter had demanded it. This seed
exists to catch the moment it stops being speculative.

**Revisit when:** a concrete adopter (or real, repeated user friction) demands a
more structured / guided way to operate the method — at which point the deciding
driver becomes UX / adoption, *not* cost.

## What maturing this looks like

When the condition fires, this seed matures and **promotes to a new ADR that
supersedes ADR-0036** (`Supersedes:` / `Superseded by:`, ADR-0012), re-weighing
Option B (adopt skills on the reliability/UX axis) with the fresh adopter evidence
in hand. Until then it rests as `seed`, surfacing in the idea table of
`overview.md` as a live "come back to this" marker.

## Update — the ADR-0040 precedent (2026-07-16)

A first, deliberately-narrow crack in the purism has now been made, and it did
*not* spoil the method. [ADR-0040](../decisions/0040-optional-deterministic-overview-regen-script.md)
added an **optional, deterministic `overview.md` regeneration script** — the exact
kind of purely-mechanical task a machine should own rather than re-reason every
time. The lived experience is worth banking here, because it reframes what this
seed is really about:

- **The agnosticism dogma was mitigated *a little*, not abandoned.** The absolute
  "instructions-and-markdown-only" stance softened to "instructions-and-markdown
  are *normative*; an optional script may implement them." That is a real change of
  posture — but a bounded one.
- **Economy (#2) clearly won.** Regen went from ~8–13k tokens (disciplined
  hand-regen) or ~110k (naive) toward near-zero, deterministic, model-invariant.
- **Transparency / tool-agnosticism (#3) still stands well.** It held because of
  four guards, each of which is the *general recipe* for doing this safely again:
  1. **prose stays normative** — the script is an *implementation of* the spec, not
     a second source of truth;
  2. **strictly optional & additive** — absence changes nothing;
  3. **instruction-triggered, invisible to the user** — the trigger is standing
     agent guidance ("run the script if present, else regenerate by hand"), not a
     new command or harness hook;
  4. **only the *output* is contract** — so the script may be reimplemented in any
     language or simply omitted, and an adopter without the runtime falls through
     to the prose path.

So the dogma and the promises did not collide: #2 won a lot, #3 lost almost
nothing. That is the precedent this seed should carry forward.

## A widened question: more economy-win candidates?

ADR-0040 handled *one* mechanical task. The natural follow-on: **are there other
deterministic, mechanical procedures in the method that could get the same
optional-`.ps1` treatment** under the same four guards? Some candidates to weigh
(for a proposal, not this seed):

- **A conformance / lint check** — verify mandatory `Date:` headers, the canonical
  bulleted header block (ADR-0026), title-line ordinal ↔ filename agreement
  (ADR-0028), per-family status vocabulary (ADR-0024), and reciprocal cross-links
  present for amend/supersede/promotion (ADR-0012). Read-only, cheap, high-value —
  and idea 0033 already measured detection as far cheaper than generation.
- **Insert-and-shift renumbering** (ADR-0025) — renumber an out-of-order insert,
  shift every later artifact, rewire reciprocal cross-links, and regenerate
  `overview.md`. Highly mechanical but multi-file and error-prone by hand.
- **Reciprocal-link integrity** — flag a forward `Promoted to:` / `Amends:` /
  `Supersedes:` whose back-link is missing (a natural subset of the conformance
  check).

Each is a plausible "Economy wins again" case; each must clear the *same* four
guards before it earns a script.

## What this seed now is

Two axes now live under this one reminder, and they should not be conflated:

- **The reliability/UX axis** (original) — revisit ADR-0036's *skills* rejection
  when a concrete adopter demands structured, guided operation (the reopen
  condition above still governs this).
- **The economy/script axis** (added) — ADR-0040 opened it; the widened question
  above tracks the remaining mechanical candidates.

Held together, this seed is the **preliminary staging ground** for eventually
promoting the broader "optional structured tooling" idea — scripts first, skills
if/when the UX driver fires — *without* spoiling the method. It stays `seed`: a
place to accumulate evidence and candidates until one of the two axes matures
enough to promote on its own.
