# Plan 0029: Ship the optional deterministic overview-regen script and its agent-guidance trigger

- Date: 2026-07-16
- Status: done
- Implements: [ADR-0040](../decisions/0040-optional-deterministic-overview-regen-script.md)

Mechanical execution of ADR-0040: add a deterministic, cross-platform `pwsh`
script that regenerates `overview.md`, plus the standing agent-guidance rule that
makes the agent look for the script on any regen request (script-first, prose
fallback) — invisible to the user, whose trigger stays the plain ADR-0016 request.
The script must faithfully implement the *normative prose refresh procedure* (same
five derived views, same ordering) and **flag** non-conformant headers (ADR-0026
bullet block, ADR-0028 title-line ordinal) rather than silently copy drift. The
canonical spec is `starter/docs/working-method.md`; `AGENTS.md` (this repo) and
`starter/AGENTS.md` are derived renderings kept in sync. The script ships in
`starter/` so adopters receive it via the copy-driven update (ADR-0022).

## Tasks

### The script

- [x] Write the `pwsh` regen script (portable, no Windows-only dependency): scan
      each family, regex-extract the title line + `- Date:` / `- Status:` /
      `- Tags:` / `- Implements:` bullets, sort by ordinal.
- [x] Emit the three family tables, the ADR → plans sub-index (group plans by
      `Implements:`), and the "accepted, no plan yet" backstop — stamped "as of
      <date>" — byte-for-byte matching the prose procedure's output shape.
- [x] Flag non-conformant headers (bare/bullet-less block per ADR-0026;
      title-line ordinal disagreeing with the filename slot per ADR-0028) instead
      of dropping or misfiling a row.
- [x] Validate: run it in this repo and diff its output against a hand-regen to
      confirm parity.

### The standing agent-guidance trigger

- [x] In the canonical spec (`starter/docs/working-method.md`), state the
      script-first-else-prose rule as standing agent guidance, keeping the
      user-facing trigger unchanged (ADR-0016) and noting the prose procedure
      stays normative.
- [x] Mirror the rule into the derived renderings — `AGENTS.md` (this repo) and
      `starter/AGENTS.md` — in the agent-guidance section.

### Delivery

- [x] Place the script in `starter/` (and this repo) so it reaches adopters via
      the copy-driven update (ADR-0022); confirm its location is what the
      instruction trigger keys on.
- [x] Regenerate `overview.md` on request once the mechanism is in place.
