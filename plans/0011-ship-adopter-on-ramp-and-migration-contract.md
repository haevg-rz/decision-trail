# Plan: ship the adopter on-ramp (`adopting.md`) and the release-migration contract

- Date: 2026-07-03
- Status: done
- Implements: [ADR-0021](../decisions/0021-a-single-adopter-on-ramp-fresh-inject-update.md)

## Goal

Give decision-trail a single, discoverable **on-ramp** so using it in your own repo
is turnkey across all three scenarios — **fresh**, **inject**, **update** — and make
the **update** path safe by binding release authors to state each release's adopter
migration. Deliver this as **pure do-guidance** (ADR-0021, Option D). _No adoption
tool ships — see the note below._

## Design notes (placement)

- **`adopting.md` lives at this repo's root**, not in `starter/`. It is
  adopter-facing guidance *about the standard*; adopters reach it at the repo URL
  already in their provenance citation (`Based on decision-trail vX.Y — <url>`).
- **The release-migration contract is a release-author rule for this repo** (the
  standard), so it belongs with this repo's release discipline: documented in
  `CHANGELOG.md`'s intro and noted in this repo's `AGENTS.md` agent operating
  guidance. It is **not** method spec text, so `starter/docs/working-method.md`
  does not change for it.
- **Adopters must be able to find the update steps.** Add a short forward pointer
  from the starter's `working-method.md` (near the provenance line) to
  `<repo URL>/adopting.md`, so a copied repo knows where upgrade guidance lives.
- **No adoption tool ships (decided during execution).** A requirements pass found
  no adopter step that is hard, error-prone, *and* beyond "agent + copy-paste": the
  fresh/inject steps are trivial copies and edits, and the update migrations are
  written as agent-executable steps that the agentic precondition already covers.
  A copy/adopt script would duplicate trivial copying and cannot know future
  migrations, so it earns nothing. `adopting.md` explains this in a *"Why there's no
  adoption tool"* section instead.

## Tasks

### On-ramp document (this repo)
- [x] Create top-level **`adopting.md`** with a short intro (the two preconditions:
      a git repo; an agentic setup that understands `AGENTS.md`) and three
      step-by-step sections:
  - [x] **Fresh repo** — copy the contents of `starter/` into the new repo; it owns
        its artifacts and its ADR log from `0001-adopt-decision-trail.md`;
        `AGENTS.md` *is* the "How we work" pointer block (ADR-0008, ADR-0010).
  - [x] **Inject into an existing repo** — non-destructive drop-in: copy
        `starter/docs/` into `docs/` without touching existing files; create
        `AGENTS.md` from the pointer block or **append** it if one exists (exact
        wording from ADR-0010); seed `docs/decisions/0001-adopt-decision-trail.md`;
        pre-existing history/decisions coexist untouched, decision-trail's ADR log
        starts fresh at 0001 and never inherits this repo's construction ADRs.
  - [x] **Update `X.Y → X.Y+n`** — read the current version from the
        `Based on decision-trail vX.Y` citation (the anchor); replace
        `docs/working-method.md` and `docs/guide.md` with the target's copies and
        bump the citation; apply, in order, the `Adopter migration:` steps of each
        release between current and target (read from this repo's `CHANGELOG.md`).
- [x] In `adopting.md`, add a **"Why there's no adoption tool"** note explaining
      that the fresh/inject steps are trivial copies/edits and the update migrations
      are agent-executable, so a script earns nothing (the GitHub-template option
      stays deferred, ADR-0008).

### Release-migration contract
- [x] Document the contract in **`CHANGELOG.md`**'s intro: every release **must**
      carry an **`Adopter migration:`** line/heading — **even when "none"** — written
      as agent-executable steps.
- [x] Add a bullet to this repo's **`AGENTS.md` → Agent operating guidance**
      recording the release-author rule (and mirror the release-discipline note in
      `starter/AGENTS.md` only if it already carries release guidance; otherwise
      leave the starter untouched).
- [x] Add an **`Adopter migration:`** line to every past `CHANGELOG.md` entry
      (non-trivial ones get real steps; additive/behavioral ones state "none"), so
      the contract is complete across history.

### Adopter-facing pointer (starter)
- [x] Add a one-line forward pointer near the provenance citation in
      `starter/docs/working-method.md` (and mirror in `starter/AGENTS.md` if
      appropriate): *"To update or (re)adopt, see `adopting.md` at
      https://github.com/ckluth/decision-trail."* Bump the provenance citation to
      **v2.6** in `starter/docs/working-method.md` and `starter/AGENTS.md`.

### Adoption tooling (considered, then dropped)
- [x] Considered a `giveaway/` copy helper; **dropped after a requirements pass**
      (no adopter step is hard, error-prone, *and* beyond "agent + copy-paste").
      `adopting.md` documents *why there's no tool* instead.

### Guides
- [x] Add a one-line mention + link to `adopting.md` from this repo's `guide.md`
      (and from `starter/docs/guide.md` a pointer to the standard repo's
      `adopting.md` for updates), so the on-ramp is discoverable from the narrative
      intro.

### Release
- [x] Add a **`[2.6.0]`** entry to `CHANGELOG.md` (Added: ADR-0021 — adopter on-ramp
      `adopting.md` + release-migration contract; minor/additive bump), including its
      own **`Adopter migration:`** line (likely "none — additive; new guidance only").

### Overview
- [x] Regenerate `overview.md` to include this plan (and confirm idea 0004 →
      promoted, ADR-0021 → accepted); restamp "as of".

## Out of scope

- **Promoting `starter/` to a GitHub template repository** — recorded in ADR-0008 as
  a deferred future option; not part of this plan.
- **A full retroactive `Adopter migration:` backfill** was completed across the
  entire `CHANGELOG` history; the contract binds all releases going forward.
- **Any method-spec change** — `adopting.md` and the release contract are the
  standard repo's onboarding/release machinery, not the eight-promise contract or
  the lifecycle; `working-method.md` gains only a discoverability pointer.
- **Any adoption tool / script** — dropped during execution; adopting and updating
  are pure do-guidance the agent executes (ADR-0021, Option D). Promoting `starter/`
  to a GitHub template stays a deferred option (ADR-0008).

