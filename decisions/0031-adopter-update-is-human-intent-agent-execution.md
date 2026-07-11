# ADR-0031: The adopter update path is human intent, agent execution

- Date: 2026-07-11
- Status: accepted
- Promoted from: [Idea-0025](../ideas/0025-clarify-how-a-consuming-repo-adopts-a-newer-version.md)
- Amends: [ADR-0022](0022-every-release-ships-reliable-update-instructions.md)

## Context

Idea 0025 observed that the update path — moving an already-adopting repo from one
version of decision-trail to a newer one — is the least clear part of the on-ramp.
In [`adopting.md`](../adopting.md) it is **chapter 3 ("Update `X.Y → X.Y+n`")**,
and to a human reader it reads as overcomplicated and a little deterrent: a dense
block of re-copy rules, a preserve-vs-overwrite table, citation bumps,
changelog-migration ordering, and a six-point conformance check.

The idea asked the deciding question: is the confusion **presentational** (rewrite
chapter 3 more clearly) or **substantive** (the update ritual itself is heavier
than it needs to be)? Weighing it surfaced the real defect: **mixed audiences.**
The chapter is written as a *human checklist*, yet decision-trail's own
precondition is *an agentic setup* — the agent is present by definition. So the
human is handed mechanical steps a present-by-definition agent should own, and the
prose carries the full copy-driven procedure (ADR-0022) at a human reader when its
true reader is the agent.

Two questions from idea 0025 are settled here; the rest (where a short "updating"
note also lives, the relationship to the deferred GitHub-template option) are left
to the implementing plan and to ADR-0008.

## Decision Drivers

