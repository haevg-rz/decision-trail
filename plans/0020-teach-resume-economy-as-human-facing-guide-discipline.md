# Plan 0020: teach resume economy as a human-facing guide discipline

- Date: 2026-07-11
- Status: done
- Implements: [ADR-0030](../decisions/0030-resume-economy-as-a-human-facing-guide-discipline.md)

## Goal

Carry [ADR-0030](../decisions/0030-resume-economy-as-a-human-facing-guide-discipline.md)
into the method texts: add a short, **human-facing "resuming cheaply" section to
`guide.md`** (register A only, per ADR-0014) that names the discipline making
Economy (#2) real at resume time. Scope is strictly the **levers the human
controls** — how you re-open a session, naming the artifact not the topic, asking
narrow, investing at pause-time, and terseness as a write/approve discipline.
**Explicitly exclude** the agent-mechanic restatements (grep headers vs. bodies,
header-only `overview.md` regeneration): those are already owned by ADR-0011 /
idea 0008 and are cross-referenced, not repeated. This is **purely advisory** —
no mechanism, no new artifact family, no cross-link vocabulary, and **no change
to the always-loaded spec register** (`working-method.md` / `AGENTS.md`), whose
weight sibling ADR-0029 exists to shrink (option B rejected). Ship as a release
whose behavioral migration is **"none"** — the new guide prose reaches adopters
via the copy-driven "bring me current" update (ADR-0022).

## Tasks

- [x] **Author the section in `starter/docs/guide.md`.** Add a short "resuming
      cheaply" (or similarly named) narrative section carrying the five
      human-controlled levers from ADR-0030's Decision: (1) how you re-open the
      session is the biggest lever; (2) name the artifact, not the topic; (3) ask
      narrow; (4) invest at pause-time, not resume-time; (5) terseness is a human
      write/approve discipline. Keep it prose and human-facing — the register
      `guide.md` owns (ADR-0014).
- [x] **Cross-reference, don't restate.** In that section, point to the travel
      diary (ADR-0018) for pause-time catch-up and to `overview.md` /
      ADR-0011 / idea 0008 for the derived-index and header-only mechanics —
      instead of repeating the agent-facing mechanics, per ADR-0030's scope test.
- [x] **Mirror into the repo-root `guide.md`.** Add the same section to this
      repo's `guide.md`, keeping the two renderings in sync (ADR-0014), adjusting
      only what the home-repo/adopter delta requires (paths, provenance framing).
- [x] **Guard the spec register.** Confirm `starter/docs/working-method.md`, the
      repo-root `AGENTS.md` (derived body + `## Agent operating guidance`), and
      `starter/AGENTS.md` are **untouched** — ADR-0030 is advisory and must add
      no always-loaded weight (protecting ADR-0029's shrink). A diff check, not
      just intent.
- [x] **Provenance bump.** Bump the `Based on decision-trail vX.Y` citation to
      **v2.13** in `starter/AGENTS.md`, `starter/docs/working-method.md`, and
      `starter/docs/guide.md`.
- [x] **CHANGELOG + release.** Add a `## [2.13.0]` entry to `CHANGELOG.md`
      describing the new human-facing resume-economy guidance in `guide.md`
      (ADR-0030: advisory only, register A, human levers, agent mechanics
      cross-referenced not restated), with **`Adopter migration: none`** — the
      new guide prose reaches adopters via the copy-driven "bring me current"
      update (ADR-0022); no behavioral action required.
- [x] **Regenerate `overview.md`** after all edits, and set this plan's status
      `draft` → `active` → `done` as work proceeds (ADR-0030 already `accepted`,
      idea 0023 already `promoted`).

