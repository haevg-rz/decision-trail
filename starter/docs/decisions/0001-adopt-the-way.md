# 1. Adopt the-way

- Status: accepted
- Date: <YYYY-MM-DD>

## Context

This project needs a reasonable, structured, reproducible, economic way to work
that survives the end of a session and keeps its reasoning in plain markdown.

`the-way` is a generic, borrowed-standards method that provides exactly this: a
lifecycle (idea → proposal → decision → plan → execution) across three artifact
families, described in [`docs/working-method.md`](../working-method.md).

## Decision

This project adopts **the-way at version vX.Y** (replace with the version you
copied; see https://github.com/ckluth/the-way and its `CHANGELOG.md`).

- We work the lifecycle in `docs/ideas/`, `docs/decisions/`, `docs/plans/` as
  described in `docs/working-method.md`.
- This project's ADR log starts here, at 0001, and is independent of the-way's
  own construction history.

## Consequences

- Every later decision in this project is recorded as an ADR in `decisions/`,
  numbered from 0002 onward.
- To take a newer version of the-way, re-copy its `starter/docs/working-method.md`
  (and note the change in a new ADR), since the method text is copied, not
  referenced.
