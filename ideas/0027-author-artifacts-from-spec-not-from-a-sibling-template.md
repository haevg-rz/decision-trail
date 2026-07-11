# Idea 0027: author new artifacts from the spec, not from a sibling as a template

- Date: 2026-07-11
- Status: seed

## Observation

While preparing to draft a proposed ADR (promoting [idea 0026](0026-guide-sync-model-cant-hold-audience-deltas.md)),
the agent reflexively opened a recent same-family ADR "to see the shape" — using
an existing artifact as a fill-in-the-blanks **template** rather than authoring
from the specification. The human caught it.

The reflex is dangerous even though the format is *already fully pinned*:

- the **header block** — `- Date:` then `- Status:`, then cross-link fields,
  optional `- Tags:` (ADR-0026);
- the **title line** — typed, zero-padded H1 ordinal matching the filename
  (ADR-0028);
- **per-family status** — a new proposal is `proposed`, a new idea `seed`, a new
  plan `draft`, never borrowed (ADR-0024);
- the **body template** — classic Status / Context / Decision / Consequences,
  plus Decision Drivers / Considered Options when weighing alternatives (ADR-0014,
  ADR-0001/0003).

Copying a sibling imports its **incidental reality** — the wrong status
(`accepted` instead of `proposed`), its specific `Amends:` / `Promoted from:`
cross-links, its particular section choices. That is a fresh source of exactly the
kind of drift the method works to prevent, and the current agent operating
guidance says nothing against it.

## Why this deserves its own thread

The mechanics above are lookups, not judgment calls — the guidance already frames
them that way. What is missing is a rule that closes the *sourcing* question:
**where does the shape of a new artifact come from?** Today an agent may satisfy
"follow the mechanics" while still scaffolding from a sibling, silently absorbing
that sibling's incidental content.

This is **generic** — every adopter's agent shares the reflex — so any rule
belongs in the agent operating guidance that ships via `starter/AGENTS.md`, not
only in this repo's copy.

A candidate rule:

> **Author from the spec, never from a sibling.** A new artifact's header, title
> line, status, and body template are fully specified (§ *The lifecycle*). Do not
> open an existing artifact as a *template* — copying imports incidental reality
> (a wrong status, the wrong cross-links). Reading a sibling to check that the
> format is being followed is fine; using one as a fill-in-the-blanks scaffold is
> not. If you feel you need an example to know the shape, that is a signal the
> *spec* is unclear — sharpen the spec, don't copy.

## A latent spec gap this surfaced

The same investigation exposed a small underspecification. The spec pins the
header and the template *sections*, but **not the wording a proposal uses for its
decision heading**. Existing proposals wrote **`## Proposed decision`** while
`Status: proposed` (e.g. ADR-0014), reading as the `## Decision` section once
accepted — but that is an *observed habit*, not a written rule. An agent authoring
strictly from the spec has no instruction telling it `## Proposed decision` vs
`## Decision`, which is precisely the kind of hole that sends an agent reaching for
a sibling in the first place. Pinning this convention both removes an ambiguity and
strengthens the "author from the spec" rule by making the spec actually sufficient.

## Open questions

- Is the fix purely a **new agent-guidance rule** ("author from the spec, never
  from a sibling"), a **spec sharpening** (pin the `## Proposed decision` heading
  convention), or **both** — likely both, since each reinforces the other?
- Where does the rule live? Agent operating guidance is carried in both this
  repo's `AGENTS.md` and `starter/AGENTS.md`; the spec text lives canonically in
  `starter/docs/working-method.md`. Which additions land where?
- Should the `## Proposed decision` → `## Decision` transition be stated as a rule
  (rename on acceptance) or left as the single heading `## Decision` throughout,
  with status alone marking proposal-vs-decision?
- Does "never from a sibling" over-reach — are there legitimate cases (e.g. a
  genuinely novel section an agent has no spec for) where consulting prior art is
  the honest move, and how is that bounded without reopening the judgment-call door?
