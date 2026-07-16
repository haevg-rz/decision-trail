# Idea 0033: Overview regeneration is mechanical yet error-prone — is a script/skill/tool worth the agnosticism cost?

- Date: 2026-07-15
- Status: promoted
- Promoted to: [ADR-0040](../decisions/0040-optional-deterministic-overview-regen-script.md)

## The itch

Regenerating `overview.md` has quietly stopped being a *trivial* agent task. It is
now: scan every artifact's header, reconcile title-line ordinals, rebuild three
family tables, the ADR → plans sub-index (ADR-0034), and the "Accepted — no plan
yet" backstop (ADR-0038). That is **purely mechanical** — but its correctness now
depends on the model's capability and the precision of the agent instructions.
Real drift has already crept in (hand-shortened titles, a stale H1, a double-prefix
H1) precisely because a fallible agent did by hand what a deterministic routine
would do identically every time. As the derived views grow, the task gets more
error-prone, not less.

## The dilemma

decision-trail is deliberately **harness- and tool-agnostic**: it relies on
instructions and plain markdown only (contract #3 Transparency, #7 Genericity, #8
Borrow-don't-invent). That agnosticism is a core promise.

But a **script / skill / tool** for the regen would have real value the pure-prose
approach cannot match:

- **Reliability** — deterministic output, no model-to-model variance, no drift.
- **Economy (#2)** — far fewer tokens than re-deriving by hand each time.
- **Precision** — the very kind of mechanical, spec-fixed procedure a machine
  should own, not re-reason.

The tension: adding *any* executable artifact risks breaking tool-agnosticism and
transparency — a script is opaque where markdown is legible, and it binds the
method to a runtime/language the next adopter may not have.

## Prior art in this repo (do not re-litigate blindly)

- **ADR-0036 (rejected)** — "render the method's fixed procedures as optional
  skills." This idea is *not* a straight re-run of that: it is scoped narrowly to
  the **overview regen specifically**, and is motivated by *observed* drift, not a
  general wish to skill-ify procedures.
- **ADR-0030** — "revisit optional skills if adopters demand structured operation."
  This itch is a concrete instance of exactly that trigger, driven from inside the
  method's own use rather than an external adopter.

## Possible directions (unexplored — for the proposal, not this seed)

- A tool/script, but **optional and additive** — the prose procedure stays the
  normative fallback, so agnosticism holds; the script is a convenience an adopter
  may or may not run.
- A **skill** (harness-specific) that wraps the same spec — value without touching
  the markdown source of truth.
- Tightening the **prose procedure + a conformance check** instead, so the agent's
  hand-regen is verifiable rather than replaced.
- Do nothing — accept hand-regen as the price of agnosticism.

## Facts to weigh (measured 2026-07-15, this repo)

The decision felt too theoretical, so here are hard numbers rather than adjectives.
The four directions above resolve to **two distinct levers** the seed lists side by
side without separating: attack *generation* (make it deterministic — script/skill)
or attack *detection* (make errors catchable — a conformance check). They pay very
different prices.

**Scale (and it only grows):**

| Metric | Value |
|--------|-------|
| Artifacts to scan | 98 (33 ideas + 38 decisions + 27 plans) |
| Growth | 98 in ~2.5 weeks of active use — climbing steadily |
| `overview.md` size | 178 lines, ~6.2k tokens of output |
| Derived views to rebuild | 5 (3 family tables + ADR → plans + stand-alone) |
| Observed drift incidents | 3 classes (hand-shortened titles, stale H1, double-prefix H1) |

**Token cost per regen (Economy #2):**

| Approach | Input tokens | Output tokens | Notes |
|----------|-------------|---------------|-------|
| Naive hand-regen (read full files) | ~110k | ~6.2k | reads all 439 KB |
| Header-scan hand-regen (shell pre-filter) | ~8–13k | ~6.2k | `Select-String` filters first |
| Deterministic script | ~0 | ~0 | just `run` + "done"; script writes the file |
| Conformance check (verify only) | ~8–13k | <0.5k | reads headers + overview, returns pass/fail |

The token gap is ~15k–115k per regen → near-zero. But note the *header-scan*
approach already cuts naive cost ~10×, so the script's **marginal** win over a
disciplined hand-regen is ~12k tokens/regen, not 110k.

**Determinism (Reliability):**

- Prose regen: output varies by model and run; 3 drift classes already observed.
  Correctness = model capability × instruction precision.
- Script: byte-identical every run, every model — but only for the *copying* step.
  It cannot fix bad *source* headers; ADR-0026 (header format) and ADR-0028
  (title-line pin) already guard those at the source, so much observed drift is an
  authoring problem the regen faithfully copies, not a regen-logic problem.

**Method-purity cost (the price):**

| Cost | Concrete measure |
|------|------------------|
| Opaque code added | ~60–100 lines, illegible where markdown is legible (Transparency #3) |
| Runtime binding | picks one of Python/Node/PowerShell; an adopter without it can't run it (Genericity #7) |
| Promises touched | #3, #7, #8 — unless strictly optional/additive with prose normative |
| Prose-rot risk | once a script exists it becomes the de-facto path; the "fallback" prose silently rots and drifts from it |
| Precedent | ADR-0036 rejected general skill-ify; ADR-0030 says "revisit on adopter demand" |

**The honest asymmetry (the crux):**

- A **generation script** pays the *full* purity cost (runtime binding, opaque code,
  prose-rot) for the full determinism + token win.
- A **conformance check** pays a *fraction* of that cost — small, read-only, returns
  pass/fail, can stay prose ("verify these 4 invariants") or be a tiny optional
  script — while still killing the 3 drift classes, because verifying is far easier
  than generating. It keeps hand-regen but makes it *safe*.
- **Do nothing** costs ~12k tokens + one drift-risk per regen, forever, growing with
  each new derived view.

The single fact that reframes it: a hand-regen on 2026-07-15 came out correct
because headers were gathered with a *deterministic shell scan* and only reasoned
over afterward — the sole real risk was hand-editing a title. **Detection would have
caught exactly that, at ~1/12th the output cost of regeneration** — the strongest
single argument for the verifier over the generator.

An unexplored middle the numbers suggest: **deterministic scan + verifier**, with
full generation staying prose. A cheap next step (for the proposal, not this seed)
would be to prototype the portable read-only conformance check and measure its
actual cost and false-positive rate on this repo, turning the last theoretical
corner into data.

## Not yet decided

Whether the value beats the agnosticism cost at all; if yes, which form (script /
skill / verifier) and how to keep it strictly optional and non-binding; how it
relates to ADR-0036's rejection and ADR-0030's revisit-trigger. All of this belongs
to a proposal, not this seed.
