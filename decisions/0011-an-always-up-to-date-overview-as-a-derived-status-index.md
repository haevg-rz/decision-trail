# 11. An `overview.md` status index, regenerated as a dated snapshot

- Status: accepted
- Date: 2026-06-28
- Promoted from: [idea 0003](../ideas/0003-an-always-up-to-date-overview.md)
- Amends: ADR-0005 (extends the header conventions: ideas and plans gain a `Date:` field)
- Amended by: [ADR-0026](0026-pin-canonical-artifact-header-format.md)

## Context

The method now produces a growing set of artifacts across three families
(`ideas/`, `decisions/`, `plans/`). The lifecycle directories tell you *what
exists* but not, at a glance, *what is still open versus done*. As the set
grows this matters in two specific ways the contract already anticipates:

- ideas pile up at status `seed` — *not now, but do not forget*;
- decisions pile up at status `proposal` — *deferred for later processing*.

Idea [ADR-0003](../ideas/0003-an-always-up-to-date-overview.md) asks for an
always-current `overview.md`: a single table listing every idea, decision, and
plan with its **name**, **creation date**, and — most importantly — its
**state**. The character is a plain **to-do / what's-done** list for a human
keeping track. The agent should keep it current after doing work; the user may
also flip a state by hand.

This raises four questions the idea left open: where the file lives, whether it
is generated or hand-kept, where the creation date comes from, and how it is
kept from drifting out of date. The last is the hard one: a derived index
maintained by hand silently rots, and "always up-to-date" is a promise hand
maintenance cannot keep. The resolution below answers it by **regenerating the
file as a dated snapshot** rather than incrementally patching a parallel copy.

### Decision drivers

- **Transparency (#3)** and **Borrow, don't invent (#8):** the overview must be
  plain, readable markdown with no tool required to view it — like the task
  lists ADR-0004 borrowed. No external generator, build step, or dependency.
- **Economy (#2):** cheap to produce; rebuilding the table is a bounded read of
  the artifact headers plus one write.
- **Continuity (#1):** a returning session sees the whole open/done picture in
  one file, stamped with how fresh it is.
- **Genericity (#7):** it must drop into any adopting project unchanged.

A note on the ADR-0004 precedent: a plan checkbox lives only in the plan — it is
not a copy of state held elsewhere, so it cannot drift. `overview.md` *does*
duplicate state that lives in the artifact headers, so it needs more than a
"keep it current by hand" rule. Regenerating it wholesale from those headers —
not maintaining a second copy — is what keeps the duplication honest.

## Decision

Add a single **`overview.md`** — a derived status index over all three artifact
families, **regenerated wholesale from the artifact headers as a dated
snapshot**, never incrementally hand-patched.

- **Location.** `overview.md` sits at the artifact root, beside the three
  family directories. In *this* repository that is the repo root. In an adopting
  project it is `docs/overview.md`, and it ships in `starter/docs/`.

- **Content.** An **"as of YYYY-MM-DD" stamp** at the top, then three tables —
  Ideas, Decisions, Plans — each row carrying:
  - **Name** — a relative markdown link to the artifact,
  - **Created** — the artifact's creation date,
  - **State** — its current lifecycle status (`seed`/`promoted`/`dropped`;
    `proposed`/`accepted`/`rejected`; `draft`/`active`/`done`/`abandoned`).

  The file is a navigation aid, not a lifecycle artifact, so it carries no
  status header and is not numbered.

- **Creation date source.** The date comes from the artifact's own header
  `Date:` field. ADRs already carry one; this ADR extends the header convention
  of ADR-0005 so **ideas and plans also carry a mandatory `Date:` field**.
  Reading the date from the file (not git) keeps the source self-contained and
  offline (Transparency #3).

- **Regenerated, not maintained.** `overview.md` is rebuilt in full by reading
  the artifact headers and writing the file fresh — there is no script, build
  step, or dependency; the agent does the read-and-write as an ordinary markdown
  operation (Economy #2, Borrow #8). Because it is recomputed from the source of
  truth rather than patched, it cannot half-update or drift into a state the
  headers don't support. *Regeneration is an agent action, not external tooling.*

- **A dated snapshot, honest about freshness.** The file is true **as of its
  stamp** and claims no more. The stamp is the visible staleness marker: between
  regenerations the headers are the source of truth and the snapshot may lag,
  but the date makes that lag legible instead of hidden.

- **Produced two ways.**
  1. **On explicit user request, any time** — the user can ask the agent
     "regenerate the overview" and get a fresh, re-stamped snapshot on demand.
  2. **As part of the agent's definition of done** — after work that creates an
     artifact or changes a state, the agent regenerates the overview in the same
     change.

- **Responsibility.** Keeping `overview.md` current is the **agent's**
  responsibility, never the user's burden — the user is never expected to edit
  the overview at all. The user *may* flip a state directly in an artifact (and
  then owns only that the change makes sense), or simply ask the agent to do it;
  either way the next regeneration reconciles the index. A user's manual edit
  therefore self-heals and never rots into something the user must repair.

## Consequences

- The whole open/done picture lives in one plain-markdown file, readable with no
  tooling and walkable to every artifact by relative link (Continuity #1,
  Transparency #3).
- Ideas stuck at `seed` and decisions stuck at `proposal` are now visible in one
  place, serving the "don't forget" intent that motivated the idea.
- Ideas and plans gain a mandatory `Date:` header field (a small extension to
  ADR-0005); existing idea files predating this ADR are backfilled when next
  touched.
- The "as of" stamp makes the snapshot honest: it never claims to be more current
  than it is, and the user can always demand a fresh regeneration. Drift becomes
  visible and on-demand-curable rather than silent — the failure mode of a
  hand-maintained derived index is avoided.
- Because the file is regenerated from the headers rather than maintained as a
  parallel copy, it cannot drift into a state the artifacts don't support; the
  artifacts remain the single source of truth and the overview is purely derived.
- Keeping it current is the agent's responsibility, never the user's; a user's
  manual state-flip self-heals at the next regeneration (Economy #2).
- The method itself gains its first *use-phase* feature — exercised the-way, as a
  proposed-then-accepted ADR — demonstrating "settled, not frozen."
- A plan carries this out: create `overview.md` here, add it to `starter/`, add
  the `Date:` convention and the regenerate-on-demand duty to the working-method
  text. Ships in the next version (`CHANGELOG.md`).
