# Plan: ship intermediate artifacts as an optional execution-stage companion

- Date: 2026-07-03
- Status: done
- Implements: [ADR-0020](../decisions/0020-intermediate-artifacts-a-scratch-layer-for-execution.md)

## Goal

Ship **intermediate artifacts** — an optional, informal `intermediate-artifacts/`
folder that gives plan execution a scratch persistence layer for gathered material.
It is the execution-stage counterpart to the human-facing travel diary: outside the
lifecycle, **not a source of truth**, guard-free to create/use/delete, internally
unstructured, committed by default (per-repo choice). Ship the **mechanism +
documented-but-empty starter folder**; the home repo may seed its own.

## Design notes (placement)

- The **mechanism** (what it is, where it lives, what it is *not*) is generic method
  text → documented in `starter/docs/working-method.md` (canonical) and rendered
  into this repo's `AGENTS.md` per ADR-0014 (repo-root deltas: `intermediate-artifacts/`
  at root here vs. `docs/intermediate-artifacts/` in adopters).
- The `starter/` skeleton ships `docs/intermediate-artifacts/README.md` explaining
  the folder's purpose (no fabricated contents), like the empty `Tags:` vocabulary.
- The guard-free nature is noted in the **agent operating guidance** (this repo's
  `AGENTS.md` and `starter/AGENTS.md`).

## Tasks

### Method spec (canonical)
- [x] Add a **## Intermediate artifacts (optional companion)** section to
      `starter/docs/working-method.md`: a scratch persistence layer for material
      gathered during plan execution; lives in `docs/intermediate-artifacts/`;
      **not a source of truth**; outside the lifecycle and cross-link vocabulary;
      internally unstructured; guard-free to create/use/delete; committed by default
      (repo may gitignore); a plan *may* carry an informal forward-only prose pointer
      (not a formal cross-link); left to rot harmlessly when a plan is done; optional.
- [x] Add `docs/intermediate-artifacts/` to the **Layout** block in
      `starter/docs/working-method.md`.
- [x] Bump the provenance citation to **v2.5** in `starter/docs/working-method.md`
      and `starter/AGENTS.md`.

### Starter skeleton
- [x] Create `starter/docs/intermediate-artifacts/README.md` — a short purpose note:
      what the folder is (scratch persistence for execution), what it is *not* (not a
      source of truth, outside the lifecycle), guard-free, committed by default, and
      that its internal shape is the project's business. No fabricated contents.

### Derived renderings (this repo)
- [x] Regenerate the derived method body in `AGENTS.md` (this repo) to include the
      **## Intermediate artifacts (optional companion)** section and the
      `intermediate-artifacts/` layout entry — applying ADR-0014 repo-root deltas.
- [x] Add a guard-free note about creating/using intermediate artifacts to the
      **Agent operating guidance** in this repo's `AGENTS.md`, and mirror it in
      `starter/AGENTS.md`.

### Guides
- [x] Add a one-line mention of intermediate artifacts (execution-stage companion,
      alongside the diary) near the relevant section in `guide.md` and
      `starter/docs/guide.md`.

### Home-repo dogfood (optional)
- [x] Optionally seed this repo's own `intermediate-artifacts/` folder with a
      `README.md` (same purpose note), so the home repo has a ready home.

### Release
- [x] Add a `[2.5.0]` entry to `CHANGELOG.md` (Added: ADR-0020 — intermediate
      artifacts as an optional execution-stage companion; minor/additive bump).

### Overview
- [x] Regenerate `overview.md` to include idea 0013, ADR-0020, and this plan;
      restamp "as of".

## Out of scope

- Any authoritative role for intermediate artifacts — they never become a source of
  truth, and no formal cross-link field is added.
- A prescribed internal structure — organization is left entirely to the project.
- Automatic cleanup/pruning — artifacts are left to rot harmlessly.
