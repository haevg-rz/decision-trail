# Plan: add explicit numbering rule to method texts

- Date: 2026-06-29
- Status: done
- Implements: [ADR-0015](../decisions/0015-artifact-numbering-is-ordinal-only.md)

## Goal

Make the "numbers are ordinal only, always use the next free slot" rule explicit
and visible in every context where an agent or human reads the method — so the
misbehaviour that prompted ADR-0015 cannot recur.

## Tasks

- [x] Add a "Numbering" rule paragraph to `AGENTS.md` (agent operating guidance
      section or the layout/conventions section — wherever it is most likely to
      be read before creating an artifact).
- [x] Add the same rule to `starter/docs/working-method.md` so adopting repos
      inherit it.
- [x] Check `starter/AGENTS.md` (the skeleton hand-off file) and add the rule
      there too if it contains artifact-creation guidance.
- [x] Regenerate `overview.md` after all edits are done.
