# ADR-0026: Pin the canonical artifact-header format

- Date: 2026-07-10
- Status: accepted
- Promoted from: [Idea-0019](../ideas/0019-pin-canonical-artifact-header-format.md)
- Amends: [ADR-0011](0011-an-always-up-to-date-overview-as-a-derived-status-index.md)
- Amends: [ADR-0022](0022-every-release-ships-reliable-update-instructions.md)

## Context

Artifact header blocks drifted into **two renderings** that parse the same but
look different — bulleted (`- Status: accepted`, a Markdown list item) and bare
(`Status: accepted`, a plain paragraph line). The bulleted form is the *de facto*
canonical one: it is what the `starter/` seed ADR ships and what the overview
**refresh procedure** greps for. Yet decisions `0015`–`0025`, ideas `0006`–`0018`,
and plans `0005`–`0014` had all slipped into the bare form before it was noticed
and mechanically repaired.

The root cause is the same class as ADR-0025 (numbering): the convention lives as
**folklore, not as a stated, checkable rule.** The method pins header **field
names and meanings** (the cross-link table, the mandatory `Date:`) but **never
states the header's canonical *rendering*** — there is no header template anywhere
in `AGENTS.md` or `working-method.md`. So each new artifact is cloned from its
**nearest neighbor** rather than the starter exemplar; once one bare header slipped
in, every later sibling copied it and the drift **self-propagated**.

This is **more than cosmetic**. The refresh procedure greps `- Status:` /
`- Date:` / `- Tags:` **with the bullet**, so a bare header is **silently missed**
during regeneration — leaving a stale or wrong row in the derived `overview.md`.
The conformance check (ADR-0022) verifies `Date:` presence and overview-sync, but
**not header format**, so nothing catches the drift.

## Decision Drivers

- **Reliability** — a mis-rendered header must not silently corrupt `overview.md`.
- **Economy (#2)** — one stated template + a check, not per-artifact vigilance.
- **Consistency** — reuse the existing conformance check (ADR-0022) and the
  hardening theme of ADR-0025 rather than add a parallel mechanism.
- **Transparency (#3)** — the canonical form should be written down, not folklore.

## Considered Options

1. **Pin the header template + harden the refresh procedure + extend the
   conformance check.** *(Recommended.)*
2. **Only fix the data** (already done) and rely on agent care — rejected: it has
   already drifted across three families and will recur.
3. **Fold into ADR-0025** as a second clause — rejected as the primary record, but
   the two are siblings and may share one implementing plan.

## Decision

Take **Option 1**:

- **State a canonical header template** in the method texts (`AGENTS.md` +
  `starter/docs/working-method.md`), and confirm the `starter/` exemplars match:
  a `# Title` line, a blank line, then a **bulleted header block** — `- Date:`,
  `- Status:`, then any cross-link fields (`- Promoted to:`, `- Implements:`,
  `- Amends:`, …) and the optional `- Tags:` — each field on its own
  `-`-prefixed line.
- **Harden the overview refresh procedure** so it cannot silently miss a
  mis-rendered header — either tolerate both forms on read, or treat a bare header
  as a conformance failure rather than an invisible skip.
- **Add header-format detection to the conformance check** (ADR-0022): flag any
  artifact whose header fields are not in the canonical bulleted form — a natural
  companion to the duplicate-number check proposed in ADR-0025.

## Consequences

- The header format becomes a **stated, checkable rule**; new artifacts have a
  template to follow instead of copying a neighbor.
- Drift becomes both **less likely** (template) and **detectable** (conformance
  step), and can no longer silently corrupt `overview.md`.
- Slightly more prescriptive header guidance — a small, justified cost.
- On acceptance, reciprocal `Amended by: ADR-0026` is added to ADR-0011 and
  ADR-0022, and a plan carries the template + refresh-procedure + conformance-check
  edits into the method texts and `starter/` — possibly shared with ADR-0025's
  plan, since both harden a stated-but-unenforced convention.
