# ADR-0018: A travel diary for the human-machine interface

- Date: 2026-07-03
- Status: accepted
- Promoted from: [Idea-0010](../ideas/0010-a-human-friendly-travel-diary.md)

## Context

Idea 0010 diagnosed a gap at the **human-machine interface**. decision-trail
already answers the machine-facing continuity questions with precision: after a
break an agent can reconstruct the exact state from `overview.md` (derived status
index), the active plan (precise continuation point), and the ADRs (reasoning).
The trail is complete and the source of truth is solid.

But when a *human* colleague asks "where are we? / what changed last session? /
what is left? / what is next?", the only honest answer today is "browse the repo
documents and synthesize" — precisely the work a busy human wants to skip. The
information exists but is scattered and terse, optimized for an agent
reconstructing state, not for a human catching up in thirty seconds.

The gap is **navigational / ergonomic**, not a content gap — a cousin of the tags
gap (idea 0009 → ADR-0017) on a different axis. `overview.md` is *derived, terse,
machine-facing, state-oriented* and deliberately carries no synthesis (ADR-0011).
What a catching-up human wants is the opposite: an *authored, prose, human-facing,
narrative* account, skimmable newest-first.

The concept is not hypothetical: it is already implemented and in use in the
sibling repo **josyn-builder** as a single self-describing file
(`docs/travel-diary.md`) plus a one-paragraph pointer in that repo's agent
instructions, where it is framed as *"outside the method."* This ADR promotes it
into decision-trail itself.

## Decision drivers

