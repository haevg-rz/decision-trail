# 8. Adopt the-way via a copied starter skeleton; version this repo as the standard

- Status: accepted
- Date: 2026-06-28
- Implements idea: [ideas/0002](../ideas/0002-adopting-the-way-in-other-repos.md)

## Context

Real projects must not live in this repository (idea 0002). Each project needs
its own repo with its own `the-way` artifacts and its own ADR log from 0001,
while this repo plays the role of the **standard**. We must decide how a new
project repo adopts the-way.

Three delivery mechanisms were considered, and one cross-cutting choice (copy vs
reference the method text). The promises that constrain the choice:

- **Genericity** (#7): the skeleton must be project-agnostic — no my-second-brain
  or "two shifts" origin story baked in.
- **Transparency & Continuity** (#1, #3): an adopting repo should be
  self-contained and readable offline; it should not break if this repo moves.
- **Economy & Borrow** (#2, #8): prefer the lightest mechanism that reuses an
  existing standard over bespoke tooling.
- **Agility** (#5): the method is "settled (not frozen)"; adopters must be able
  to say *which version* they took.

### Considered options

- **GitHub template repository** — native "Use this template" button. Zero
  tooling, but needs a *clean* skeleton repo separate from this development repo.
- **A `starter/` folder copied by hand** — a skeleton kept inside this repo that
  an adopter copies into a fresh repo. Cheapest to create and maintain now; can
  be promoted to a template repo later.
- **copier / cookiecutter template** — a scaffolding tool generates the
  structure. Powerful, but adds a tooling dependency to a plain-markdown method.

### Decision drivers

Self-containedness and low tooling win. Referencing this repo at runtime would
make every adopter depend on it staying put, violating Continuity (#1).

## Decision

We adopt the-way into other repos via a **copied starter skeleton**, and we treat
this repository as the **versioned standard**.

- **This repo is the standard.** It is versioned with git tags following semver
  (first release `v1.0.0`) and a short `CHANGELOG`. Improvements to the method
  ("not frozen") land as new ADRs here and are released as new versions.
- **A top-level `starter/` directory** holds a clean, project-agnostic skeleton:
  - a self-contained `AGENTS.md` carrying the generic method text (contract,
    lifecycle, layout, conventions, how-to-work) **without** this repo's origin
    narrative, plus a citation line *"Based on the-way vX.Y — <repo URL>"*;
  - empty `ideas/`, `decisions/`, `plans/` directories (kept with `.gitkeep`);
  - a seed `decisions/0001-adopt-the-way.md` recording the project's own first
    decision: to adopt the-way at a stated version.
- **Adopting = copying** the contents of `starter/` into a fresh repo. The new
  repo then owns its artifacts and its ADR log from 0001 onward and never
  inherits this repo's construction ADRs (0001–0007).
- **Copy, not reference:** the method text is copied so each project is
  self-contained and offline-readable (Transparency #3, Continuity #1), with the
  version citation making the provenance explicit.
- **Future option (not now):** promote `starter/` to a dedicated GitHub *template
  repository* for a one-click "Use this template" flow. Recorded here as the
  intended next step, deferred to keep one repo for now (Economy #2).

## Consequences

- A clean separation appears: this repo = the method's standard and construction
  history; each project repo = its own application of the method. The two never
  mix ADR logs.
- The `starter/` skeleton introduces a second, generic `AGENTS.md` alongside this
  repo's canonical one. The two share the method core and must be kept in step
  when the method changes; versioning + CHANGELOG make that drift visible and
  intentional.
- Choosing copy-over-reference costs adopters a manual re-copy to take a newer
  version, but buys self-containedness — the right trade for promises #1 and #3.
- This is the first ADR that defines a deliverable *for adopters* rather than a
  mechanic of the method itself; it turns the-way from a self-contained concept
  into something reusable across repos (Genericity #7).
