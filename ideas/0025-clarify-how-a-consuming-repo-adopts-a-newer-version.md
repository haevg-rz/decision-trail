# Idea 0025: clarify how a consuming repo adopts a newer version of decision-trail

- Date: 2026-07-11
- Status: promoted
- Promoted to: [ADR-0031](../decisions/0031-adopter-update-is-human-intent-agent-execution.md)

## Observation

The update path — moving an already-adopting repo from one version of
decision-trail to a newer one — is the least clear part of the on-ramp. In
[`adopting.md`](../adopting.md) it is **chapter 3 ("Update `X.Y → X.Y+n`")**, and
from a human reader's point of view it currently reads as overcomplicated and a
little deterrent: a dense block of re-copy rules, a preserve-vs-overwrite table,
citation bumps, changelog-migration ordering, and a six-point conformance check.
The *mechanics* are sound (they come from ADR-0022 — re-copy the `starter/`
method-owned set, bump the citation, apply each release's `Adopter migration:`
note in order, regenerate `overview.md`, run the conformance check), but the
*presentation* buries the simple question a human actually asks:

> *"I'm sitting in my own repo that already uses decision-trail. A newer version
> is out. What, concretely, do I do?"*

It is not even obvious this is best done as a copy-and-migrate at all versus, say,
letting the agent simply read the target version and reconcile — i.e. **adopting
the newer version by using the method on itself**.

## Why this deserves its own thread

This is exactly the kind of question decision-trail exists to answer *decision-trail*:
capture it as an idea, weigh options in an ADR, and carry the chosen shape into a
plan — rather than hand-patching `adopting.md`'s chapter 3 with more prose. The
rework may keep the ADR-0022 contract intact and only re-present it for a human,
or it may propose a genuinely simpler update ritual; that is a decision to reason
out in the open, not to guess at now.

## Open questions

- Is the confusion purely *presentational* (rewrite chapter 3 as a concrete,
  human-friendly step-by-step) or *substantive* (the update ritual itself is
  heavier than it needs to be)?
- Can "bring me current" be expressed as a single concrete walkthrough a human can
  follow without the preserve/overwrite table — e.g. an ordered checklist the agent
  executes end to end?
- Does the ADR-0022 update contract need refining, or only re-teaching? Any change
  to the contract itself must be made as a new ADR that amends/cross-links ADR-0022,
  not an informal edit.
- Where does the human-facing walkthrough live — `adopting.md` only, or is a short
  "updating" note also warranted in `guide.md`?
- How does this relate to the deferred GitHub-*template* option (ADR-0008) for a
  one-click start?
