# 3. Rename the-way to decision-trail

- Status: done
- Date: 2026-06-28
- Implements: [ADR-0013](../decisions/0013-rename-the-way-to-decision-trail.md)

## How

ADR-0013 is the spec: the method is renamed **the-way → decision-trail**, and the
citation string becomes `Based on decision-trail vX.Y`.

Guiding principle for *what* to change: **rename live, forward-facing surfaces;
leave history intact.** Past ideas, ADRs, and plans are dated records that
referred to the method by the name it had at the time — they are not rewritten
(the same reason amended/superseded ADRs are never edited away). So construction
ADRs 0001–0012, ideas 0001–0004, and plans 0001–0002 keep their "the-way" text.
Idea 0005 and ADR-0013 also keep it deliberately — they *are* the record of the
old name. Only the live method surfaces and the provenance string move.

## Tasks

### Live method text
- [x] `AGENTS.md` — rename the method throughout (title, prose, "work the-way"
      → "work decision-trail" / "the method"); keep references that point at
      historical ADRs accurate.
- [x] `README.md` — rename the method in all forward-facing prose.
- [x] `.github/copilot-instructions.md` — update the pointer prose to the new
      name.
- [x] `overview.md` — update the descriptive prose (not the artifact rows).

### Starter skeleton (what adopters copy)
- [x] `starter/docs/working-method.md` — rename the method; update the citation
      to `Based on decision-trail vX.Y`.
- [x] `starter/AGENTS.md` — rename in the `## How we work` pointer.
- [x] `starter/docs/overview.md` — update prose.
- [x] `starter/docs/decisions/0001-adopt-the-way.md` — rename the seed adoption
      ADR (file + body) to `0001-adopt-decision-trail.md`; it cites the new name
      and version.

### Provenance & release
- [x] Decide the version number for the rename and add the `CHANGELOG.md` entry
      (a rename of the citation string is adopter-visible → favour a **major**
      bump, e.g. `2.0.0`).
- [x] Cut the semver git tag for that version.

### Repository
- [x] Rename the GitHub repo `ckluth/the-way` → `ckluth/decision-trail`
      (`gh repo rename`) and update the local `origin` remote.

### Close-out
- [x] Regenerate `overview.md` and re-stamp the date (ADR-0013 already accepted;
      this plan moves `draft → active → done`).

## Open question

- The repo rename and tag are real-world side effects; confirm with the user
  before executing those two tasks even after the plan is approved.
