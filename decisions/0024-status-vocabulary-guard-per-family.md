# ADR-0024: Status vocabulary is per-family — state entry status and guard against cross-contamination

Date: 2026-07-10
Status: accepted
Promoted from: [Idea-0015](../ideas/0015-status-vocabulary-guard-per-family.md)

## Context

In a consuming repo an agent created a fresh idea and headed it
`Status: proposed` — a value from the **proposal/decision** family, not the
**idea** family (a new idea must start at `seed`). The same agent had earlier
flagged a plan as `proposed` instead of `draft`. Both are one underlying
mistake: **borrowing a status word from the wrong artifact family.**

The state machines themselves are correct and already tabulated in the
lifecycle section. What is missing is a *guardrail* against mixing the
vocabularies. Three properties of the current documentation make the error easy
for any adopter (human or agent):

1. **No stated entry status.** The lifecycle table shows `seed → promoted /
   dropped` and `draft → active → done / abandoned`, but never states in words
   that a newly created idea *starts* at `seed` and a newly created plan *starts*
   at `draft`. The initial state must be inferred from an arrow.
2. **`proposed` is primed for misuse.** It appears both in the lifecycle table
   (for proposals) and prominently in "How to start working" step 2 (`open an
   ADR … with Status: proposed`) — the most visible status word in the document,
   so the one reached for by default even on an idea or a plan.
3. **No exclusivity guard.** Artifact numbering — an equally easy trap — got an
   explicit, repeated guard (ADR-0015, "ordinal only; never derive a number from
   a related artifact"). Status vocabulary has no equivalent, despite being the
   same class of implicit-rule gap already recognized once in ADR-0014.

## Decision

Make the per-family status vocabulary **explicit and guarded** in both method
renderings (`AGENTS.md` and `starter/docs/working-method.md`).

1. **State the entry status in words**, alongside the lifecycle table: a new
   idea starts `seed`; a new proposal starts `proposed`; a new plan starts
   `draft`. (Decisions and executions are in-place continuations of a proposal
   and a plan respectively, so they have no separate entry status.)
2. **Add a per-family exclusivity guard**, in the same spirit and location as
   the ordinal-only numbering guard: *a status value is drawn only from the
   artifact's own family; never borrow another family's status.* Concretely — an
   idea is never `proposed`, `draft`, `accepted`, `active`, or `done`; a plan is
   never `proposed`, `seed`, or `accepted`; a proposal/decision is never `seed`
   or `draft`.
3. **Prescribe the ordering heuristic:** name the artifact family first, then
   pick a status from *that family's* list only.

The guard belongs in the **derived method body** (so it reaches adopters via the
copy-driven update), reinforced by a short bullet in the **agent-guidance**
section — mirroring how the numbering rule appears in both places.

## Consequences

- Agents and humans get an unambiguous rule for the initial status of a new
  artifact, and an explicit prohibition against cross-family status words — the
  same protection numbering already enjoys.
- Both method renderings must be updated together (per ADR-0014's sync rule), and
  the change reaches existing adopters through the copy-driven "bring me current"
  update path (ADR-0022).
- The lifecycle table may optionally annotate which value is the *initial* one;
  whether that visual change is worth the noise, versus a one-line prose guard
  beneath the table, is left to the implementing plan.
- No behavioral change to any state machine — this is a documentation/guardrail
  clarification only, so the CHANGELOG entry's `Adopter migration:` is "none"
  (the new wording arrives automatically via the copied method text).
