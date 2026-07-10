# Plan: add the optional `Tags:` axis for cross-cutting navigation

- Date: 2026-07-03
- Status: done
- Implements: [ADR-0017](../decisions/0017-optional-tags-axis-for-cross-cutting-navigation.md)

## Goal

Add the optional `Tags:` header field and a derived `Tags` column to the method,
shipping only the **mechanism + governance rule** (recommended-but-not-enforced,
curated per repo) — **no content vocabulary**. The `starter/` skeleton carries an
empty "recommended tags" placeholder; this repo defines no vocabulary of its own
and applies no tags.

## Design notes (placement)

- The `Tags:` **mechanism and governance** are generic method text → live in
  `starter/docs/working-method.md` (canonical) and are rendered into this repo's
  `AGENTS.md` per ADR-0014 (repo-root deltas).
- A repo's **own recommended vocabulary** is project-specific content, kept in a
  clearly demarcated "Recommended tags for this repo" placeholder — empty in the
  `starter/` skeleton and empty in this repo.
- The `Tags` overview column is populated by the existing wholesale regeneration;
  the refresh procedure gains one extra header line to read (`Tags:`).

## Tasks

### Method spec (canonical)
- [x] In `starter/docs/working-method.md`, document the optional `Tags:` header
      field in the lifecycle section (alongside the mandatory `Date:` paragraph):
      comma-separated, optional, omitted when empty; applies to ideas, decisions,
      and plans.
- [x] Add a short **## Tags (optional)** section to `starter/docs/working-method.md`
      stating the governance rule — *recommended-but-not-enforced, curated per
      repo, off-list tags allowed, misuse has no structural consequence* — plus a
      demarcated empty **"Recommended tags for this repo:"** placeholder with the
      one-line instruction "list your project's recurring themes here."
- [x] Update the **Refresh procedure** in `starter/docs/working-method.md` to also
      read the `Tags:` header line and emit the new column.

### Overview column
- [x] Add a `Tags` column to the three tables in `starter/docs/overview.md`
      (template rows show an empty cell).
- [x] Add a `Tags` column to the three tables in this repo's `overview.md` and
      regenerate it (this repo's own tag cells are empty; stamp "as of" the date).

### Derived renderings (this repo)
- [x] Regenerate the derived method body in `AGENTS.md` (this repo) to include the
      `Tags:` field, the **## Tags (optional)** section, and the updated refresh
      procedure — applying the enumerated ADR-0014 deltas (repo-root paths, etc.).
      This repo's "Recommended tags" placeholder stays empty.
- [x] If `guide.md` and `starter/docs/guide.md` describe artifact headers or the
      overview, add a one-line mention that `Tags:` is an optional field; skip if
      they don't cover headers.

### Adopter entry point
- [x] Review `starter/AGENTS.md`; if its agent-guidance warrants it, add a brief
      note that a tag vocabulary is optional and curated per repo. Skip if the
      pointer to `working-method.md` already covers it. — *Skipped: the pointer to
      `working-method.md` (which now carries the Tags section) covers it.*

### Release
- [x] Add a `[2.3.0]` entry to `CHANGELOG.md` (Added: ADR-0017 — optional `Tags:`
      axis; mechanism only, vocabulary curated per repo; minor/additive bump).
      Also bumped the provenance citation to v2.3 in `starter/AGENTS.md` and
      `starter/docs/working-method.md`.

## Out of scope

- The filtered/by-tag view (deferred by ADR-0017; a future decision if pursued).
- Any content vocabulary in the method or in this repo.