- **Continuity (#1) at the human layer:** let a human — not just an agent — pick
  up cheaply after a break, from a single short read.
- **Economy (#2):** add as little as possible — one optional prose file, no new
  lifecycle, no new cross-links, cheap to write and cheap to read.
- **Transparency (#3):** plain, human-readable markdown; nothing hidden.
- **Genericity (#7):** the diary narrates *any* project's journey; it ships as a
  mechanism + template, imposing no project-specific content.
- **Borrow, don't invent (#8):** lift a concept already proven in josyn-builder
  rather than inventing a new one.
- **Do not corrupt the source of truth (ADR-0011):** the diary must never become
  authoritative. It is authored prose that *drifts by design* — acceptable only
  because it is explicitly **not** a source of truth and touches no artifact.

## Considered options

1. **No diary — point humans at `overview.md` + the active plan.** Cheapest;
   changes nothing. Rejected: it leaves the real ergonomic gap open — `overview.md`
   is terse state, not a skimmable narrative, and synthesizing across artifacts is
   exactly the burden humans want lifted.
2. **A travel diary as a shipped, optional companion (chosen).** One
   self-describing prose file, informal to maintain, outside the artifact
   lifecycle. Closes the gap at minimal cost.
3. **Extend `overview.md` with a narrative section.** Rejected: it would pollute a
   *derived, never-authored* artifact (ADR-0011) with authored synthesis that
   drifts — reintroducing exactly the disease the derived overview cures.
4. **A new authoritative artifact family (a "session log" lifecycle).** Rejected
   as over-engineering: heavy, and it would compete with the plans/ADRs for
   source-of-truth status. The diary's whole value is being *lightweight and
   non-authoritative*.

### Inside or outside the method?

In josyn-builder the diary is framed as *"outside the method."* Adopting it here
resolves that tension by reframing: the diary becomes a **shipped, optional
companion of the method** — the human-facing counterpart to the machine-facing
`overview.md`. It is *part of what decision-trail ships*, yet it sits *outside the
idea/decision/plan lifecycle* and touches none of those artifacts. Both are true
and consistent: the method ships the mechanism; the diary itself carries no
authority.

## Decision

Introduce the **travel diary** as an optional, human-facing companion of
decision-trail.

- **One growing prose file, `travel-diary.md`.** It lives beside `overview.md`
  (repo root here; `docs/` in adopters). Newest entry first. Each entry is headed
  with the date in brackets — `## [YYYY-MM-DD]` — and same-day entries are
  disambiguated with a counter: `## [YYYY-MM-DD-(2)]`, `-(3)`, and so on.
- **Each entry** covers, in brief friendly prose: **where we are**, **what we
  achieved** (since the last entry), **what is left**, and **what is next** —
  optionally closing with a one- or two-sentence **continuation brief** that links
  the relevant plan or ADR.
- **Self-describing.** The file carries its own short "agent instructions" header,
  so the mechanism travels with the artifact and needs no external spec to use.
- **Light-weight to maintain — no confirmation guard.** When the user says *"add a
  chapter to the travel diary"* (or similar), the agent prepends a new dated
  section directly — **no ADR, no plan, no confirmation guard** — because the file
  touches nothing authoritative. This is a deliberate, explicit exception to the
  confirmation guard, justified by the diary carrying no authority.
- **Not a source of truth.** The ideas, decisions, and plans remain the only
  source of truth. The diary is prose narration over them; it may drift, and that
  is fine because nothing depends on it. It touches no idea, decision, or plan and
  sits outside the lifecycle and the cross-link vocabulary.
- **Optional and safe to ignore.** Like the `Tags:` axis, a repo that does not
  want a diary simply has none. The method ships the **mechanism + a starter
  template**; each repo decides whether to keep a live one.
- **The method ships a template; this home repo dogfoods a live diary.** The
  `starter/` skeleton carries a `docs/travel-diary.md` template (header + agent
  instructions, no fabricated entries). Unlike the `Tags:` vocabulary — which is
  project-specific content the home repo left empty (ADR-0017) — a diary is
  *generic prose narration*, so decision-trail's home repo keeps its **own live
  travel diary**, both as a real catch-up aid and as a worked example.

The method spec (`starter/docs/working-method.md`, rendered per ADR-0014)
documents the diary in a short **Travel diary** section and adds it to the layout.
The agent operating guidance notes the guard-free "add a chapter" task.

This is additive and safe to ignore: a repo with no diary behaves exactly as
today, and nothing in the lifecycle, overview, or cross-link vocabulary changes.

## Consequences

- The human-machine-interface gap from idea 0010 is closed: a colleague catching
  up reads the last diary entry — a short, friendly narrative — instead of
  synthesizing across `overview.md`, the active plan, and recent ADRs (Continuity
  #1, Economy #2).
- The diary is the **human-facing counterpart to `overview.md`**: overview is
  derived/terse/state; diary is authored/prose/narrative. Together they cover both
  audiences without either compromising the other.
- The source of truth is untouched (ADR-0011): the diary is explicitly *not*
  authoritative, so its drift is harmless. `overview.md` stays derived and
  synthesis-free.
- The lifecycle, artifact families, and cross-link vocabulary are unchanged; the
  diary is orthogonal to them and carries no `Implements:` / `Promoted` / `Amends`
  links.
- A deliberate exception to the **confirmation guard** is introduced, scoped
  narrowly to "add a chapter to the travel diary" and justified by the file's lack
  of authority. All authoritative work keeps the guard.
- decision-trail's home repo gains a live `travel-diary.md` (dogfooding), and the
  `starter/` skeleton gains a `docs/travel-diary.md` template.
- On acceptance, a plan will: add the **Travel diary** section and layout entry to
  `starter/docs/working-method.md` (bumping the provenance citation to v2.4); ship
  the `starter/docs/travel-diary.md` template; regenerate this repo's `AGENTS.md`
  method body and add the guard-free "add a chapter" note to the agent guidance
  (and mirror the note in `starter/AGENTS.md`); add a one-line mention to both
  `guide.md` renderings; create this repo's live `travel-diary.md` with a first
  reconstructed entry; add a `[2.4.0]` entry to `CHANGELOG.md`; and regenerate
  `overview.md`.
