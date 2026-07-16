# ADR-0040: An optional, deterministic overview-regen script, prose-normative and instruction-triggered

- Date: 2026-07-16
- Status: accepted
- Promoted from: [idea 0033](../ideas/0033-overview-regen-mechanical-yet-error-prone-script-or-skill.md)

## Context

Regenerating `overview.md` has stopped being a *trivial* agent task. It now means:
scan every artifact header, reconcile title-line ordinals, rebuild three family
tables, the ADR → plans sub-index (ADR-0034), and the "accepted, no plan yet"
backstop (ADR-0038) — five derived views over ~100 artifacts and climbing. The work
is **purely mechanical**, yet its correctness rides on model capability and
instruction precision, and real drift has already crept in (hand-shortened titles,
a stale H1, a double-prefix H1) precisely because a fallible agent did by hand what
a deterministic routine would do identically every time. As the derived views grow,
the task gets *more* error-prone, not less.

Idea 0033 measured the trade rather than argued it (numbers as of 2026-07-15, this
repo):

- **Token cost** — naive hand-regen ~110k in / 6.2k out; a disciplined shell-scan
  hand-regen ~8–13k in / 6.2k out; a deterministic script ≈ 0 / 0 (just `run` +
  "done"). The script's *marginal* win over disciplined hand-regen is ~12k
  tokens/regen, not 110k.
- **Determinism** — prose output varies by model and run (3 drift classes already
  observed); a script is byte-identical every run, every model.
- **The crux** — much observed drift is a *source-header* authoring problem the
  regen faithfully copies, not a regen-logic problem; ADR-0026 and ADR-0028 already
  guard headers at the source, and *detection* (a verifier) catches exactly the
  remaining hand-edit risk at ~1/12th the output cost of regeneration.

The tension is real and is a first-class promise: decision-trail is deliberately
**harness- and tool-agnostic** (Transparency #3, Genericity #7, Borrow-don't-invent
#8). Any executable artifact risks binding the method to a runtime, adding opaque
code where markdown is legible, and — worst — becoming the *de-facto* path while the
"fallback" prose silently rots away from it.

Prior art must not be re-litigated blindly. **ADR-0036 (rejected)** turned down
rendering the method's fixed procedures as optional *skills*; this proposal is
narrower — scoped to the **overview regen specifically**, motivated by *observed*
drift, and deliberately *not* a harness-bound skill. **ADR-0030** said "revisit
optional tooling if adopters demand structured operation"; this itch is that trigger
firing from *inside* the method's own use.

## Decision Drivers

- **Reliability** — kill the observed drift classes; deterministic, model-invariant
  output.
- **Economy (#2)** — cut the per-regen token cost toward zero for a task that only
  grows.
- **Agnosticism (#3, #7, #8)** — do not bind the method to a runtime, do not let an
  opaque artifact become the sole path, keep plain markdown normative.
- **Precedent discipline** — respect ADR-0036's rejection and ADR-0030's
  revisit-trigger; stay narrowly scoped.

## Considered Options

1. **Do nothing.** Accept hand-regen as the price of agnosticism. Costs ~12k tokens
   + one drift-risk per regen, forever, growing with each new derived view.
2. **Generation script, normative.** Make a script *the* way to regen. Fastest and
   most deterministic, but pays the *full* purity cost (runtime binding, opaque
   code) and makes the script the source of truth — the sharpest break with #3/#7/#8.
3. **Conformance verifier only.** Keep prose generation, add a cheap read-only check
   that flags the 3 drift classes. Pays a fraction of the purity cost but leaves the
   ~12k-token generation cost and model variance in place.
4. **Optional generation script, prose-normative, instruction-triggered (chosen).**
   Add the script as an *optional companion*; keep the prose procedure normative;
   trigger it by a single instruction, not a hook or command; have the script also
   *flag* non-conformant headers so detection rides along with generation.

## Decision

Adopt option 4: add a **deterministic `overview.md` regeneration script as an
optional companion** to the method, under three constraints that preserve
agnosticism.

1. **Optional and additive.** The script is a convenience companion, in the same
   spirit as `travel-diary.md`, `intermediate-artifacts/`, and `derived-artifacts/`.
   The **prose refresh procedure stays normative** (the spec in `AGENTS.md` /
   `working-method.md`); the script is a faithful *implementation of* that spec —
   same five derived views, same ordering — never a divergent second source of truth.

2. **Instruction-triggered, not harness-bound — and invisible to the user.** The
   **user-facing trigger is unchanged** from ADR-0016: the same plain "regenerate
   `overview.md`" request (or the agent proposing it and the user saying "yes"). The
   user never recites any script-vs-prose logic — a long explicit prompt would just
   guarantee no one uses it. Instead, the branch lives **entirely in standing agent
   guidance**: on any regen request the agent *itself* looks for the script and, if
   present, executes it; if absent, it regenerates the prose way. Not a hook, not a
   slash-command. An adopter without the script's runtime simply falls through to the
   prose path — agnosticism holds by construction. The script is written in
   cross-platform `pwsh` (portable, no Windows-only dependency); an adopter may
   replace it with an equivalent in any language, since only the *output* is contract,
   not the script.

3. **Generation with built-in detection.** Because verifying is far cheaper than
   generating and catches the residual hand-edit risk, the script does not silently
   copy source-header drift: on encountering a non-conformant header (bare/bullet-less
   header block per ADR-0026, or a title-line ordinal that disagrees with the filename
   slot per ADR-0028) it **flags** it rather than emitting a misfiled or dropped row.
   This folds idea 0033's "verifier" win into the generator — determinism *and*
   detection in one artifact.

The script ships in the method's own repo and in the `starter/` skeleton so adopters
receive it via the copy-driven update (ADR-0022); its presence or absence is exactly
what the instruction trigger keys on.

## Consequences

- **Reliability + Economy.** Regen becomes byte-identical and near-zero-token when
  the script is present; the 3 observed drift classes are eliminated for the
  generation logic and *surfaced* (not copied) for source headers.
- **Agnosticism preserved, not sacrificed.** Prose stays normative and self-
  sufficient; the runtime binding is optional and fall-through-safe; only
  `overview.md`'s *shape* is contract, so any-language reimplementation is legal.
- **Prose-rot risk — acknowledged and bounded.** The stated mitigation is that the
  script is defined as an *implementation of* the normative prose spec, must track the
  same five views, and any change to the derived views is made in the spec first, then
  the script. This ADR does not pretend the risk is zero; it pins the discipline that
  keeps the two tied.
- **Relation to prior art.** This does **not** reopen ADR-0036 (no harness-bound
  skill; a plain optional script) and is the concrete adopter-demand instance ADR-0030
  reserved. It adds an optional companion; it changes no lifecycle status, no
  cross-link field, and no promise.
- **Follow-on.** On acceptance, a `draft` stub plan `Implements:` this ADR to actually
  write the `pwsh` script, wire the instruction trigger into the agent guidance, and
  place the script in `starter/` for copy-driven delivery.
