# Overview

A derived status index over all ideas, decisions, and plans — a plain
*to-do / what's-done* list. It is **regenerated wholesale from the artifact
headers** (never hand-patched) and stamped with the moment it was true. The
artifacts themselves are the source of truth; this file is a convenience
snapshot. Keeping it current is the agent's responsibility (see
[ADR-0011](decisions/0011-an-always-up-to-date-overview-as-a-derived-status-index.md)).

You can ask the agent to **regenerate the overview** at any time.

**As of: 2026-07-11 (updated)**

## Ideas

| Name | Created | State | Tags |
|------|---------|-------|------|
| [0001 A generic way to work on projects](ideas/0001-a-generic-way-to-work-on-projects.md) | 2026-06-28 | promoted | |
| [0002 Adopting the-way in other project repos](ideas/0002-adopting-the-way-in-other-repos.md) | 2026-06-28 | promoted | |
| [0003 An always up-to-date overview.md](ideas/0003-an-always-up-to-date-overview.md) | 2026-06-28 | promoted | |
| [0004 Using decision-trail in your own repo should be as easy as possible](ideas/0004-using-decision-trail-in-your-own-repo-should-be-easy.md) | 2026-06-28 | promoted | |
| [0005 The name "the-way" may be too pretentious to share](ideas/0005-renaming-the-way.md) | 2026-06-28 | promoted | |
| [0006 Documentation flaw — sync and audience](ideas/0006-documentation-flaw-sync-and-audience.md) | 2026-06-28 | promoted | |
| [0007 Artifact numbering is ordinal only — always use the next free slot](ideas/0007-artifact-numbering-is-ordinal-only.md) | 2026-06-29 | promoted | |
| [0008 Overview regeneration should be more economical](ideas/0008-overview-regeneration-should-be-more-economical.md) | 2026-06-29 | promoted | |
| [0009 Cross-cutting concerns have no navigable home — is a "spine" missing?](ideas/0009-cross-cutting-concerns-have-no-home.md) | 2026-07-03 | promoted | |
| [0010 A human-friendly travel diary for the human-machine interface](ideas/0010-a-human-friendly-travel-diary.md) | 2026-07-03 | promoted | |
| [0011 Stamp the overview with a date-time, not just a date](ideas/0011-stamp-overview-with-date-time.md) | 2026-07-03 | dropped | |
| [0012 The confirmation guard is never perfectly safe — scope lives in the "yes"](ideas/0012-confirmation-guard-never-perfectly-safe.md) | 2026-07-03 | promoted | |
| [0013 Intermediate artifacts — a scratch persistence layer for execution](ideas/0013-intermediate-artifacts-a-scratch-layer-for-execution.md) | 2026-07-03 | promoted | |
| [0014 Every change must ship precise, agent-reliable update instructions for older adopters](ideas/0014-every-change-ships-reliable-update-instructions.md) | 2026-07-03 | promoted | |
| [0015 Promote and teach the method — a didactical guide, and a German translation](ideas/0015-promote-and-teach-the-method.md) | 2026-07-05 | promoted | |
| [0016 Status vocabulary is per-family — guard against cross-contamination](ideas/0016-status-vocabulary-guard-per-family.md) | 2026-07-10 | promoted | |
| [0017 A large idea has no home to decompose into — is a "container" idea missing?](ideas/0017-decomposing-a-large-idea-container-gap.md) | 2026-07-10 | promoted | |
| [0018 Harden next-slot numbering so it can't collide](ideas/0018-harden-slot-numbering-against-collisions.md) | 2026-07-10 | promoted | |
| [0019 Pin the canonical artifact-header format so it can't drift](ideas/0019-pin-canonical-artifact-header-format.md) | 2026-07-10 | promoted | |
| [0020 Advice and means to run the method economically and token-saving](ideas/0020-use-the-method-economically-and-token-saving.md) | 2026-07-10 | decomposed | |
| [0021 Shrink the always-loaded agent instruction weight](ideas/0021-shrink-the-always-loaded-agent-instruction-weight.md) | 2026-07-11 | promoted | |
| [0022 Render the method's fixed procedures as optional skills](ideas/0022-render-fixed-procedures-as-optional-skills.md) | 2026-07-11 | seed | |
| [0023 Name the resume-time economy practices as a stated discipline](ideas/0023-name-the-resume-time-economy-practices-as-a-discipline.md) | 2026-07-11 | seed | |
| [0024 Pin the title-line format so the ordinal is always visible in the H1](ideas/0024-pin-the-title-line-format-ordinal-in-h1.md) | 2026-07-11 | promoted | |

## Decisions

| Name | Created | State | Tags |
|------|---------|-------|------|
| [0001 Record decisions as ADRs](decisions/0001-record-decisions-as-adrs.md) | 2026-06-28 | accepted | |
| [0002 Capture an idea as a small markdown file](decisions/0002-capture-an-idea-as-a-small-markdown-file.md) | 2026-06-28 | accepted | |
| [0003 A proposal is an ADR in the `proposed` status](decisions/0003-a-proposal-is-an-adr-in-the-proposed-status.md) | 2026-06-28 | accepted | |
| [0004 A plan carries a decision into action](decisions/0004-a-plan-carries-a-decision-into-action.md) | 2026-06-28 | accepted | |
| [0005 Repo layout and cross-linking conventions](decisions/0005-repo-layout-and-cross-linking-conventions.md) | 2026-06-28 | accepted | |
| [0006 A single tool-agnostic entry point (AGENTS.md)](decisions/0006-a-single-tool-agnostic-entry-point.md) | 2026-06-28 | accepted | |
| [0007 Seal the method: AGENTS.md is the single source of truth](decisions/0007-seal-the-method-agents-md-single-source-of-truth.md) | 2026-06-28 | accepted | |
| [0008 Adopt the-way via a copied starter skeleton](decisions/0008-adopt-the-way-via-a-copied-starter-skeleton.md) | 2026-06-28 | accepted | |
| [0009 Adopters use conventional, unbranded locations](decisions/0009-adopters-use-conventional-unbranded-locations.md) | 2026-06-28 | accepted | |
| [0010 Adopters keep the method text in `working-method.md`](decisions/0010-adopters-keep-the-method-text-in-working-method-md.md) | 2026-06-28 | accepted | |
| [0011 An `overview.md` status index, regenerated as a dated snapshot](decisions/0011-an-always-up-to-date-overview-as-a-derived-status-index.md) | 2026-06-28 | accepted | |
| [0012 Promotion carries a reciprocal `Promoted from:` back-link](decisions/0012-promotion-carries-a-reciprocal-promoted-from-back-link.md) | 2026-06-28 | accepted | |
| [0013 Rename the method from "the-way" to "decision-trail"](decisions/0013-rename-the-way-to-decision-trail.md) | 2026-06-28 | accepted | |
| [0014 Single-source method renderings; split into guide / spec / agent guidance](decisions/0014-sync-method-renderings-and-separate-audiences.md) | 2026-06-28 | accepted | |
| [0015 Artifact numbering is ordinal only — always use the next free slot](decisions/0015-artifact-numbering-is-ordinal-only.md) | 2026-06-29 | accepted | |
| [0016 Overview regeneration on explicit request only](decisions/0016-overview-regeneration-on-explicit-request-only.md) | 2026-06-29 | accepted | |
| [0017 An optional `Tags:` axis for cross-cutting navigation](decisions/0017-optional-tags-axis-for-cross-cutting-navigation.md) | 2026-07-03 | accepted | |
| [0018 A travel diary for the human-machine interface](decisions/0018-a-travel-diary-for-the-human-machine-interface.md) | 2026-07-03 | accepted | |
| [0019 Teach that the confirmation guard is never perfectly safe](decisions/0019-confirmation-guard-never-perfectly-safe.md) | 2026-07-03 | accepted | |
| [0020 Intermediate artifacts — a scratch persistence layer for execution](decisions/0020-intermediate-artifacts-a-scratch-layer-for-execution.md) | 2026-07-03 | accepted | |
| [0021 A single adopter on-ramp covering fresh, inject, and update](decisions/0021-a-single-adopter-on-ramp-fresh-inject-update.md) | 2026-07-03 | accepted | |
| [0022 Every release ships precise, agent-reliable "bring me current" instructions](decisions/0022-every-release-ships-reliable-update-instructions.md) | 2026-07-04 | accepted | |
| [0023 Promote and teach the method — a didactical guide](decisions/0023-promote-and-teach-the-method.md) | 2026-07-05 | accepted | |
| [0024 Status vocabulary is per-family — state entry status and guard against cross-contamination](decisions/0024-status-vocabulary-guard-per-family.md) | 2026-07-10 | accepted | |
| [0025 Harden next-slot numbering with a collision-proof procedure](decisions/0025-harden-slot-numbering-with-collision-proof-procedure.md) | 2026-07-10 | accepted | |
| [0026 Pin the canonical artifact-header format](decisions/0026-pin-canonical-artifact-header-format.md) | 2026-07-10 | accepted | |
| [0027 A `decomposed` status for a budded parent idea](decisions/0027-a-decomposed-status-for-a-budded-parent-idea.md) | 2026-07-10 | accepted | |
| [0028 Pin the title-line format so the ordinal is always visible in the H1](decisions/0028-pin-the-title-line-format-ordinal-in-h1.md) | 2026-07-11 | accepted | |
| [0029 Shrink the always-loaded agent instruction weight](decisions/0029-shrink-the-always-loaded-agent-instruction-weight.md) | 2026-07-11 | accepted | |

## Plans

| Name | Created | State | Tags |
|------|---------|-------|------|
| [0001 Build overview.md and the mandatory `Date:` convention](plans/0001-build-overview-and-mandatory-date.md) | 2026-06-28 | done | |
| [0002 Make the `Promoted` link reciprocal](plans/0002-make-the-promoted-link-reciprocal.md) | 2026-06-28 | done | |
| [0003 Rename the-way to decision-trail](plans/0003-rename-the-way-to-decision-trail.md) | 2026-06-28 | done | |
| [0004 Split the method text into guide / spec / agent guidance](plans/0004-split-method-into-guide-spec-agent-guidance.md) | 2026-06-28 | done | |
| [0005 Add explicit numbering rule to method texts](plans/0005-add-explicit-numbering-rule-to-method-texts.md) | 2026-06-29 | done | |
| [0006 Update overview regeneration rule to explicit-request only](plans/0006-update-overview-regeneration-rule.md) | 2026-06-29 | done | |
| [0007 Add the optional `Tags:` axis for cross-cutting navigation](plans/0007-add-optional-tags-axis.md) | 2026-07-03 | done | |
| [0008 Ship the travel diary as an optional human-facing companion](plans/0008-ship-the-travel-diary.md) | 2026-07-03 | done | |
| [0009 Teach that the confirmation guard is never perfectly safe](plans/0009-teach-confirmation-guard-fragility.md) | 2026-07-03 | done | |
| [0010 Ship intermediate artifacts as an optional execution-stage companion](plans/0010-ship-intermediate-artifacts.md) | 2026-07-03 | done | |
| [0011 Ship the adopter on-ramp (`adopting.md`) and the release-migration contract](plans/0011-ship-adopter-on-ramp-and-migration-contract.md) | 2026-07-03 | done | |
| [0012 Carry ADR-0022 into the method — copy-driven update, manifest, in-repo pointer, conformance check](plans/0012-carry-adr-0022-into-the-method.md) | 2026-07-04 | done | |
| [0013 Promote and teach the method — didactical guide with Mermaid visuals](plans/0013-promote-and-teach-the-method.md) | 2026-07-05 | done | |
| [0014 Make the per-family status vocabulary explicit and guarded](plans/0014-status-vocabulary-guard-in-method-texts.md) | 2026-07-10 | done | |
| [0015 Harden next-slot numbering with a collision-proof procedure](plans/0015-harden-slot-numbering-procedure.md) | 2026-07-10 | done | |
| [0016 Pin the canonical artifact-header format](plans/0016-pin-canonical-artifact-header-format.md) | 2026-07-10 | done | |
| [0017 Carry the `decomposed` idea status into the method](plans/0017-carry-decomposed-status-into-the-method.md) | 2026-07-10 | done | |
| [0018 Pin the title-line format so the ordinal is always visible in the H1](plans/0018-pin-the-title-line-format-ordinal-in-h1.md) | 2026-07-11 | done | |
| [0019 Shrink the always-loaded agent instruction weight](plans/0019-shrink-the-always-loaded-agent-instruction-weight.md) | 2026-07-11 | done | |
