# ADR-0023: Promote and teach the method — a didactical guide

- Date: 2026-07-05
- Status: accepted
- Promoted from: [Idea-0015](../ideas/0015-promote-and-teach-the-method.md)

## Context

The method is settled and usable, but it is barely *taught*. Idea 0015 diagnosed
the gap: `guide.md` exists as a *narrative introduction*, yet it is not genuinely
**educational and didactical**. It explains what the method *is* more than it
teaches a newcomer how to *learn and adopt* it — there is no gentle on-ramp, no
worked example, no motivation-before-mechanics, no progressive build-up from a
first idea to a full lifecycle.

Two threads followed from that diagnosis: **promote & teach** — make the method
something a newcomer can *learn*, not just *reference* — and a **German
translation** to reach a German-speaking audience. A first machine-drafted
translation proved clumsy and uninspiring, and refining it was judged not worth the
cost, so the **translation thread is dropped**; this ADR settles only the
teaching-material thread. (Because this decision was revised in place while still
uncommitted, the translation thread leaves no trace in the permanent record.)

This ADR settles the design questions idea 0015 left open for the teaching material
(structure, worked example, and which renderings are affected) so a plan can carry
them into action. It touches only the *documentation companion* `guide.md`. It
changes **nothing** in the contract, the lifecycle, the artifact families, the
cross-link vocabulary, or `overview.md`; those remain exactly as decided.

The repo already has two parallel guide renderings (per ADR-0014's derived-rendering
pattern): this home repo's `guide.md` and `starter/docs/guide.md`, the copy an
adopter takes. Idea 0006 → ADR-0014 also established the relevant audience split
(agent guidance vs. human manual) and the "one canonical source, derived
renderings" discipline this ADR builds on.

## Decision drivers

- **Economy (#2) / Continuity (#1):** a method that is hard to learn is expensive to
  adopt; good teaching lowers the cost of the *first* pick-up, which is the most
  expensive one.
- **Transparency (#3):** teaching material stays plain, human-readable markdown —
  nothing hidden in a tool or a slide deck.
- **Genericity (#7):** the tutorial teaches with a *generic* worked example bound to
  no real project.
- **Borrow, don't invent (#8):** lean on ordinary tutorial pedagogy
  (motivate → show → build up progressively). Visualize with **Mermaid** — an
  existing plain-text diagram standard that renders natively on GitHub — rather
  than inventing a diagram format or shipping binary images.
- **Do not corrupt the source of truth (ADR-0011):** the guide is *documentation*,
  not an authoritative artifact; the ideas, decisions, and plans remain the only
  source of truth.

## Considered options

The questions from idea 0015 (teaching-material thread), and the option chosen for
each:

### 1. Where does the teaching content live?

1. **Rework `guide.md` in place into the didactical tutorial (chosen).** Keeps a
   single human-facing entry point; no new file competing with the guide.
2. Add a separate tutorial/onboarding artifact alongside `guide.md`. Rejected: two
   overlapping human intros invite drift and dilute the "read this first" pointer.
3. Keep `guide.md` as-is and add a short "start here" companion. Rejected: leaves the
   actual didactical gap in `guide.md` unfixed.

### 2. What is the canonical worked example?

1. **A tiny generic project — "add dark mode to a small app" — walked idea → ADR →
   plan → execution (chosen).** Concrete enough to feel real, generic enough to bind
   to no domain (Genericity #7), small enough to show the *whole* lifecycle without
   drowning the reader.
2. decision-trail's own construction (this repo's real artifacts). Rejected as the
   *primary* teaching vehicle: it is self-referential and heavier than a newcomer
   needs (the real ADRs stay available as further reading).
3. An abstract placeholder example (Idea A → Decision A → Plan A). Rejected: too
   bloodless to teach *why* each stage earns its place.

### 3. Which renderings does the didactical rework touch?

The didactical rework applies to **both** guide renderings — this repo's `guide.md`
**and** `starter/docs/guide.md` — because adopters deserve the same teaching (an
adopter's first read is the starter copy) (Genericity #7).

## Decision

Rework the guide into a **didactical tutorial**.

- **Rework `guide.md` into a didactical tutorial, in both renderings** (this repo's
  `guide.md` and `starter/docs/guide.md`). The reworked guide:
  - **motivates the problem before the mechanics** — why continuity/economy/
    transparency hurt without the method, before naming the eight promises;
  - **introduces the lifecycle progressively** — one stage at a time
    (idea → proposal → decision → plan → execution), each earned before the next;
  - **walks one canonical worked example end to end** — *"add dark mode to a small
    app"* — from a first captured idea, to a proposal/ADR, to an accepted decision,
    to a plan, to ticking execution checkboxes;
  - **visualizes the mechanics with Mermaid diagrams where they earn their place** —
    e.g. a state/flow diagram of the lifecycle (idea → proposal → decision → plan →
    execution) and a small diagram of the cross-link vocabulary — kept plain-text
    (Transparency #3), rendered inline by GitHub, and used only where a picture
    teaches faster than prose (no decorative diagrams);
  - stays a **guide** (human-facing narrative), keeping `AGENTS.md` /
    `working-method.md` as the terse reference; it does not absorb the reference.

A **German translation** was considered (idea 0015's second thread) but **dropped**:
a first machine-drafted `guide.de.md` was clumsy and uninspiring, and refining it to
the quality bar was judged not worth the cost. Translation may return as a future
idea, done properly.

This is additive and documentation-only. Nothing in the contract, lifecycle,
artifact families, cross-link vocabulary, or `overview.md` changes.

## Consequences

- The didactical gap from idea 0015 is closed: a newcomer reads a guide that
  motivates, shows a concrete end-to-end example, and builds the lifecycle up
  progressively — lowering the cost of the first adoption (Economy #2, Continuity
  #1).
- Adopters benefit too: `starter/docs/guide.md` gets the same didactical rework, so
  an adopter's first read teaches rather than merely describes (Genericity #7).
- The source of truth is untouched (ADR-0011): the guide is documentation;
  ideas/decisions/plans remain authoritative.
- On acceptance, a plan will: rework `guide.md` and `starter/docs/guide.md` into the
  didactical tutorial around the "dark mode" worked example, adding Mermaid diagrams
  for the lifecycle and cross-link vocabulary where they teach faster than prose; add
  a `CHANGELOG.md` entry (with an `Adopter migration:` line — the reworked starter
  guide reaches adopters via the copy-driven update, so required migration is
  "none"); and regenerate `overview.md`.
