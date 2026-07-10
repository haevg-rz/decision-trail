# Idea: overview regeneration should be more economical

- Date: 2026-06-29
- Status: promoted
- Promoted to: [ADR-0016](../decisions/0016-overview-regeneration-on-explicit-request-only.md)

## Observation

The current rule requires the agent to regenerate `overview.md` after **every
single artifact change** — a new idea, a status flip, a plan checkbox. This
violates promise #2 (Economy): it adds cost and noise to every interaction, even
when the user does not care about the index at that moment.

## Desired improvement

Make regeneration cheaper or deferred. Candidates:

1. **Explicit user command only** — the agent never regenerates automatically;
   the user asks for it when they want a fresh snapshot. Simplest; the overview
   may be stale between requests, but it is always clearly "as of <date>" so
   staleness is visible.

2. **Separate confirmed step** — after completing artifact work the agent
   proposes "regenerate overview?" as a distinct, explicit follow-up and waits
   for confirmation before doing it. Keeps the user in control without requiring
   them to remember to ask.

3. **Batched at session end** — regenerate once at the end of a working session
   (e.g. before committing), not after each individual change.

## Open questions

- Is a stale overview acceptable as long as the "as of" stamp makes staleness
  visible?
- Does the current rule exist because agents were forgetting to update at all,
  and removing it risks regression to that problem?
- Should the rule differ between the method's own repo and adopting repos?
