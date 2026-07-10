# Idea: a human-friendly travel diary for the human-machine interface

- Date: 2026-07-03
- Status: promoted
- Promoted to: [ADR-0018](../decisions/0018-a-travel-diary-for-the-human-machine-interface.md)

## Observation

decision-trail already answers, with technical precision, the machine-facing
continuity questions. After a break, an agent can reconstruct exactly where the
work stands: `overview.md` gives an up-to-date derived status index, the active
plan gives a precise continuation point, and the ADRs give the reasoning. The
*trail* is complete and the *source of truth* is solid.

Yet something is missing at the **human-machine interface**. When a colleague
walks up and asks:

- *Where are we?*
- *What was achieved / changed in the last session?*
- *What is left?*
- *What is next?*

…the honest answer today is "browse the respective repo documents" — read
`overview.md`, open the active plan, skim the recent ADRs, and synthesize. That
synthesis is exactly the work a busy human wants to avoid. The information exists,
but it is **scattered and terse**, optimized for an agent reconstructing state,
not for a human catching up in thirty seconds.

The wish is to be able to say instead: *"it's all in the travel diary — last
entry, short read, you're welcome."*

## Framing

This is a **navigational / ergonomic** gap, not a content gap — a close cousin of
the gap idea 0009 (→ ADR-0017, tags) diagnosed, but on a different axis:

- `overview.md` is **derived, terse, machine-facing, state-oriented** — a table of
  `name / date / state`. It deliberately carries *no synthesis* (ADR-0011).
- What a catching-up human wants is the **opposite**: an **authored, prose,
  human-facing, narrative** account — "where were we, and where were we headed" —
  that can be *skimmed*, newest entry first.

So the missing thing is not more truth (the artifacts hold it) but a **friendly
narration layer** over the trail: an informal, growing logbook that touches no
idea, decision, or plan and never becomes a source of truth — just a warm,
skimmable entry point for humans.

## Prior art (Borrow, don't invent #8)

This is not hypothetical: the concept is already implemented and in use in the
sibling repo **josyn-builder** as a single self-describing file,
`docs/travel-diary.md`, plus a one-paragraph pointer in that repo's agent
instructions. There it is framed as *"outside the method."* Promoting it here
would make it a **shipped, optional companion of the method** — the human-facing
counterpart to the machine-facing `overview.md`.

## Candidate shape

- **One growing prose file** (`travel-diary.md`), newest entry first, each entry
  dated `## [YYYY-MM-DD]` (same-day entries disambiguated `-(2)`, `-(3)`, …).
- Each entry covers roughly **where we are / what we achieved / what is left /
  what is next**, optionally closing with a short **continuation brief** linking
  the relevant plan or ADR.
- **Light-weight to maintain**: adding a chapter is an informal task — *no
  confirmation guard, no ADR, no plan* — because it touches nothing authoritative.
- **Self-describing**: the file carries its own short "agent instructions" header,
  so the mechanism travels with the artifact.
- **Optional and safe to ignore**: a repo that doesn't want one simply has none,
  like the optional `Tags:` axis.

## Open questions

- Is the diary genuinely *outside* the method (as in josyn-builder) or a
  *shipped companion of* the method once decision-trail adopts it?
- Does its authored, drifting nature clash with the method's "derived, never
  hand-patched" instinct (ADR-0011) — or is it fine precisely because it is
  explicitly *not* a source of truth?
- Should decision-trail's own home repo dogfood a live diary, or ship only the
  mechanism + a starter template (as tags did)?
- How light should "add a chapter" be — truly guard-free?
