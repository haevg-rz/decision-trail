# 1. Adopt the-way

- Status: accepted
- Date: <YYYY-MM-DD>

## Context

This project needs a reasonable, structured, reproducible, economic way to work
that survives the end of a session and keeps its reasoning in plain markdown.

`the-way` is a generic, borrowed-standards method that provides exactly this: a
lifecycle (idea → proposal → decision → plan → execution) across three artifact
families, described in [`AGENTS.md`](../AGENTS.md).

## Decision

This project adopts **the-way at version v1.0.0** (replace with the version you
copied; see https://github.com/ckluth/the-way and its `CHANGELOG.md`).

- We work the lifecycle in `ideas/`, `decisions/`, `plans/` as described in
  `AGENTS.md`.
- This project's ADR log starts here, at 0001, and is independent of the-way's
  own construction history.

## Consequences

- Every later decision in this project is recorded as an ADR in `decisions/`,
  numbered from 0002 onward.
- To take a newer version of the-way, re-copy its `starter/AGENTS.md` (and note
  the change in a new ADR), since the method text is copied, not referenced.
