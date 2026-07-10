# Plan: teach that the confirmation guard is never perfectly safe

- Date: 2026-07-03
- Status: done
- Implements: [ADR-0019](../decisions/0019-confirmation-guard-never-perfectly-safe.md)

## Goal

Add a short reflective prose passage to the human guide teaching that the
confirmation guard is never perfectly safe — a "yes" carries ambiguous scope, and
scope is a shared responsibility — plus a one-sentence scope reminder in the agent
operating guidance. **Version stays v2.4**: no bump, no `CHANGELOG.md` entry
(batched with anticipated follow-on ideas).

## Design notes (placement)

- The reflective passage is **didactic** → canonical `starter/docs/guide.md`,
  regenerated wholesale into this repo's derived `guide.md` (ADR-0014, paths-only
  delta). It goes where the confirmation guard / how the method is used is
  discussed.
- The one-sentence reminder is an **operating instruction** → the existing
  confirmation-guard bullet in this repo's `AGENTS.md` and in `starter/AGENTS.md`.
- No `CHANGELOG.md` change and no provenance bump this time.

## Tasks

### Guide (canonical + derived)
- [x] Add the reflective prose passage to `starter/docs/guide.md`, near the
      confirmation-guard / usage discussion: the guard is a core safety mechanism
      but never perfectly safe; a "yes"/"ok" carries ambiguous scope (this step vs.
      the batch it implies); step-by-step must not give a false sense of safety;
      scope is a shared responsibility — the agent names its intended scope before
      acting, the human bounds a confirmation in words when in doubt
      (*"yes, but only this single next step [...]"*).
- [x] Regenerate this repo's `guide.md` from the canonical guide (paths-only
      delta): the same passage with repo-root framing.

### Agent operating guidance
- [x] Append one sentence to the confirmation-guard bullet in this repo's
      `AGENTS.md`: before acting, name the intended scope explicitly, especially
      when a bare approval could be read as covering a larger batch.
- [x] Mirror that one sentence in `starter/AGENTS.md`.

### Overview
- [x] Regenerate `overview.md` to include idea 0012, ADR-0019, and this plan;
      restamp "as of".

## Out of scope

- Any version bump or `CHANGELOG.md` entry (v2.4 held; batched for a later release).
- Hardening the guard into an enforced scope-echo mechanic (left as a future
  decision by ADR-0019 if prose proves insufficient).
