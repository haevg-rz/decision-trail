# ADR-0016: Overview regeneration should be more economical

- Date: 2026-06-29
- Status: accepted
- Promoted from: [Idea-0008](../ideas/0008-overview-regeneration-should-be-more-economical.md)

## Context

The current rule requires the agent to regenerate `overview.md` after every
single artifact change. In practice this means every idea creation, every status
flip, and every plan checkbox tick triggers a wholesale file rewrite. This
conflicts with promise #2 (Economy): it adds cost and noise to every interaction,
even when the user has no interest in the index at that moment.

## Decision Drivers

- Promise #2: Economy — cheap to write, cheap to resume.
- The "as of <date>" stamp already makes staleness visible to any reader.
- The original motivation for the rule was preventing agents from *never*
  updating the overview; a lighter rule must not regress to that.

## Considered Options

1. **Explicit user command only** — agent never regenerates automatically; user
   asks when they want a fresh snapshot.
2. **Separate confirmed step** — after completing artifact work the agent proposes
   "regenerate overview?" as a distinct follow-up and waits for confirmation.
3. **Batched at session end** — regenerate once before committing / closing the
   session, not after each individual change.

## Decision

Replace the "after every change" rule with **option 1: explicit user command
only**.

- The agent regenerates `overview.md` when the user explicitly asks (e.g.
  "update the overview", "regenerate overview").
- The agent does **not** regenerate automatically after creating or updating
  individual artifacts.
- The "as of <date>" stamp ensures any reader can see how fresh the snapshot is.

Option 2 (confirmed step) was considered but rejected: asking for confirmation
after every artifact change is still noisy — it just moves the interruption from
action to question. Option 3 (session end) is harder to define precisely across
different agent runtimes.

## Consequences

- `overview.md` may be stale between explicit requests; the stamp makes this
  transparent.
- Agents are cheaper to run and interactions are less cluttered.
- The rule in `AGENTS.md` and `starter/docs/working-method.md` must be updated
  to reflect the new trigger.
