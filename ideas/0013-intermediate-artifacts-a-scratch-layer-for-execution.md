# Idea: intermediate artifacts — a scratch persistence layer for execution

- Date: 2026-07-03
- Status: promoted
- Promoted to: [ADR-0020](../decisions/0020-intermediate-artifacts-a-scratch-layer-for-execution.md)

## Observation

Executing a plan is not always a clean walk down a checklist. Sometimes ticking a
checkbox requires **gathering information first** — pulling data together,
extracting or transcribing findings, capturing intermediate outputs — and then
*working on that gathered material later*, across steps or even across sessions.

decision-trail today has nowhere obvious to park that material. The three artifact
families are all **authoritative**: `ideas/` hold thoughts, `decisions/` hold ADRs,
`plans/` hold the task list and its execution state. None of them is meant to be a
dumping ground for work-in-progress data. So the gathered material either leaks
into a plan (polluting an authoritative artifact with scratch content), lives only
in the agent's ephemeral context (lost at session end — a Continuity #1 failure),
or gets improvised somewhere different every time.

## Framing

This is a **working-material** gap, not a content or navigational gap. What is
missing is a *persistence layer for execution* — a place to stash gathered,
non-authoritative material so that plan execution can pause and resume cheaply.

Crucially, this is **not a fourth lifecycle family**. Intermediate artifacts are
not ideas, decisions, or plans; they carry no status, take no place in the
idea → proposal → decision → plan → execution flow, and hold no cross-links. They
are a **companion of the execution stage** — much as the travel diary
(idea 0010 → ADR-0018) is a companion sitting *outside* the lifecycle, and the
optional `Tags:` axis (idea 0009 → ADR-0017) is orthogonal to it.

The parallel to the travel diary is close and instructive:

- both are **informal** and **explicitly not a source of truth**;
- both may **drift / go stale harmlessly**, because nothing authoritative depends
  on them;
- both are **optional and safe to ignore** — a repo that doesn't need one has none;
- both were **proven first in the sibling repo josyn-builder** before being
  considered for promotion into the method (Borrow, don't invent #8).

The difference is audience and shape: the travel diary is a *single human-facing
prose file* with a fixed entry shape; intermediate artifacts are an
*agent-facing folder of heterogeneous, ad-hoc files* whose internal structure is
deliberately **unstructured** — that informality is the whole point.

## Prior art (Borrow, don't invent #8)

The concept is already implemented and working in the adopting repo
**josyn-builder**, which introduced an informal `intermediate-artifacts/` folder
during plan execution and reports it works well. Promoting it here would turn a
proven, recurring local convention into a **shipped, optional companion of the
method** — the execution-stage counterpart to the human-facing travel diary.

## Candidate shape

- **A conventional folder + name** (e.g. `intermediate-artifacts/`) — repo root
  here, `docs/`-prefixed in adopters, mirroring the layout split of ADR-0009.
- **Explicitly not a source of truth** — outside the lifecycle and the cross-link
  vocabulary; free to drift, free to delete, disposable by nature.
- **Guard-free** to create, populate, and remove, because it touches nothing
  authoritative (the same deliberate confirmation-guard exception granted to the
  travel diary in ADR-0018).
- **Internally unstructured** — the method defines only *where* it lives and *what
  it is not*; the shape of its contents is entirely the project's business.
- **Optional forward-only pointer** — a plan *may* note "execution parked material
  in `intermediate-artifacts/…`" for findability, but with **no** reciprocal
  bookkeeping.
- **Ship documented-but-empty in `starter/`** — like the `Tags:` vocabulary
  (ADR-0017), since the *contents* are project-specific; perhaps a short
  `README`/`.gitkeep` explaining the folder's purpose.
- **Gitignore-or-commit guidance** — the method should say whether intermediate
  artifacts are meant to be committed (durable across machines) or ignored
  (purely local scratch), or explicitly leave it to the adopter.

## Open questions

- **Guide-only vs explicit member?** Is naming + locating + "not a source of truth"
  enough value to justify a method member, or would a "how to work successfully"
  tip in the guide suffice? (Leaning: explicit member, matching the travel diary.)
- **Committed or ignored?** Are intermediate artifacts durable (committed, so they
  survive across machines/sessions) or ephemeral local scratch (gitignored)? Or is
  that per-repo?
- **Any structure at all, or none?** Should the method suggest even a light
  convention (e.g. one subfolder per plan), or is total informality the point?
- **Relationship to a plan.** Forward-only optional pointer, or nothing at all —
  does even an optional link risk dragging scratch material toward being treated as
  authoritative?
- **Lifespan / cleanup.** Once the plan is `done`, do its intermediate artifacts
  get pruned, archived, or left to rot harmlessly (like a stale diary entry)?
- **Naming.** Is "intermediate artifacts" the right name, given the method already
  calls ideas/decisions/plans "artifacts"? Could it be confused with them? (Would a
  name like "working notes" / "scratch" reduce collision with the authoritative
  "artifact" vocabulary?)
- **Scope creep.** Every new member dilutes the "settled, minimal" method — does
  this clear the bar (generic recurring need + proven in use + fits the existing
  companion pattern), as the diary and tags did?
