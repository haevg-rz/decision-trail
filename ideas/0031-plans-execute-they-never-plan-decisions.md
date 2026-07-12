# Idea 0031: plans execute — they never "plan decisions"

- Date: 2026-07-12
- Status: promoted
- Promoted to: [ADR-0037](../decisions/0037-plans-are-mechanical-execution-questions-return-to-the-decision-stage.md)

## Observation

An incident surfaced while the method was in use in a consumer repo. An agent
derived a plan, and **part of that plan was to clarify undecided things — to
make, inside the plan, decisions that had not yet been decided.** The plan
carried steps like "decide X" / "clarify Y" as ordinary execution tasks.

That is a **major violation of a core method concept**. The lifecycle is
`idea → proposal → decision → plan → execution`: a plan sits *downstream* of an
accepted decision. Deciding is the job of the **decision** stage (an ADR), not
the **plan** stage. A plan that schedules decision-making collapses two
distinct lifecycle stages into one and lets an agent decide things under the
cover of "just executing the plan" — with no ADR, no confirmation guard on the
decision, no paper trail.

The rule an agent must internalize:

- **A plan carries out an already-accepted decision — the ADR is the spec, the
  plan is the mechanical *how*, execution is the plan in motion.** Plans are for
  mechanical execution.
- **Plans never "plan decisions."** A plan task is never "decide X" / "clarify
  the open question Y." If a decision is still open, the plan is not ready to be
  written for that part yet.
- **Questions *will* arise during execution — that is normal.** The correct
  response is **not** to fold the decision into the plan, but to go back up the
  lifecycle: **clarify the ADR — patch or amend it** (or open a new one). Once
  the decision stage settles the question, execution resumes against the updated
  spec.

## The candidate

Harden the AI instructions (`AGENTS.md` and `starter/docs/working-method.md`,
which propagates to adopters) so an agent **cannot** derive a plan that
schedules decision-making, and knows the escalation path when a question
surfaces mid-execution.

The spec today (§ *The lifecycle*) already says a plan "carries an accepted
decision into action: the ADR is the spec, the plan is the *how*." That framing
is correct but **too soft to prevent the observed failure** — it describes the
happy path without naming the anti-pattern or the mid-execution escalation.

Candidate shape (to be sharpened when this matures):

1. **Spec (§ *The lifecycle*, plans bullet):** state explicitly that plans are
   for *mechanical execution only* and **never contain decision-making tasks**;
   a still-open question is decided in the **decision** stage, not the plan.
2. **Spec — mid-execution escalation:** when a question arises while executing,
   the answer is to **clarify / patch / amend the ADR** (or open a new one), then
   resume — never to add a "decide X" step to the plan.
3. **Agent operating guidance checklist:** add a bullet flagging this trap in
   the same "lookup, not judgment call" list, pointing back to the spec — so the
   agent scans it before writing a plan.

## Why this deserves a thread

It is **generic** — every adopter writes plans; any agent can slip a "decide X"
task into a plan, so the same violation can recur anywhere, not just the repo
where it was caught.

It defends a **core promise** — the *lifecycle for thoughts* (#4) and the
*confirmation guard*: decisions must go through the decision stage (an ADR),
where a human accepts them, not slip through as unreviewed plan steps.

## Open questions — resolved

- **One ADR or an amendment?** Resolved: a **new dedicated ADR that `Amends:`
  ADR-0004** (the decision that defined the plan/execution stage), with the
  reciprocal `Amended by:` back-link. The hardening does not reverse ADR-0004 —
  which already says "the ADR is the spec, the plan is the *how*" — it sharpens
  it by naming the anti-pattern and the escalation path. Amending keeps ADR-0004
  stable and gives this gap its own paper trail (same shape as ADR-0035).

- **How prescriptive is the escalation?** Resolved: **forbid the in-plan
  decision absolutely** — the hard rule ("a plan never contains a
  decision-making task; a surfaced question goes back to the decision stage") is
  a fixed lookup — but **leave the choice among patch / amend / new-ADR to
  judgment**, sized to the question. This mirrors the method's standing pattern
  (fixed *mechanic*, human *strategy*), as with disentangling a large idea.

- **Where exactly the hardening text lives?** Resolved: **spec body + agent
  operating guidance checklist, in both renderings, plus a brief guide note.**
  1. **Spec (§ *The lifecycle*, plans bullet)** — the substantive rule: plans
     are mechanical execution only, never contain decision tasks; a surfaced
     question returns to the decision stage (clarify / patch / amend the ADR, or
     open a new one), then execution resumes.
  2. **Agent-guidance checklist** — a short "lookup, not judgment call" bullet
     flagging the trap ("a plan task is never 'decide X'"), pointing back to the
     spec and the new ADR.
  3. Both renderings — canonical `starter/docs/working-method.md` →
     derived `AGENTS.md`; `starter/AGENTS.md` checklist → repo `AGENTS.md`.
  4. **`guide.md`** — a brief matching narrative note, since this is a
     conceptual point a learner can trip on.
