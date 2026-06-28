# 9. Adopters use conventional, unbranded locations — no `the-way/` folder

- Status: accepted
- Date: 2026-06-28
- Amends: ADR-0005 (drops the `the-way/` nesting), ADR-0008 (restructures the starter)
- Amended by: ADR-0010 (relocates the method body to `docs/working-method.md`; pins the merge text)

## Context

Two earlier ADRs left adoption ambiguous and, worse, branded:

- **ADR-0005** said that when the method is adopted into a host project, the
  families nest under a single physical `the-way/` subfolder to avoid colliding
  with the host's own folders.
- **ADR-0008**'s starter instead copied its contents to the repository *root*,
  never reconciling with ADR-0005, and never addressing an existing repo that
  already has its own root `AGENTS.md`.

Beyond the inconsistency, the `the-way/` subfolder is a problem in itself. A
directory named `the-way/` dropped into a colleague's repository reads as a
*proprietary harness with an awkward name* — it invites the question "what is
this?". That directly violates two promises:

- **Borrow, don't invent** (#8), whose whole point is to *guard against building
  a proprietary harness*.
- **Genericity** (#7): the method should leave no project-specific or
  brand-specific footprint.

The name "the-way" is fine as the *name of the method*; it must not be imposed as
a *directory* inside adopting repositories.

## Decision

When a project adopts the-way, its artifacts use **conventional, self-descriptive
locations**. There is no `the-way/` folder.

- **Decisions (ADRs) live in `docs/decisions/`** — the established MADR location
  for Architecture Decision Records. A reader recognizes it on sight.
- **Ideas live in `docs/ideas/`, plans in `docs/plans/`** — only the stages a
  project actually uses need exist.
- `docs/` is the universally-understood umbrella that prevents collisions with
  the host project's own folders, replacing ADR-0005's `the-way/` nesting.
- **The working-method description lives in the repository's root `AGENTS.md`** —
  a conventional, unbranded *filename* that agents read automatically. It carries
  a one-line provenance note, *"Based on the-way vX.Y"*, the way a file cites
  "Keep a Changelog". If the repo already has an `AGENTS.md`, the adopter
  **merges** a short "How we work" pointer into it rather than adding a second
  file.
- This removes the need for any "dedicated repo vs existing repo" distinction:
  there is one way to adopt. Copy the starter into the repository root; `docs/`
  merges cleanly with anything already there, and the only file that may need
  hand-merging is `AGENTS.md`.

## Consequences

- From the outside, an adopting repository simply looks well-organized — standard
  ADRs under `docs/decisions/`. The name "the-way" survives only as the method's
  name and a provenance citation, never as an imposed directory (Genericity #7,
  Borrow #8).
- The `starter/` skeleton in this repo is restructured to mirror the target
  shape: `AGENTS.md` plus `docs/ideas/`, `docs/decisions/`, `docs/plans/`.
- ADR-0005's layout still holds for *this* repository — the method's own home,
  where the families sit at the repo root. Only the *adoption* guidance changes:
  adopters use `docs/`, not a copy of this repo's root-level layout.
- This is a post-v1.0.0 refinement; it ships in the next version (see
  `CHANGELOG.md`).
