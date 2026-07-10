# Idea: status vocabulary is per-family — guard against cross-contamination

Date: 2026-07-10
Status: promoted
Promoted to: [ADR-0024](../decisions/0024-status-vocabulary-guard-per-family.md)

## Observation

In a consuming repo an agent created a fresh idea and headed it
`Status: proposed`. That value belongs to the **proposal/decision** family, not
the **idea** family — a newly created idea must start at `seed`. The same agent
had previously flagged a plan as `proposed` instead of `draft`. Both are the
same underlying mistake: **borrowing a status word from the wrong artifact
family.**

The method's mechanics are correct — each family's state machine is well
defined. What is missing is a *guardrail* against mixing the vocabularies. Three
things in the current documentation make this error easy for any adopter (human
or agent):

1. **No stated entry status.** The lifecycle table shows `seed → promoted /
   dropped` and `draft → active → done / abandoned`, but nowhere states in words
   that a **newly created** idea *starts* at `seed` and a **newly created** plan
   *starts* at `draft`. The initial state must be inferred from an arrow.

2. **`proposed` is primed for misuse.** The word appears both in the lifecycle
   table (for proposals) *and* prominently in "How to start working" step 2
   (`open an ADR … with Status: proposed`). It is the most visible status word
   in the document, so it is the one reached for by default — even when the
   artifact in hand is an idea or a plan.

3. **No "don't mix families" guard.** Contrast with **artifact numbering**,
   which is an equally easy trap and *did* get an explicit, repeated guard
   ("ordinal only — never derive a number from a related artifact", ADR-0015 /
   idea 0007) precisely because it is easy to get wrong. Status vocabulary has no
   equivalent guard. This is the same class of implicit-rule gap that idea 0006
   ("documentation flaw") already recognized once.

## Desired clarification

Make the per-family status vocabulary explicit and guarded, visible in both
`AGENTS.md` and `starter/docs/working-method.md`:

- **State the entry status in words** for each family: a new idea starts `seed`;
  a new proposal starts `proposed`; a new plan starts `draft`. Optionally
  annotate the lifecycle table's status column to mark which value is the
  *initial* one.
- **Add a short per-family exclusivity guard**, in the same spirit as the
  ordinal-only numbering guard: *status values are drawn only from the artifact's
  own family; never borrow another family's status* — e.g. an idea is never
  `proposed` or `draft`; a plan is never `proposed` or `seed`.
- Consider phrasing that nudges the reader to **name the artifact family first,
  then pick from that family's list only.**

## Open questions

- Does this warrant its own ADR, or is it small enough to fold into a future
  documentation-consistency ADR (cf. ADR-0014)?
- Should the guard live in the derived-method body (so it reaches adopters via
  the copy-driven update) or only in the agent-guidance section, or both?
- Is annotating the lifecycle table's status column worth the added visual noise,
  or is a one-line prose guard beneath the table enough?