- **Economy (#2):** the human interface for an update should cost one sentence of
  intent, not a checklist rehearsal.
- **Transparency (#3):** each audience should read text aimed at it; a procedure
  that serves neither the human (too heavy) nor the agent (buried in human framing)
  is opaque to both.
- **Continuity (#1) / reliability:** the agent-facing procedure must still land an
  adopter reliably on the target shape — the ADR-0022 contract must survive intact.
- **Settled, not frozen:** ADR-0022 is freshly decided; do not churn a settled
  contract for a defect that is presentational.
- **Borrow, don't invent (#8):** the agent is already the executor; do not ship a
  tool to do what the present agent does.

## Considered Options

1. **A — Human states intent, agent executes (chosen).** Separate the two
   audiences into two artifacts. The human path shrinks to a single intent —
   *"adopt decision-trail vX.Y from `<path>`"* — captured as an ordinary ask (or a
   small ADR in the adopter's own trail) in `adopting.md`. The copy-driven ritual
   (re-copy `starter/`, preserve project content, bump the citation, apply
   migration notes in order, regenerate `overview.md`, run the conformance check)
   moves into a terse, tool-agnostic **agent-facing file, `updating.agent.md`**, so
   the agent loads only the procedure — not the human prose — when updating. The
   ADR-0022 mechanics are unchanged.
2. **B — Dual-audience rewrite.** Keep chapter 3 hand-executable by a human, just
   re-present it more clearly. Rejected: given the agentic precondition,
   hand-execution is a path that essentially never runs, and preserving it is
   exactly what keeps the prose heavy — it optimizes for a case that does not
   happen at the cost of the case that does.
3. **C — Also simplify the ADR-0022 mechanics.** Reopen the update ritual itself
   (e.g. drop the preserve/overwrite distinction or the conformance check).
   Rejected: the mechanics are sound and freshly settled; the only genuinely fiddly
   spot — the preserve rule's "shipped scaffold vs. project-populated content"
   judgment (e.g. an adopter-populated `travel-diary.md` must not be overwritten) —
   is a reasoning step the agent already handles, and sharpening its *wording* is
   re-presentation, not a contract change. Simplifying would churn a settled
   contract for no substantive gain.
4. **D — Ship a conformance/regeneration tool.** Split the steps by determinism:
   regenerating `overview.md` and most of the conformance check are deterministic
   (a linter + regenerator), while applying each release's `Adopter migration:`
   note is bespoke and future-unknown, so no general "update tool" is possible.
   Rejected as a build item: the agent already is that tool (Borrow #8, and the
   existing "Why there's no adoption tool" stance). Kept as a **deferred option**
   — a conformance linter — parked like the GitHub-template convenience in
   ADR-0008, not built now.

## Decision

The adopter update path is re-presented around a clean **audience split**; the
ADR-0022 update contract is left mechanically intact.

1. **Human interface = intent + an explicit source + the how-to pointer.**
   Updating is triggered by a plain-language intent that names **both** the source
   and where the procedure lives — *"update the method from `<path/URL>`; the how-to
   is `<path/URL>/updating.agent.md`"* — meaning, not a fixed command string
   (agents parse intent; consistent with the tool-agnostic entry point, ADR-0006).
   The human **must supply the source** (a path/URL to the target version); the
   **agent never guesses** the target or fetches a "latest" on its own. From there
   the agent reads the repo's current version from the `Based on decision-trail
   vX.Y` citation, loads the named `updating.agent.md`, and runs it. The human is
   not asked to perform or rehearse the mechanical steps.

   **Bootstrap (the hen-and-egg).** The version that *introduces* this mechanism is
   the first whose `updating.agent.md` an adopter can use — but an adopter sitting
   on an **older** version has no in-repo knowledge that the file or the procedure
   even exists. The trigger resolves this by **carrying the how-to pointer in the
   prompt itself**: because the human names `<source>/updating.agent.md` explicitly,
   the adopter's agent needs no prior knowledge of the update method — the prompt
   hands it the entry point. Once updated, the in-repo pointer shipped by ADR-0022
   makes future runs self-describing, but the **bootstrap prompt never depends on
   prior in-repo knowledge**.

   The run is **one transparent batch under the confirmation guard** (ADR-0019):
   the agent first states the resolved plan (from vX to the named target; which
   releases' `Adopter migration:` notes apply; what it will re-copy and
   regenerate), takes **one green light**, then executes the whole batch —
   *pausing only* where a step needs genuine human judgment (a non-trivial
   migration note, or a preserve-conflict) — and closes by recording the
   version-bump ADR and the conformance-check result. Neither silent auto-apply
   nor step-by-step nagging.

2. **Agent interface = execution, in its own file.** The copy-driven "bring me
   current" procedure from ADR-0022 — re-copy the `starter/`-derived method-owned
   set, preserve project-owned content, apply non-"none" `Adopter migration:` notes
   in version order, bump the citation in both places, regenerate `overview.md`,
   run the conformance check — lives as a **terse, agent-facing file,
   [`updating.agent.md`](../updating.agent.md)**, in the standard repo alongside
   `adopting.md`. It is the *operational* rendering: executable steps, no human
   narrative. This lets an agent load only the procedure it needs when updating,
   instead of wading through the human on-ramp prose. The name is deliberately
   **tool-agnostic** (not a harness-specific `*.instructions.md`), faithful to the
   single tool-agnostic entry point (ADR-0006, Genericity #7). Note this file is
   *not* always-loaded — it is read only during an update — so the saving is a
   per-update economy, narrower than the always-on concern of ADR-0029.

3. **`adopting.md` chapter 3 becomes intent + pointer.** The human on-ramp's
   update chapter shrinks to the minimum: tell the agent to update the method and
   give it the source (path/URL or version), and it runs `updating.agent.md`
   transparently, confirming before it changes anything. It no longer rehearses the
   mechanical steps — it points to `updating.agent.md`.

4. **Single operational source of truth — no triplication.** The steps must not
   be duplicated across three artifacts. Roles are split cleanly: **ADR-0022** is
   the *contract and rationale* (why); **`updating.agent.md`** is the *executable
   steps* (the operational source of truth); **`adopting.md`** carries *human
   intent and a pointer*, never a copy of the steps (Economy #2 — the renderings
   must never diverge).

5. **ADR-0022 mechanics unchanged.** This ADR **amends** ADR-0022 only in
   *presentation and audience framing*. Every step, the preserve rule, and the
   conformance check remain exactly as decided; nothing in the contract is added,
   dropped, or reordered — they simply move into `updating.agent.md`.

6. **No tool now; a conformance linter is a deferred option.** Consistent with the
   existing toolless stance, nothing is shipped. The deterministic subset
   (`overview.md` regeneration and the mechanical conformance checks) is recorded
   here as a **deferred, optional** convenience — a linter, never an "update tool"
   — to be reconsidered separately, alongside the ADR-0008 template option.

Placement is an execution concern for the implementing plan: create
`updating.agent.md` with the terse executable procedure, slim `adopting.md`
chapter 3 to the one-sentence human intent plus a pointer to it, and decide
whether a short "updating" note also belongs in the narrative `guide.md`.

## Consequences

- The update path reads honestly for each audience, in separate artifacts: the
  human sees a single intent in `adopting.md`; the agent loads the full, reliable
  procedure from `updating.agent.md`. The "deterrent" quality idea 0025 flagged is
  removed without weakening the contract (Economy #2, Transparency #3).
- ADR-0022's copy-driven update, preserve rule, and conformance check remain the
  authoritative mechanics — this amendment re-teaches and relocates them into
  `updating.agent.md`, it does not rewrite them (Continuity #1).
- The steps gain a single **operational** source of truth (`updating.agent.md`);
  `adopting.md` and ADR-0022 point at it rather than duplicating it, so the three
  cannot drift (Economy #2).
- This is a **presentational** change to method-adjacent text (a new
  `updating.agent.md`, a slimmed `adopting.md`, possibly a `guide.md` note); it
  introduces no new status, cross-link field, or lifecycle rule, and requires no
  adopter behavioral migration — the `Adopter migration:` for its release is
  "none."
- A conformance linter stays explicitly deferred, so a future decision to build one
  starts from a recorded option rather than a fresh debate.
- **Bootstrap is closed:** because the human trigger names the target's
  `updating.agent.md` explicitly, an adopter on any older version can update without
  prior in-repo knowledge of the mechanism — so `updating.agent.md` must be
  **self-contained** (it assumes the running agent knows nothing about the update
  method beyond what the prompt and the file itself say).
- Follow-up work for the implementing plan: create `updating.agent.md`; slim
  `adopting.md` chapter 3 to intent + pointer; decide the `guide.md` note; keep the
  ADR-0022 wording intact.
