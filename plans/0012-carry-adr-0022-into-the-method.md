# Plan: carry ADR-0022 into the method — copy-driven update, `starter/`-derived manifest, in-repo pointer, conformance check

Date: 2026-07-04
Status: done
Implements: [ADR-0022](../decisions/0022-every-release-ships-reliable-update-instructions.md)

## Goal

Make "bring me current" reliable for older adopters, as decided in ADR-0022. Turn
the update path from note-driven (replace two files) into a **copy-driven**
procedure anchored on a **`starter/`-derived method-owned set + preserve rule**,
carried by a **stable in-repo pointer** every version ships, and closed by a
**lightweight conformance check** delivered as pure agent do-guidance. No tool
ships (faithful to ADR-0021 Option D).

## Design notes (placement)

- **The update procedure is adopter-facing guidance about the standard**, so the
  rewrite lands in this repo's top-level `adopting.md` (§3 Update), not in the
  method spec. The method spec's only job is to make that guidance *discoverable*
  from within an adopter via the in-repo pointer.
- **The in-repo pointer must ride in the copied method text** so it persists into
  every adopter: it lives in `starter/docs/working-method.md` (near the provenance
  citation) and therefore in each adopter's `docs/working-method.md` after an
  update. A forward pointer was first added in v2.6; ADR-0022 makes it a durable
  guarantee — confirm/strengthen its wording, don't duplicate it.
- **The method-owned set is not a hand-maintained manifest.** `starter/`'s own
  contents are the source of truth; `adopting.md` states the *preserve rule* (copy
  method text/templates, never overwrite project content) rather than listing paths
  that could drift.
- **ADR-0022 amends part of ADR-0021** (the note-driven update step becomes
  copy-driven; the migration contract's scope is clarified). Record the reciprocal
  amend cross-links so the decision log stays navigable (ADR-0012 vocabulary).

## Tasks

### Decision cross-links (ADR hygiene)
- [x] Add `Amends: [ADR-0021](0021-a-single-adopter-on-ramp-fresh-inject-update.md)`
      to ADR-0022's header, and the reciprocal
      `Amended by: [ADR-0022](0022-every-release-ships-reliable-update-instructions.md)`
      to ADR-0021's header (ADR-0022 changes ADR-0021's update-path step and
      refines the migration-contract scope).

### Rewrite the update path (`adopting.md` §3)
- [x] Replace the note-driven step 2 ("overwrite `working-method.md` + `guide.md`")
      with the **copy-driven procedure**: re-copy the **method-owned set** from the
      target version's `starter/` (mapped to the adopter's `docs/` locations),
      overwriting those files.
- [x] State the **preserve rule** explicitly: never overwrite project-owned content
      — the artifact families (`docs/decisions/`, `docs/ideas/`, `docs/plans/`), a
      populated `docs/travel-diary.md`, `docs/intermediate-artifacts/`, and
      `docs/overview.md`. Rule of thumb: **copy method text/templates, preserve
      project content.** Note that additive scaffolds (travel diary,
      intermediate-artifacts) therefore arrive automatically via the copy.
- [x] Keep the remaining steps in the new order: bump the `Based on decision-trail
      vX.Y` citation in **both** `docs/working-method.md` and the `## How we work`
      block of `AGENTS.md`; apply each release's non-"none" `Adopter migration:`
      steps in version order; regenerate `docs/overview.md`; run the conformance
      check; record the bump ADR; commit.

### Conformance check (agent do-guidance)
- [x] Add a **"Conformance check"** section to `adopting.md` (and reference it as
      the closing step of §3 Update): verify that every idea/decision/plan carries
      the mandatory `Date:` header; `overview.md` is in sync with the artifact
      headers; and the `Based on decision-trail vX.Y` citation matches in **both**
      `docs/working-method.md` and the `AGENTS.md` `## How we work` block. Pure
      do-guidance — **no tool ships** (ADR-0021 Option D).
- [x] Add a bullet to this repo's **`AGENTS.md` → Agent operating guidance** noting
      the conformance check as a do-guidance step available after any update or on
      request.

### Stable in-repo pointer
- [x] Confirm/strengthen the forward pointer near the provenance citation in
      `starter/docs/working-method.md` so every copied version carries a durable
      pointer to the standard repo's `adopting.md` (the update on-ramp). If wording
      is already sufficient (v2.6), make it explicit that this pointer is a
      guaranteed, version-carried anchor; regenerate this repo's `AGENTS.md` derived
      method body only if the shared spec text changed.

### Refine the release-migration contract wording
- [x] Clarify, in `CHANGELOG.md`'s intro **release-author rule**, that
      `Adopter migration:` states **only required behavioral changes** an adopter
      must perform (still "none" when apt) — new optional scaffolds are **not**
      enumerated there; they arrive via the copy-driven "bring me current"
      procedure. Mirror the clarification in this repo's `AGENTS.md` release-author
      guidance bullet (ADR-0021 reference).

### Release
- [x] Add a **`[2.7.0]`** entry to `CHANGELOG.md` (Added: ADR-0022 — copy-driven
      "bring me current", `starter/`-derived manifest + preserve rule, stable
      in-repo pointer, conformance check; Changed: `adopting.md` §3 rewritten,
      release-author rule wording clarified). Include its own **`Adopter
      migration:`** line — likely *"none — additive; adopter-facing update guidance
      only. Optionally re-run the new conformance check."*

### Overview
- [x] Regenerate `overview.md` to include this plan and reflect final states
      (idea 0013 → promoted, ADR-0022 → accepted, ADR-0021 → amended-by note);
      restamp "as of".

## Out of scope

- **Any adoption/conformance tool or script** — the conformance check ships as pure
  do-guidance; a give-away script stays a deferred, non-method option (ADR-0021
  Option D, ADR-0008).
- **Changing the eight-promise contract or the lifecycle** — this plan touches the
  onboarding/update machinery and the discoverability pointer only, not the method
  spec's core.
- **Editing accepted decisions away** — ADR-0021 is amended via cross-links and
  refined contract *wording*, not rewritten; the ADRs stay append-only.
- **A GitHub-template `starter/`** — deferred (ADR-0008).

