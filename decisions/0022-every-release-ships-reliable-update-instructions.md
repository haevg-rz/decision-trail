# ADR-0022: Every release ships precise, agent-reliable "bring me current" instructions

- Date: 2026-07-04
- Status: accepted
- Promoted from: [Idea-0014](../ideas/0014-every-change-ships-reliable-update-instructions.md)
- Amends: [ADR-0021](0021-a-single-adopter-on-ramp-fresh-inject-update.md)
- Amended by: [ADR-0026](0026-pin-canonical-artifact-header-format.md), [ADR-0031](0031-adopter-update-is-human-intent-agent-execution.md)

## Context

ADR-0021 gave adopters a first update path: read each release's `Adopter
migration:` note between your version and the target, and apply them in order.
Dogfooding that path against a real adopter (`josyn-builder`, on v2.3, updating to
v2.6) surfaced that it answers a **narrower** question than the update requirement
actually demands.

The `Adopter migration:` contract answers *"what is the minimum I must do so the
new version doesn't break me?"* — and for additive features that minimum is
legitimately **"none."** But the instruction an adopter's agent is handed is
*"a newer decision-trail is over there — read it and bring me current"*: put me in
the shape a **fresh adopter of the target version** would have. Those two are not
the same, and the current design only serves the first. Idea 0014 sharpens the
requirement: **any** further change to the standard must ship instructions precise
enough that an agent in an older adopter-repo can reach the fully-current shape
**reliably**, without guesswork.

### Concrete gaps the dogfood run exposed

1. **"none" migrations hide new scaffolding.** 2.4.0 (travel diary) and 2.5.0
   (intermediate artifacts) are additive, so their migration is "none" — yet each
   shipped new starter files (`docs/travel-diary.md`,
   `docs/intermediate-artifacts/`) and new sections in `working-method.md` /
   `guide.md`. After a "none"-driven update, the adopter's method text *describes*
   companions its repo has no scaffold for: not broken, but not fully current.
2. **No manifest of method-owned vs project-owned paths.** "Bring me current" wants
   to re-copy the method-owned files but must **never** clobber project-owned
   artifacts (`ideas/`, `decisions/`, `plans/`, a populated `travel-diary.md`,
   `overview.md`). Getting that selective copy right reliably needs an explicit
   list of which paths the method owns.
3. **`adopting.md` isn't discoverable from a pre-2.6 adopter.** The pointer to
   `adopting.md` was only added to `working-method.md` in 2.6, so a repo on an
   older version has no in-repo breadcrumb to the update procedure; it finds it
   only by reading the standard repo's `CHANGELOG` directly.
4. **The result is unverified.** The version citation must be bumped in two places
   (`working-method.md` and the `AGENTS.md` "How we work" block), and nothing
   checks that the updated repo actually conforms (headers present, overview in
   sync, citation consistent).

### Considered options

- **A — Leave the `Adopter migration:` contract as-is.** Cheapest, but leaves the
  "bring me current" instruction only partially served; additive scaffolds are
  silently omitted and the selective copy stays guesswork (against the sharpened
  requirement, Economy #2, Continuity #1).
- **B — Copy-driven update anchored on a method-owned-files manifest.** Define an
  explicit manifest of method-owned paths (overwrite on update) vs project-owned
  paths (never touch). "Bring me current" becomes: re-copy the method-owned set
  from the target's `starter/`, apply any non-"none" migrations, bump the citation
  in both places, regenerate `overview.md`.
- **C — Two-part migration note per release.** Keep `Adopter migration:` for
  required migrations and add a second additive line (e.g. `New scaffolds:`) naming
  optional files/sections a release introduces, so "bring me current" and "just
  don't break me" are separately answerable.
- **D — B and/or C, plus a lightweight conformance check** — agent do-guidance
  ("does my adopted repo match the method it cites?": headers present, overview in
  sync, citation consistent) that verifies the end state, possibly the one
  give-away that pays for itself.
- **E — A discoverable in-repo pointer** every version carries, so future updates
  don't depend on finding the standard repo's `CHANGELOG` by hand (addresses gap 3,
  combinable with any of the above).

### Decision drivers

- **Reliability of "bring me current"** — the sharpened requirement from idea 0014:
  an older adopter's agent must reach the target's full shape without guesswork.
- **Non-destructiveness** — updating must never clobber project-owned artifacts.
- **Economy (#2) / Borrow (#8)** — prefer deriving a manifest from `starter/` and
  reusing `CHANGELOG` over inventing new machinery; keep the method plain markdown.
- **Genericity (#7)** — the procedure must work for any adopter with no
  hand-knowledge of which files are the method's and which are the project's.
- **Continuity (#1)** — an update should land a repo reliably on the target shape.

## Decision

"Bring me current" is delivered as a **copy-driven update procedure**, distinct
from the required-migration contract, anchored on a `starter/`-derived manifest, a
stable in-repo pointer, and a lightweight conformance check.

- **Copy-driven update (the "bring me current" procedure).** To update an adopter
  from its cited version to a target version, the agent:
  1. Reads the repo's current version from the **"Based on decision-trail vX.Y"**
     citation.
  2. **Re-copies the method-owned set** from the target version's `starter/`
     (mapped to the adopter's `docs/` locations), overwriting those files.
  3. Applies, in version order, any non-"none" **`Adopter migration:`** steps from
     each release between the current and target version.
  4. Bumps the version citation in **both** places — `docs/working-method.md` and
     the `AGENTS.md` "How we work" block.
  5. Regenerates `overview.md`.
  6. Runs the conformance check (below).

  Because the target's `starter/` already contains every additive scaffold (e.g.
  the travel diary, `intermediate-artifacts/`), re-copying lands them
  automatically — no per-release file-addition bookkeeping, and no silent omission
  (closes gap 1). This subsumes and refines the note-driven step 2 of ADR-0021's
  update path.

- **`Adopter migration:` = required behavioral changes only.** The per-release
  contract from ADR-0021 stays, but its scope is clarified: it states *only*
  required **behavioral** migrations an adopter must perform (e.g. "backfill
  missing `Date:` fields, then regenerate `overview.md`"), still **"none"** when
  there is nothing required. New optional scaffolds are **not** enumerated here —
  they arrive via the copy-driven procedure. "Bring me current" and "just don't
  break me" are thus answered by two separate mechanisms.

- **Method-owned set derived from `starter/`, with a preserve rule.** The set of
  method-owned paths (safe to overwrite on update) is **not** a hand-maintained
  manifest; it is **`starter/`'s own contents**, which are the single source of
  truth (consistent with the repo's "derived, never hand-patched" stance, Economy
  #2). Updating copies the method **text and templates** (`working-method.md`,
  `guide.md`, and skeleton/companion scaffolds) and **must preserve project-owned
  content**: the artifact-family contents (`ideas/`, `decisions/`, `plans/`), a
  populated `travel-diary.md`, `intermediate-artifacts/`, and `overview.md` are
  never overwritten. Rule of thumb: **copy method text/templates, preserve project
  content** (closes gap 2, Genericity #7).

- **A stable in-repo pointer.** Every version carries, in its method text
  (`docs/working-method.md`), a durable pointer to the update on-ramp
  (`adopting.md` in the standard repo). Once an adopter lands on a version bearing
  this pointer, all future "bring me current" runs are self-describing — the agent
  finds the procedure in-repo instead of hunting the standard repo's `CHANGELOG` by
  hand (closes gap 3).

- **A lightweight conformance check (agent do-guidance).** The method defines a
  verification step — pure agent do-guidance, **no shipped tool** (faithful to
  ADR-0021's give-away stance) — that answers *"does my adopted repo match the
  method it cites?"* It checks that: every idea/decision/plan carries the mandatory
  `Date:` header; `overview.md` is in sync with the artifact headers; and the
  version citation is consistent in both `docs/working-method.md` and the
  `AGENTS.md` block. It runs at the end of an update and may be invoked any time
  (closes gap 4).

## Consequences

- "Bring me current" reliably lands an adopter on the target version's **full
  fresh-adopter shape**, additive scaffolds included, without per-release
  enumeration — satisfying idea 0014's sharpened requirement (Continuity #1,
  Economy #2).
- The `Adopter migration:` contract gets **lighter and clearer**: release authors
  state only required behavioral steps (still "none" when apt), never a scaffold
  inventory.
- The method-owned set is **derived, not duplicated** — `starter/` stays the single
  source of truth and cannot drift from a parallel manifest — but this depends on a
  crisp preserve rule so project content is never clobbered (Genericity #7).
- Every version becomes **self-describing** about how to update it, so future
  upgrades no longer depend on external archaeology (closes gap 3).
- The conformance check makes "reliably" **verifiable**, closing the loop after an
  update, at the cost of one more do-guidance step and no new dependency (Borrow
  #8).
- Follow-up work: `adopting.md`'s update path must be rewritten to the copy-driven
  procedure; the release-migration contract's wording (ADR-0021) must be refined to
  "required behavioral changes only"; the in-repo pointer and conformance check
  must be added to the method texts. These are execution items for a plan that
  `Implements:` this ADR.

