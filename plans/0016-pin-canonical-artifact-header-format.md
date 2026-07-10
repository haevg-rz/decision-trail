# Plan: pin the canonical artifact-header format

- Date: 2026-07-10
- Status: done
- Implements: [ADR-0026](../decisions/0026-pin-canonical-artifact-header-format.md)

## Goal

Carry [ADR-0026](../decisions/0026-pin-canonical-artifact-header-format.md) into
the method texts. The header block drifted into two renderings that parse the
same but look different — bulleted (`- Status:`) and bare (`Status:`) — and the
overview **refresh procedure** greps the bulleted form, so a bare header is
**silently missed**, leaving a stale row in the derived `overview.md`. The root
cause is the same class as ADR-0025: the convention lives as folklore, not as a
stated, checkable rule. Fix it by (a) **stating a canonical header template** in
both method texts, (b) **hardening the refresh procedure** so a mis-rendered
header can't silently corrupt `overview.md`, and (c) **adding header-format
detection to the conformance check** (ADR-0022). Close sibling of ADR-0025 /
plan 0015; keep both renderings in sync (ADR-0014) and ship as a release whose
behavioral migration is "none" (the wording reaches adopters via the copy-driven
"bring me current" update, ADR-0022).

## Tasks

- [x] **Canonical method body — header template.** In
      `starter/docs/working-method.md`, near the header-field guidance (the
      mandatory `Date:` / cross-link vocabulary), state the **canonical header
      template**: a `# Title` line, a blank line, then a **bulleted header block**
      — `- Date:`, `- Status:`, then any cross-link fields (`- Promoted to:`,
      `- Implements:`, `- Amends:`, …) and the optional `- Tags:` — each field on
      its own `-`-prefixed line.
- [x] **Canonical agent guidance — header template.** Add/adjust a bullet in the
      "Agent operating guidance" list of `starter/AGENTS.md` (and the repo-root
      `AGENTS.md`) stating the bulleted-header rule and cross-referencing
      ADR-0026.
- [x] **Confirm the `starter/` exemplars match.** Verify the seed ADR
      (`starter/docs/decisions/0001-adopt-decision-trail.md`) and any other
      shipped exemplars use the canonical bulleted header; fix if not.
- [x] **Harden the overview refresh procedure.** In the refresh-procedure text
      (`AGENTS.md` + `starter/docs/working-method.md`, and the mirror in
      `starter/AGENTS.md`), make it robust to a mis-rendered header — either
      tolerate both forms on read, or treat a bare header as a conformance
      failure rather than an invisible skip — so drift can no longer silently
      corrupt `overview.md`.
- [x] **Conformance check — header-format detection.** In `adopting.md`, add a
      **header-format** step to the "Conformance check" list: flag any artifact
      whose header fields are not in the canonical bulleted form. Keep the check
      pure agent do-guidance (no script); site it beside the ADR-0025
      duplicate-number step.
- [x] **Regenerate the derived rendering.** Regenerate the method body of the
      repo-root `AGENTS.md` from `starter/docs/working-method.md` (section
      `## The contract` through `## How to start working`), applying the standard
      deltas (repo-root paths, construction-ADR refs, no provenance citation),
      and carry the header-template + refresh-procedure edits and the
      agent-guidance bullet there too. Do **not** touch the preamble or the
      non-derived guidance framing.
- [x] **Provenance bump.** Bumped the `Based on decision-trail vX.Y` citation to
      **v2.10** in both `starter/` renderings (`starter/docs/working-method.md` and
      `starter/docs/guide.md`) and the adopter hand-off `starter/AGENTS.md` (shared
      with plan 0015).
- [x] **CHANGELOG + release.** Added the ADR-0026 entry to `CHANGELOG.md`
      `## [2.10.0]` (canonical header template + hardened refresh procedure +
      header-format conformance step), with **`Adopter migration: none`**.
- [x] **Regenerate `overview.md`** after all edits are done (idea 0019 →
      `promoted`, ADR-0026 → `accepted`, this plan → state updated).
