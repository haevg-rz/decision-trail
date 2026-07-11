# Plan 0021: split the adopter update path — human intent + agent-facing `updating.agent.md`

- Date: 2026-07-11
- Status: done
- Implements: [ADR-0031](../decisions/0031-adopter-update-is-human-intent-agent-execution.md)

## Goal

Carry ADR-0031 into the repo: re-present the adopter **update path** around a clean
audience split. Move the copy-driven "bring me current" ritual (decided in
ADR-0022, mechanics unchanged) out of the human on-ramp and into a terse,
self-contained, tool-agnostic **`updating.agent.md`**; slim `adopting.md` chapter 3
to a plain-language human trigger (intent + explicit source + how-to pointer) that
runs as one transparent batch under the confirmation guard. No tool ships; a
conformance linter stays a deferred option.

## Design notes (placement)

- **`updating.agent.md` is standard-repo-only**, alongside `adopting.md` — it is the
  file an adopter's agent is *pointed at* (fetched from the source) during an
  update. It does **not** go in `starter/` and is **not** copied into adopters.
- **Single operational source of truth (ADR-0031 clause 4).** The executable steps
  — including the conformance check — live in `updating.agent.md`. `adopting.md`
  chapter 3 and the conformance section become intent + pointer, never a second
  copy of the steps. ADR-0022 stays the *why*.
- **Self-contained for bootstrap (ADR-0031 clause 1).** `updating.agent.md` must
  assume the running agent knows *nothing* about the update method beyond the prompt
  and the file itself, so an adopter on any older version can run it. The trigger
  carries the how-to pointer explicitly, closing the hen-and-egg.
- **ADR-0022 mechanics are unchanged** — this is relocation + re-presentation, not a
  rewrite of the copy-driven procedure, the preserve rule, or the conformance check.
- **Cross-link hygiene** — ADR-0031 `Amends` ADR-0022; the reciprocal `Amended by`
  is already recorded on ADR-0022. (Done during ADR drafting; verify.)

## Tasks

### Decision cross-links (ADR hygiene)
- [x] Verify ADR-0031 header carries `Promoted from: Idea-0025` and
      `Amends: ADR-0022`, idea 0025 carries `Promoted to: ADR-0031` (`Status:
      promoted`), and ADR-0022 carries the reciprocal `Amended by: ADR-0031`.

### Create `updating.agent.md` (agent-facing, self-contained)
- [x] Create a new top-level **`updating.agent.md`** in this standard repo: a terse,
      executable, tool-agnostic rendering of the copy-driven "bring me current"
      procedure, written for an agent that knows nothing about the method beyond
      this file. Steps, verbatim in intent from ADR-0022: (1) read the adopter's
      current version from the `Based on decision-trail vX.Y` citation; (2) re-copy
      the `starter/`-derived method-owned set from the target source into the
      adopter's `docs/`, applying the **preserve rule** (copy method text/templates,
      never overwrite project content — `docs/ideas/`, `docs/decisions/`,
      `docs/plans/`, a populated `docs/travel-diary.md`, `docs/intermediate-artifacts/`,
      `docs/overview.md`); (3) apply each release's non-"none" `Adopter migration:`
      note in version order; (4) bump the citation in **both** `docs/working-method.md`
      and the `AGENTS.md` "How we work" block; (5) regenerate `docs/overview.md`;
      (6) run the conformance check.
- [x] Fold the **conformance check** (headers present, no duplicate numbers, header
      format canonical, title line matches filename, overview in sync, citation
      consistent) into `updating.agent.md` as its closing, independently-invocable
      step — the single operational home for the executable checklist.
- [x] State the **confirmation-guard batch shape** at the top of `updating.agent.md`:
      state the resolved plan (from vX → named target, which migration notes apply,
      what will be re-copied/regenerated) → take one green light → execute → pause
      only for genuine judgment (non-trivial migration, preserve-conflict) → close by
      recording the version-bump ADR + conformance result.

### Slim `adopting.md` chapter 3 (human on-ramp)
- [x] Rewrite chapter 3 ("Update `X.Y → X.Y+n`") to the minimum: the human tells the
      agent to update the method and supplies the source **and** the how-to pointer —
      e.g. *"update the method from `<path/URL>`; the how-to is
      `<path/URL>/updating.agent.md`"* — and the agent runs it transparently,
      confirming before it changes anything. Remove the rehearsed mechanical steps;
      **point to `updating.agent.md`**. Keep the bootstrap note (why the prompt names
      the how-to file).
- [x] Replace the standalone **"Conformance check"** section in `adopting.md` with a
      short pointer to the conformance step now living in `updating.agent.md` (keep it
      invocable on request; do not duplicate the checklist).
- [x] Sanity-check chapters 1–2 (fresh / inject) still read coherently and cross-link
      correctly after chapter 3 shrinks.

### Agent guidance (this repo's `AGENTS.md`)
- [x] Adjust the `## Agent operating guidance` bullets that currently describe the
      copy-driven update + conformance check (ADR-0022) so they point at
      `updating.agent.md` as the executable procedure and note the human-trigger
      shape (intent + explicit source + how-to pointer, run as a guarded batch).
      Do **not** touch the derived method body.

### `guide.md` (decide during execution)
- [x] Decide whether a one-line "updating" pointer belongs in the narrative
      `guide.md`; if yes, add a minimal sentence pointing to `adopting.md` /
      `updating.agent.md`. Keep it a pointer, not a procedure.
      **Decided: no change** — `guide.md` already routes to `adopting.md` for
      updates (§ How to start, § further reading); the agent-facing
      `updating.agent.md` stays out of the human narrative, reached transitively via
      `adopting.md`.

### Release
- [x] Add a new `CHANGELOG.md` version entry (Added: `updating.agent.md` — terse
      agent-facing update procedure; ADR-0031. Changed: `adopting.md` §3 slimmed to
      human intent + pointer; conformance check relocated). Include its
      **`Adopter migration:`** line — **"none"** (presentational; the update
      procedure is standard-repo-facing, nothing an adopter must do).

### Overview
- [x] Regenerate `overview.md` to reflect final states (idea 0025 → promoted,
      ADR-0031 → accepted, this plan) and restamp "as of".

## Out of scope

- **Changing the ADR-0022 update mechanics** — the copy-driven procedure, preserve
  rule, and conformance check move verbatim in intent; they are not redesigned.
- **Shipping any adoption/conformance tool or script** — the conformance linter
  stays a deferred, non-method option (ADR-0031 clause 6, ADR-0008).
- **Putting `updating.agent.md` in `starter/`** — it is standard-repo-only, fetched
  by an adopter's agent from the source, never copied into adopter repos.
- **Editing accepted decisions away** — ADR-0022 is amended via cross-links and
  relocation of its *presentation*, not rewritten; the ADRs stay append-only.
- **Touching the eight-promise contract or the lifecycle.**
