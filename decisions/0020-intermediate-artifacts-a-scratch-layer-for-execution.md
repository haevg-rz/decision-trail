# ADR-0020: Intermediate artifacts — a scratch persistence layer for execution

- Date: 2026-07-03
- Status: accepted
- Promoted from: [Idea-0013](../ideas/0013-intermediate-artifacts-a-scratch-layer-for-execution.md)

## Context

Idea 0013 diagnosed a **working-material** gap at the execution stage. Ticking a
plan's checkboxes is not always a clean walk down a list: sometimes a step must
first **gather information** — pull data together, extract or transcribe findings,
capture intermediate outputs — and then *work on that material later*, across
steps or across sessions.

decision-trail has nowhere obvious to park that material. All three artifact
families are **authoritative**: `ideas/` hold thoughts, `decisions/` hold ADRs,
`plans/` hold the task list and its execution state. None is meant to be a dumping
ground for work-in-progress data. So today the gathered material either leaks into
a plan (polluting an authoritative artifact with scratch content), lives only in
the agent's ephemeral context (lost at session end — a Continuity #1 failure), or
is improvised somewhere different every time.

The concept is not hypothetical. It is already implemented and working in the
adopting repo **josyn-builder**, which introduced an informal `intermediate-artifacts/`
folder during plan execution and reports it works well. This ADR promotes that
proven local convention into decision-trail itself.

