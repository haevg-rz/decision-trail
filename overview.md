# Overview

A derived status index over all ideas, decisions, and plans — a plain
*to-do / what's-done* list. It is **regenerated wholesale from the artifact
headers** (never hand-patched) and stamped with the moment it was true. The
artifacts themselves are the source of truth; this file is a convenience
snapshot. Keeping it current is the agent's responsibility (see
[ADR-0011](decisions/0011-an-always-up-to-date-overview-as-a-derived-status-index.md)).

You can ask the agent to **regenerate the overview** at any time.

**As of: 2026-07-04**

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
| [0011 The confirmation guard is never perfectly safe — scope lives in the "yes"](ideas/0011-confirmation-guard-never-perfectly-safe.md) | 2026-07-03 | promoted | |
| [0012 Intermediate artifacts — a scratch persistence layer for execution](ideas/0012-intermediate-artifacts-a-scratch-layer-for-execution.md) | 2026-07-03 | promoted | |
| [0013 Every change must ship precise, agent-reliable update instructions for older adopters](ideas/0013-every-change-ships-reliable-update-instructions.md) | 2026-07-03 | promoted | |

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
