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

Based on decision-trail v2.13 — https://github.com/haevg-rz/decision-trail

## Agent operating guidance

These rules are for an AI agent working in this repo. They **complement, not
restate** the spec in [`docs/working-method.md`](docs/working-method.md): where a
mechanic is fully specified there, this list only flags the trap to avoid and
points to it.

- **Follow the spec's mechanics** in
  [`docs/working-method.md`](docs/working-method.md) exactly — they are lookups,
  not judgment calls:
  - **Ordinal numbering** — next free slot per family via `max(number)+1`, verify
    the filename is unused; never reuse a related artifact's number; renumber
    out-of-order inserts with insert-and-shift (§ *The lifecycle*).
  - **Per-family status** — a new idea is `seed`, a proposal `proposed`, a plan
    `draft`; never borrow another family's status (§ *The lifecycle*).
  - **Canonical header + title line** — a bulleted header block, and a typed,
    zero-padded H1 ordinal matching the filename slot; a bare (bullet-less) header
    is silently missed by the refresh, and a title/filename ordinal mismatch is a
    conformance failure (§ *The lifecycle*).
  - **Disentangling a large idea** — bud into children, mark the parent
    `decomposed`, document the reasons in the parent; never multi-promote, never
    stack `promoted` and `decomposed`. **Propose** the split; the human decides
    (§ *Disentangling a large idea*).
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
  <date>" — the refresh procedure is specified in the spec (§ *The lifecycle*).
  Regenerate it — and update the stamp — whenever the user explicitly asks. A user
  may flip a state directly in an artifact; the next regeneration reconciles the
  index.
- **Travel diary — guard-free.** When the user says *"add a chapter to the travel
  diary"* (or similar), prepend a new dated `## [YYYY-MM-DD]` section to
  `docs/travel-diary.md` (same-day entries disambiguated `-(2)`, `-(3)`, …) —
  where we are / what we achieved / what is left / what is next, with an optional
  continuation brief. Light-weight: **no ADR, no plan, no confirmation guard**
  (§ *Travel diary*).
- **Intermediate artifacts — guard-free.** Creating, populating, and deleting
  files under `docs/intermediate-artifacts/` is light-weight — **no ADR, no plan,
  no confirmation guard** — because it touches nothing authoritative
  (§ *Intermediate artifacts*).
