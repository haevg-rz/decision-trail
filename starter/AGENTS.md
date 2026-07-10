# <project name>

<!--
If this repo already had an AGENTS.md, keep it and append only the
"## How we work" and "## Agent operating guidance" sections below. Otherwise,
replace this heading with your project's name and a short description of what the
project is.
-->

## How we work

This project follows **decision-trail** — a generic method for carrying a thought
through its whole life (idea → proposal → decision → plan → execution) in plain
markdown. New here? Start with the guide in [`docs/guide.md`](docs/guide.md). The
terse reference is [`docs/working-method.md`](docs/working-method.md); decision
records live in [`docs/decisions/`](docs/decisions/), starting with
[`0001-adopt-decision-trail.md`](docs/decisions/0001-adopt-decision-trail.md).

Based on decision-trail v2.9 — https://github.com/ckluth/decision-trail

## Agent operating guidance

These rules are for an AI agent working in this repo:

- **Artifact numbers are ordinal only.** When creating an artifact, assign the
  next unused number in that family (`docs/ideas/`, `docs/decisions/`,
  `docs/plans/` are independent sequences). Never derive a number from a related
  artifact — a plan implementing ADR-0004 is not named `0004`; it gets the next
  free plan slot. Relationships are expressed via cross-link fields
  (`Implements:`, `Promoted to:`, etc.), never via matching numbers.
- **Status values are per-family — never mix them.** A new idea starts `seed`, a
  new proposal `proposed`, a new plan `draft`. Pick a status only from the target
  artifact's own family: an idea is never `proposed`/`draft`/`accepted`; a plan is
  never `proposed`/`seed`; a proposal/decision is never `seed`/`draft`.
- **The method is settled.** Use decision-trail; don't redesign the *method*
  casually. (Your project's own decisions are normal work — captured as ideas,
  ADRs, and plans under `docs/`.)
- **Confirmation guard.** Never rush into writing, editing, or implementing. First
  briefly explain what you intend to do, then wait for explicit approval.
  Discussing and proposing is always fine — acting requires a green light. Before
  acting, name your intended scope explicitly — especially when a bare "yes"/"ok"
  could be read as approving a larger batch rather than just the single next step.
- **Keep `docs/overview.md` current.** It is a derived snapshot, regenerated
  wholesale from the artifact headers (never hand-patched) and stamped "as of
  <date>". Regenerate it — and update the stamp — whenever the user explicitly
  asks. A user may flip a state directly in an artifact; the next regeneration
  reconciles the index.
- **Travel diary — guard-free.** `docs/travel-diary.md` is an optional, informal
  human-facing logbook, outside the lifecycle and **not a source of truth**. When
  the user says *"add a chapter to the travel diary"* (or similar), prepend a new
  dated `## [YYYY-MM-DD]` section (same-day entries disambiguated `-(2)`, `-(3)`,
  …) covering where we are / what we achieved / what is left / what is next, with
  an optional continuation brief. This is a light-weight task — **no ADR, no plan,
  and no confirmation guard**. Full instructions live in the diary's own header.
- **Intermediate artifacts — guard-free.** `docs/intermediate-artifacts/` is an
  optional, informal scratch persistence layer for material gathered during plan
  execution, outside the lifecycle and **not a source of truth**. Creating,
  populating, and deleting files there is a light-weight task — **no ADR, no plan,
  and no confirmation guard** — because it touches nothing authoritative. Its
  internal organization is the project's business; it is committed by default (a
  repo may gitignore it) and left to rot harmlessly once a plan is done.
