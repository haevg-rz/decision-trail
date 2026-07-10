# ADR-0027: A `decomposed` status for a large idea that buds into children

- Date: 2026-07-10
- Status: accepted
- Promoted from: [Idea-0017](../ideas/0017-decomposing-a-large-idea-container-gap.md)
- Amends: [ADR-0024](0024-status-vocabulary-guard-per-family.md)

## Context

A genuinely large idea sometimes appears: one that braids several *orthogonal*
axes that only have weight **together**, as a map, where no single axis is yet
ripe enough to carry its own file. The method already has the right mechanical
tool for this — **budding** (contract promise #6): the large idea is a *parent*
that spawns child ideas via `Parent:`, and each child matures and promotes 1:1
to its own ADR. Multi-promotion is deliberately *not* the answer, because
promotion is strictly one-to-one (ADR-0012: a promotion link is reciprocal
precisely because both ends are single and write-once).

That mechanism works, but it exposes a gap in the **idea status vocabulary**,
which is only `seed → promoted / dropped`. A parent whose job is to hold a set of
axes and bud children has **no honest resting place** once it has done that job:

- it lingers at `seed` indefinitely, even though it is no longer an unexamined
  seed but a deliberately-kept, fully-worked-through index — so the `seed` row in
  `overview.md` actively *misleads*, reading as "unexamined" when the truth is
  "content has moved into children";
- or it is forced to `dropped`, which asserts rejection — but nothing was
  rejected; its content simply *moved* into children;
- or it is force-fit to `promoted` by pointing at one narrow child ADR, which
  misdescribes the parent — only one slice matured, not the whole map.

The semantic slot for "this idea's purpose was realized **through its children**,
not through its own promotion" is genuinely empty. There is also no stated,
ready-to-run *pattern* for the disentangling itself, so two reasonable agents
decompose the same large idea differently, each re-reasoning the mechanics from
scratch.

## Decision Drivers

- **Transparency (#3):** a hollowed-out `seed` lies in the overview; a status
  must be able to tell the truth about a decomposed parent.
- **Economy (#2) / Borrow, don't invent (#8):** solve this with the smallest
  possible addition — status semantics plus prose — not new machinery.
- **Agility (#5):** nothing is locked; a decomposition can be revisited.

## Considered Options

1. **Leave the parent at `seed`, reframed as "not yet promoted."** Honest for a
   *still-budding* map, but a *finished* one still reads as unexamined — the
   overview keeps lying.
2. **Overload `dropped`.** Rejected: `dropped` means *rejected*; reusing it for
   *successfully decomposed* destroys its meaning.
3. **Force `promoted` at a child ADR.** Rejected: misdescribes the parent, and
   collides with the 1:1 promotion invariant (ADR-0012).
4. **Add one terminal-ish status word, `decomposed`, hand-curated.** Chosen.

`decomposed` was preferred over `fulfilled`/`finished` deliberately: it describes
what happened to the **parent** (it broke into children) and says **nothing about
the fate of the children** — some may still be `seed`, some may be `dropped`.
`fulfilled` would over-claim success the parent cannot vouch for. `finished` sits
too close to the plan family's `done` (guard against cross-family borrowing,
ADR-0024).

## Decision

Add one value to the **idea** family's status vocabulary and state the
decomposition pattern as prose guidance. No new machinery.

1. **Idea status vocabulary becomes `seed → promoted / dropped / decomposed`.**
   `decomposed` is a rare, alternative *finalized* state (alongside the standard
   finalized `promoted`): the idea broke into budded children and its own content
   moved out. It asserts nothing about the children — their fate is told by
   *their* statuses. In `overview.md` a `decomposed` row is a pointer: *don't
   look here for substance — follow the `Parent:` links.*

2. **Reframe `seed`** in words as "not yet promoted," legitimately including a
   standing parent map that is still budding children. A living index sits at
   `seed` honestly; only once budding is finished and the map's content lives in
   the children does the human flip it to `decomposed`.

3. **One status per idea, no stacking.** Both `promoted` and `decomposed` read to
   a human as *finalized*. An idea takes whichever describes what happened; they
   are never combined. The question "can an idea be both `promoted` and a parent?"
   dissolves — a map idea is `decomposed`, not `promoted`.

4. **Hand-curated, no mechanism; reversible (#5).** Nothing computes or enforces
   `decomposed`; the responsible human flips it when the `seed` no longer reflects
   reality. It can be flipped back to `seed` to bud one more child later.

5. **A fixed *pattern* for disentangling, but no prescribed *strategy*.** When the
   thought "let's disentangle this idea" arises, the *how* is a lookup, not a
   debate: the parent idea stays and becomes `decomposed`; each axis buds into a
   child via `Parent:`; each child promotes 1:1 to its own ADR; and **the reasons
   for the branching are documented in the parent idea.** What is *not* prescribed
   is the strategy — whether to promote an already-decidable core first and bud
   the rest, or bud everything and let the parent stand as a pure map. That stays
   a judgment call, decided in conversation. **The agent may (and a good one will)
   propose the disentangling; the responsible unit is the conversing human.**

Placement: the vocabulary addition and the disentangling *pattern* belong in the
**derived method body** (so they reach adopters via the copy-driven update,
ADR-0022), reinforced by a short bullet in the **agent-guidance** section. The
human-facing **advice** for recognizing *when* and *how* to disentangle a large
idea belongs in the narrative **guide**.

## Consequences

- The idea family gains an honest terminal state for a budded parent map, closing
  the transparency leak where a hollowed-out `seed` misled the overview.
- ADR-0024 is amended: the idea family's vocabulary and its stated entry/finalized
  states now include `decomposed`; the per-family exclusivity guard extends to it.
- Both method renderings (`AGENTS.md` and `starter/docs/working-method.md`) must
  be updated together (ADR-0014's sync rule), the guide gains human advice, and
  the change reaches existing adopters through the copy-driven "bring me current"
  path (ADR-0022).
- This is an **additive vocabulary** change with no automatic reinterpretation of
  existing artifacts: no `seed` idea is retroactively `decomposed`. The
  `Adopter migration:` for the release is therefore "none" — the new wording and
  the extra permitted status arrive automatically via the copied method text.
- The implementing plan decides the exact wording and whether the lifecycle table
  annotates `decomposed` as an alternative finalized state versus a one-line prose
  note beneath it.
