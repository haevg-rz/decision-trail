# Idea 0026: the guide's derived-rendering sync model can't hold audience deltas

- Date: 2026-07-11
- Status: seed

## Observation

The home repo's [`guide.md`](../guide.md) declares itself a **derived rendering**
of the canonical [`starter/docs/guide.md`](../starter/docs/guide.md): *"regenerated
wholesale, never hand-patched. The only delta is paths … and it points at this
repo's `AGENTS.md` instead of the adopter's `docs/working-method.md`."* That claim
is no longer true. Surfaced while dogfooding the `updating.agent.md` update path
from a real consuming repo (idea 0025 / ADR-0031 / plan 0021).

Two sections now diverge by **audience**, not by path:

- **"How to start"** — the home guide opens with an adoption lead-in (*clone the
  standard repo, follow `adopting.md`*) before the lifecycle steps; the adopter's
  `starter` guide skips that and goes straight to the lifecycle, closing with
  *"Your repo's `docs/decisions/0001-adopt-decision-trail.md` already records the
  decision to adopt."* (added deliberately in the 2.13 documentation patch).
- **"Where to go next"** — the two carry different further-reading lists (home
  points at its own `decisions/` construction log; the adopter points at
  `working-method.md` + `AGENTS.md` + the external `adopting.md` URL).

These deltas are **correct per audience** — they must *not* simply be exchanged: an
adopter already has the method (adoption instructions would misfire), and the home
repo has no `0001-adopt-decision-trail.md` ADR (its `0001` is *"Record decisions as
ADRs"*). The problem is not the content; it is that the **sync contract can't
describe them**.

## Why this deserves its own thread

Two concrete defects follow from the mismatch:

1. **The sync note misdescribes reality** — it claims a paths-only delta while real
   content deltas exist, so a reader (or agent) trusting the note is misled.
2. **A faithful regeneration would clobber the home-only content** — "regenerate
   wholesale from `starter` with only path deltas" would silently delete the home
   guide's adoption lead-in and its construction-log further-reading. The 2.13
   patch is a latent casualty of the next honest regen.

This touches the **ADR-0014** single-source/sync-renderings contract, so it is a
method question — capture it, weigh options, decide in the open, rather than
hand-patching the note.

## Open questions

- Is the fix **presentational** (rewrite the sync note to enumerate the
  audience-specific sections as legitimate, preserved-on-regen deltas) or
  **substantive** (the derivation model itself can't carry section-level audience
  differences and needs rethinking)?
- Should the model stay *"derived rendering, path-only delta"* and the audience
  differences be **converged away** (one wording that serves both), or should the
  two guides be recognized as **genuinely audience-forked** at named sections?
- If deltas are made explicit, what is the crisp rule an agent follows so a
  regeneration **transforms** those sections per audience instead of flattening
  them — without turning regen into an open-ended judgment call?
- Does this generalize beyond the guide? Do `working-method.md` / `AGENTS.md`
  carry similar undeclared audience deltas that the same fix should cover?
- Relationship to ADR-0014 (sync renderings, separate audiences): does that ADR
  need an amendment, or only a sharper statement of what "derived" permits?
