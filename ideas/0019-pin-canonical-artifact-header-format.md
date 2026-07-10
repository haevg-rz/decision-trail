# Idea: pin the canonical artifact-header format so it can't drift

- Date: 2026-07-10
- Status: promoted
- Promoted to: [ADR-0026](../decisions/0026-pin-canonical-artifact-header-format.md)

## Observation

Artifact header blocks drifted into **two renderings** that parse the same but
look different:

- **Bulleted:** `- Status: accepted` (a Markdown list item), and
- **Bare:** `Status: accepted` (a plain paragraph line).

The bulleted form is the *de facto* canonical one — it is what the `starter/` seed
ADR ships (`- Status:` / `- Date:`) and what the overview **refresh procedure**
greps for. Yet decisions `0015`–`0025`, ideas `0006`–`0018`, and plans
`0005`–`0014` had all slipped into the bare form before it was noticed and
mechanically repaired.

The root cause is the same class as the numbering bug (idea 0018 → ADR-0025): the
convention lives as **folklore, not as a stated, checkable rule.** The method
pins header **field names and meanings** (the cross-link table, the mandatory
`Date:`) but **never states the header's canonical *rendering*** — there is no
"here is the header template" anywhere in `AGENTS.md` or `working-method.md`. So
each new artifact is cloned from its **nearest neighbor** rather than from the
starter exemplar; once one bare header slipped in, every later sibling copied it
and the drift **self-propagated**.

## Why this is more than cosmetic

The overview **refresh procedure** greps `- Status:` / `- Date:` / `- Tags:`
**with the bullet**. A bare-style header is therefore **silently missed** during
regeneration — so the drift can actually leave a stale or wrong row in the derived
`overview.md`, not merely look inconsistent. The conformance check (ADR-0022)
verifies `Date:` presence and overview-sync, but **not header format**, so nothing
catches the drift.

## Candidate direction

Turn the header convention from folklore into a stated, checkable rule:

- **State a canonical header template** in the method texts (`AGENTS.md` +
  `starter/docs/working-method.md`) and confirm the `starter/` exemplars match it:
  a `# Title` line, then a bulleted header block (`- Date:`, `- Status:`, then any
  cross-link fields), each field on its own `-`-prefixed line.
- **Make the overview refresh procedure robust** so it does not silently miss a
  mis-rendered header — either by tolerating both forms when reading, or by
  treating a bare header as a conformance failure rather than an invisible skip.
- **Add header-format detection to the conformance check** (ADR-0022): flag any
  artifact whose header fields are not in the canonical bulleted form (a natural
  companion to the duplicate-number check proposed in ADR-0025).

## Framing

A use-phase refinement of the method, made decision-trail as an ADR. A close
sibling of ADR-0025 (both harden a stated-but-unenforced convention); the two
could share one implementing plan, or even be considered for merging.

## Open questions

- One ADR covering "pin the header format", or fold it into ADR-0025's
  hardening theme?
- Should the refresh procedure **tolerate** both renderings on read (robust but
  permissive), or **reject** the bare form as non-conformant (strict but noisier)?
- How much header structure should be mandated vs left free — e.g. is field
  *order* part of the canonical template, or only the bullet rendering?
- Is a lightweight, agent-run conformance check enough, or is a mechanical
  linter/script warranted for header format?