This is a close cousin of the travel diary (idea 0010 → ADR-0018): both are
informal companions that sit *outside* the idea/decision/plan lifecycle, are
explicitly **not a source of truth**, may drift or go stale harmlessly, are
optional and safe to ignore, and were proven first in josyn-builder before
promotion (Borrow, don't invent #8). They differ in audience and shape: the diary
is a *single human-facing prose file* with a fixed entry shape; intermediate
artifacts are an *agent-facing folder of heterogeneous, ad-hoc files* whose
internal structure is deliberately **unstructured** — that informality is the whole
point.

## Decision drivers

- **Continuity (#1):** let plan execution pause and resume cheaply, with gathered
  material surviving a break rather than dying with the session's context.
- **Economy (#2):** add as little as possible — one conventional folder, no new
  lifecycle, no new cross-link fields, no bookkeeping.
- **Transparency (#3):** plain files in a plainly-named folder; nothing hidden.
- **Genericity (#7):** the need ("execution sometimes needs a scratch persistence
  layer") is generic, not project-specific; the method ships the mechanism, not the
  contents.
- **Borrow, don't invent (#8):** lift a concept already proven in josyn-builder,
  and reuse the companion pattern already established for the travel diary.
- **Do not corrupt the source of truth (ADR-0011):** intermediate artifacts must
  never become authoritative. They are disposable working material that drifts by
  design — acceptable only because they are explicitly **not** a source of truth
  and take no place in the lifecycle.

## Considered options

1. **Guide-only tip — a "how to work successfully" paragraph.** Cheapest; keeps the
   method minimal. Rejected: it leaves the concept **unnamed and unlocated**, so
   every adopter reinvents where scratch data lives — and the material risks leaking
   into `plans/` or being treated as authoritative. The whole value is the opposite:
   a name, a conventional home, and an explicit "not a source of truth" stamp.
2. **An explicit, optional, informal companion (chosen).** Mirror the travel-diary
   pattern: name it, locate it, declare it non-authoritative and outside the
   lifecycle, keep it guard-free. Closes the gap at minimal cost.
3. **A new authoritative artifact family (a fourth lifecycle stage).** Rejected as
   over-engineering: heavy, and it would compete with plans/ADRs for source-of-truth
   status. The concept's whole value is being *lightweight and non-authoritative*.
4. **Extend the plan artifact to hold gathered material inline.** Rejected: it
   pollutes an authoritative artifact with drifting scratch content — the same
   disease the derived overview was designed to cure (ADR-0011).

### Naming: collision with "artifact"

The method already calls ideas/decisions/plans "artifacts," so "intermediate
artifacts" risks confusion with the authoritative ones. Renaming (e.g. "working
notes" / "scratch") was considered and rejected: the name is **proven in
josyn-builder**, and the collision is neutralized by the explicit, repeated framing
that intermediate artifacts are **not a source of truth** and sit outside the
lifecycle. Keeping the proven name honors Borrow, don't invent (#8).

## Decision

Introduce **intermediate artifacts** as an optional, informal companion of
decision-trail's **execution stage**.

- **A conventional folder, `intermediate-artifacts/`.** Repo root here;
  `docs/`-prefixed in adopters (mirroring the layout split of ADR-0009). It is a
  scratch persistence layer for material gathered while executing a plan.
- **Not a source of truth.** The ideas, decisions, and plans remain the only source
  of truth. Intermediate artifacts hold non-authoritative working material; they may
  drift, go stale, or be deleted, and that is fine because nothing authoritative
  depends on them. They take no place in the idea → proposal → decision → plan →
  execution lifecycle and carry no cross-link fields.
- **Internally unstructured.** The method defines only *where* the folder lives and
  *what it is not*; the shape and organization of its contents are entirely the
  project's business. (A repo may, for example, keep one subfolder per plan — but
  this is a non-normative example, not a rule.)
- **Guard-free.** Creating, populating, and removing intermediate artifacts touches
  nothing authoritative, so it needs **no ADR, no plan, and no confirmation guard** —
  the same deliberate, narrowly-scoped exception granted to the travel diary
  (ADR-0018). All authoritative work keeps the guard.
- **Optional forward-only pointer.** A plan *may* carry an informal prose mention
  like "execution parked material in `intermediate-artifacts/…`" for findability.
  This is a plain prose note, **not** a formal cross-link field — it stays out of the
  greppable `Implements:` / `Promoted` / `Amends` vocabulary — and it has **no**
  reciprocal back-link and imposes no bookkeeping.
- **Committed by default, per-repo choice.** By default intermediate artifacts are
  **committed** to git, so gathered material survives across machines and sessions
  (Continuity #1). A repo that prefers purely-local scratch may gitignore the folder
  instead. The method states the default and leaves the switch to the adopter.
- **Left to rot harmlessly.** Once a plan is `done`, its intermediate artifacts are
  simply left in place — like a stale diary entry, nothing depends on them. A repo
  may prune them if it wishes, but the method requires no cleanup.
- **Optional and safe to ignore.** Like the travel diary and the `Tags:` axis, a
  repo that does not need intermediate artifacts simply has none.
- **The method ships the mechanism documented-but-empty.** The `starter/` skeleton
  carries an `docs/intermediate-artifacts/` folder with a short `README` explaining
  its purpose (and no fabricated contents) — like the empty `Tags:` vocabulary
  (ADR-0017), because the contents are project-specific.

The method spec (`starter/docs/working-method.md`, rendered per ADR-0014) documents
this in a short **Intermediate artifacts** section and adds the folder to the
layout. The agent operating guidance notes the guard-free nature of creating and
using them.

This is additive and safe to ignore: a repo with no intermediate artifacts behaves
exactly as today, and nothing in the lifecycle, overview, or cross-link vocabulary
changes.

## Consequences

- The working-material gap from idea 0013 is closed: plan execution gains a cheap,
  conventional persistence layer, so gathered material survives a break instead of
  dying with the session's context (Continuity #1, Economy #2).
- Intermediate artifacts are the **execution-stage companion**, alongside the
  human-facing travel diary and the machine-facing `overview.md` — three optional
  companions, each outside the lifecycle, none a source of truth.
- The source of truth is untouched (ADR-0011): intermediate artifacts are explicitly
  non-authoritative, so their drift is harmless. Plans stay clean of scratch content.
- The lifecycle, artifact families, and cross-link vocabulary are unchanged; the
  optional pointer from a plan is informal prose, not a formal link.
- The confirmation-guard exception is widened by one more narrowly-scoped case
  (creating/using intermediate artifacts), justified by their lack of authority. All
  authoritative work keeps the guard.
- The `starter/` skeleton gains an `docs/intermediate-artifacts/` folder with a
  purpose `README`; adopters get a ready-made home for scratch material.
- On acceptance, a plan will: add the **Intermediate artifacts** section and layout
  entry to `starter/docs/working-method.md` (bumping the provenance citation);
  regenerate this repo's `AGENTS.md` method body and add a guard-free note to the
  agent guidance (mirrored in `starter/AGENTS.md`); add a one-line mention to both
  `guide.md` renderings; ship the `starter/docs/intermediate-artifacts/README`;
  optionally seed this home repo's own `intermediate-artifacts/` folder; add a
  CHANGELOG entry; and regenerate `overview.md`.
