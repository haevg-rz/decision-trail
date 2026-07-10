# 14. Every change must ship precise, agent-reliable update instructions for older adopters

- Status: promoted
- Date: 2026-07-03
- Parent: [idea 0004](0004-using-decision-trail-in-your-own-repo-should-be-easy.md)
- Promoted to: [ADR-0022](../decisions/0022-every-release-ships-reliable-update-instructions.md)

## Idea

**The requirement, sharpened:** *any* further change in this repo (the standard)
shall be processed and documented in a way that an agent in an **older
adopter-repo** has **precise instructions to migrate/update — as reliable as can
be.** The target reader is not a human browsing a changelog; it is an agent that,
handed only *"a newer decision-trail is over there — read it and bring me
current,"* must be able to execute the update correctly and completely, without
guesswork.

ADR-0021 gave adopters a first update path: read each release's `Adopter
migration:` note between your version and the target, apply them in order.
Dogfooding it against a real adopter (`josyn-builder`, sitting on v2.3, updating to
v2.6) surfaced that this **falls short of the requirement above** — it answers a
narrower question than the agent is actually asked.

The `Adopter migration:` contract answers *"what is the minimum I must do so the
new version doesn't break me?"* For additive features that is legitimately
**"none."** But the instruction the adopter's agent receives is *"adopt all / bring
me fully current"* — *"put me in the shape a fresh adopter of the target version
would have."* Those two are not the same, and the current design only serves the
first. For the requirement to hold, **every release must emit instructions precise
enough that an agent can reach the fully-current shape reliably.**

### Concrete gaps the dogfood run exposed

1. **"none" migrations hide new scaffolding.** 2.4.0 (travel diary) and 2.5.0
   (intermediate artifacts) are additive, so their migration is "none" — yet each
   shipped **new starter files** (`docs/travel-diary.md`,
   `docs/intermediate-artifacts/`) and new sections in `working-method.md` /
   `guide.md`. After updating, the adopter's method text *describes* companions its
   repo has no scaffold for. Not broken, but not "fully current."

2. **No manifest of method-owned vs project-owned paths.** "Bring me current" wants
   to re-copy the method-owned files (`working-method.md`, `guide.md`, new
   templates/folders) but must **never** clobber project-owned artifacts
   (`ideas/`, `decisions/`, `plans/`, the populated `travel-diary.md`,
   `overview.md`). Getting that selective copy right "for sure" needs an explicit
   list of which paths the method owns.

3. **`adopting.md` isn't discoverable from a pre-2.6 adopter.** The pointer to
   `adopting.md` was only added to `working-method.md` in 2.6, so a repo on an
   older version has no in-repo breadcrumb to the update procedure; it finds it
   only by reading the standard repo's CHANGELOG directly.

4. **The result is unverified.** The citation must be bumped in two places
   (`working-method.md` and the `AGENTS.md` "How we work" block); nothing checks
   that the updated repo actually conforms (all headers present, overview in sync,
   citation consistent). A conformance check kept surfacing as the one piece of
   tooling that might genuinely earn its keep (it was noted, then set aside, when we
   decided against an adoption script).

## Why it matters

- **Economy (#2) / Continuity (#1):** "adopt all" should reliably land a repo on the
  target version's full shape, not a partial one that silently omits optional
  scaffolds.
- **Genericity (#7):** the update must work for any adopter without hand-knowledge
  of which files are "the method's" and which are "the project's."
- It is a live, real-world dogfooding finding — exactly the kind of use that the
  "settled, not frozen" method exists to absorb as a new decision-trail change.

## Open questions (for the promoted ADR to settle)

- Should `Adopter migration:` distinguish **"required migration"** from **"new
  optional scaffolds to copy if you want them"** — e.g. a second, additive line per
  release? Or should "bring me current" be a separate procedure from "migrate"?
- Where does a **method-owned-files manifest** live (a list in the standard repo of
  paths that updating may overwrite vs. must preserve), and is it maintained by
  hand or derivable from `starter/`?
- Should the update procedure be *"re-copy the method-owned set from the target's
  `starter/docs/`, then apply non-'none' migrations, then regenerate `overview.md`"*
  — i.e. copy-driven rather than note-driven?
- Does the on-ramp need to be discoverable from **within** an adopter (a stable
  pointer that every version carries), so future updates don't depend on finding
  the standard repo's changelog by hand?
- Is a lightweight **conformance check** ("does my adopted repo match the method it
  cites?") worth defining now — as agent do-guidance, and/or the one give-away that
  actually pays for itself?
