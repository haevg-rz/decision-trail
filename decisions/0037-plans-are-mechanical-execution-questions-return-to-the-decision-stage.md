# ADR-0037: plans are mechanical execution — a surfaced question returns to the decision stage

- Status: accepted
- Date: 2026-07-12
- Amends: [ADR-0004](0004-a-plan-carries-a-decision-into-action.md)
- Promoted from: [Idea 0031](../ideas/0031-plans-execute-they-never-plan-decisions.md)

## Context

The lifecycle is `idea → proposal → decision → plan → execution` (promise #4).
ADR-0004 placed the **plan** downstream of an accepted **decision**: "the ADR is
the spec, the plan is the *how*, execution is the plan in motion."

That framing is correct but describes only the happy path. In real use in a
consumer repo, an agent derived a plan whose tasks included **clarifying
undecided things — deciding, inside the plan, matters that had never been
decided** ("decide X", "clarify open question Y" as ordinary execution steps).

That is a major violation of a core method concept. It collapses two distinct
lifecycle stages: **deciding** belongs to the decision stage (an ADR a human
accepts), never to the plan stage. A plan that schedules decision-making lets an
agent decide things under the cover of "just executing the plan" — with no ADR,
no confirmation guard on the decision, and no paper trail. ADR-0004's soft
wording did not prevent it because it never named the anti-pattern, nor what to
do when a question surfaces *while executing*.

Questions **will** arise mid-execution — that is normal and expected. The method
needs to say, unambiguously, that the answer is to go back **up** the lifecycle,
not to fold the decision into the plan.

## Decision Drivers

- **Lifecycle for thoughts (#4)** — the stages must stay distinct; a decision is
  made in the decision stage, not smuggled into a plan.
- **The confirmation guard** — decisions must pass through a human; an unreviewed
  "decide X" plan step bypasses that.
- **Agility (#5)** — a plan must stay revisable, but revision means re-deriving
  the *how*, not deciding the *what*.
- **Economy (#2)** — the fix should sharpen existing text, not add a new mechanic.

## Considered Options

1. **Amend ADR-0004 with an explicit anti-pattern + escalation rule** (chosen) —
   name that plans are mechanical execution only and never contain
   decision-making tasks, and fix the mid-execution escalation: a surfaced
   question returns to the decision stage.
2. **Directly edit ADR-0004 in place** — rejected: erases the trail (Agility #5
   keeps decisions append-only) and hides that the plan-stage understanding was
   hardened in response to a real incident.
3. **A rigid single escalation path (always a full new ADR)** — rejected as
   over-prescriptive: a tiny clarification does not warrant a new ADR; sizing the
   response is a judgment call.
4. **Leave it to agent guidance only** — rejected: this is a lifecycle rule, not
   just an agent habit; it belongs in the spec body, reinforced by the checklist.

## Decision

Amend ADR-0004 with an explicit rule for what a plan may and may not contain, and
what happens when a question surfaces during execution.

1. **Plans are for mechanical execution only.** A plan carries out an
   already-accepted decision: the ADR is the spec, the plan is the mechanical
   *how*, execution is the plan in motion. A plan **never contains a
   decision-making task** — no "decide X", no "clarify the open question Y". If a
   part of the work still depends on an undecided question, the plan is **not yet
   ready to be written for that part**.

2. **A surfaced question returns to the decision stage.** Questions arising while
   executing are normal. The response is **never** to add a decision step to the
   plan, but to go back up the lifecycle: **clarify the governing ADR — patch it,
   amend it (a new ADR with `Amends:`), or open a new ADR** — let the decision
   stage settle the question, then resume execution against the updated spec.

3. **The mechanic is fixed; the sizing is judgment.** *That* a surfaced question
   leaves the plan and returns to the decision stage is a fixed rule with no
   exceptions. *Which* form the return takes — a small clarifying patch to the
   ADR, an amendment, or a brand-new ADR — is a judgment call sized to the
   question (mirroring how disentangling a large idea fixes the procedure but
   leaves the strategy to the human, ADR-0027).

**Placement.** The substantive rule lands in the spec body
(`starter/docs/working-method.md` § *The lifecycle*, plans bullet; propagated to
the derived `AGENTS.md`), a short "lookup, not judgment call" bullet is added to
the agent operating guidance checklist in both `AGENTS.md` renderings, and
`guide.md` gets a brief narrative note (a learner can trip on this conceptual
point).

## Consequences

- The plan stage is hardened against the observed failure: an agent cannot
  legitimately derive a plan that schedules decision-making, and knows the
  escalation path when a question surfaces mid-execution.
- The `decision → plan → execution` hand-off stays continuous and each stage
  keeps its own job; the confirmation guard is preserved for every decision.
- ADR-0004 is amended, not rewritten — its original text stands, with an
  `Amended by:` back-link to this ADR, so the trail of *why* the plan-stage
  understanding tightened is legible.
- Adopters receive the sharpened rule through the normal copy-driven update
  (§ working-method), so the same violation is prevented in every consuming repo,
  not just the one where it was caught.
- A carried-out change to the instruction text is itself ordinary decision-trail
  work: this ADR authorizes it, and a plan `Implements:` it to make the edits.
