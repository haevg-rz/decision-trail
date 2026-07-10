# Plan: ship the travel diary as an optional human-facing companion

- Date: 2026-07-03
- Status: done
- Implements: [ADR-0018](../decisions/0018-a-travel-diary-for-the-human-machine-interface.md)

## Goal

Ship the **travel diary** — one optional, self-describing prose file that narrates
the journey for humans, the human-facing counterpart to the machine-facing
`overview.md`. Ship the **mechanism + a starter template**; the home repo dogfoods
a **live** diary. The diary touches no idea, decision, or plan, sits outside the
lifecycle, and is maintained guard-free.

## Design notes (placement)

- The diary **mechanism** (what it is, entry format, guard-free maintenance) is
  generic method text → documented in `starter/docs/working-method.md` (canonical)
  and rendered into this repo's `AGENTS.md` per ADR-0014 (repo-root deltas).
- The **self-describing agent instructions** live in the diary file's own header,
  so the template carries its usage with it.
- The `starter/` skeleton ships a `docs/travel-diary.md` **template** (header +
  instructions, no fabricated entries). This home repo ships a **live**
  `travel-diary.md` with a first reconstructed entry (dogfooding).
- The guard-free "add a chapter" exception is noted in the **agent operating
  guidance** (this repo's `AGENTS.md` and `starter/AGENTS.md`).

## Tasks

### Method spec (canonical)
- [x] Add a **## Travel diary (optional companion)** section to
      `starter/docs/working-method.md`: one growing prose file, newest-first
      `## [YYYY-MM-DD]` entries (same-day `-(2)`, `-(3)`, …), covering where we are
      / achieved / left / next with an optional continuation brief; self-describing;
      maintained guard-free; **not a source of truth**; optional.
- [x] Add `docs/travel-diary.md` to the **Layout** block in
      `starter/docs/working-method.md`.
- [x] Bump the provenance citation to **v2.4** in `starter/docs/working-method.md`
      and `starter/AGENTS.md`.

### Starter template
- [x] Create `starter/docs/travel-diary.md` — the self-describing template: title,
      one-paragraph "what this is / not part of the source of truth" intro, an
      **## Agent instructions** block (prepend newest-first, date header + counter,
      the four beats, optional continuation brief), and no fabricated entries.

### Derived renderings (this repo)
- [x] Regenerate the derived method body in `AGENTS.md` (this repo) to include the
      **## Travel diary (optional companion)** section and the `travel-diary.md`
      layout entry — applying ADR-0014 repo-root deltas.
- [x] Add a guard-free "add a chapter to the travel diary" note to the **Agent
      operating guidance** in this repo's `AGENTS.md`, and mirror it in
      `starter/AGENTS.md`.

### Guides
- [x] Add a one-line mention of the travel diary (human-facing companion to the
      overview) near the overview section in `guide.md` and
      `starter/docs/guide.md`.

### Home-repo dogfood
- [x] Create this repo's live `travel-diary.md` (repo root) with the self-describing
      header and a first reconstructed entry covering the current state (v2.4 / the
      travel-diary feature just landed).

### Release
- [x] Add a `[2.4.0]` entry to `CHANGELOG.md` (Added: ADR-0018 — travel diary as an
      optional human-facing companion; minor/additive bump). Bump provenance to v2.4.

### Overview
- [x] Regenerate `overview.md` to include idea 0010, ADR-0018, and this plan;
      restamp "as of".

## Out of scope

- Any authoritative role for the diary — it never becomes a source of truth.
- A structured/machine-parsed diary format; entries stay free prose.
