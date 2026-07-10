# Idea: advice and means to run the method economically and token-saving

- Date: 2026-07-10
- Status: seed

## Observation

**Economy** (promise #2) is a promise the method makes about *itself* — cheap to
write, cheap to resume. But the method offers no explicit guidance on how to
*operate* it cheaply, and today most operators are AI agents whose real running
cost is **tokens and context budget**. A naive agent resuming a trail may read
every idea, decision, and plan in full before doing anything — the opposite of
economical — even though the artifacts are deliberately structured so it need
not.

The mechanics to work cheaply already exist; what is missing is *advice that
names them as a token-saving discipline*:

- **Greppable, fixed field names** (`Status:`, `Date:`, `Implements:`,
  `Promoted to:`, …) mean an agent can grep headers instead of reading bodies.
- **`overview.md` is a derived index** — a resuming agent should read *it* first,
  not the whole trail, and only open the artifacts it actually needs.
- **`overview.md` regeneration scans only headers** (`# N. Title` + the header
  block), never full bodies (already stated in ADR-0011 / idea 0008, but as a
  refresh procedure, not as a general economy principle).
- **The travel diary** exists precisely so a human — or agent — can catch up from
  one prose file instead of synthesizing across every artifact.

## Desired advice / means (sketch)

Collect the cheap-to-operate practices into stated guidance, e.g.:

- **Resume via the index, not the corpus.** Start from `overview.md` (and/or the
  travel diary); open individual artifacts only on demand.
- **Grep headers, not bodies.** Use the fixed field vocabulary to answer state
  and cross-link questions without reading prose.
- **Targeted reads.** Read the section you need (view ranges / header blocks)
  rather than whole files.
- **Keep artifacts terse.** Terse artifacts are cheaper to write *and* to resume
  — economy compounds on both ends.
- **Regenerate from headers only.** Never re-read bodies to rebuild `overview.md`.
- Possibly a short **"working economically" checklist** an agent can follow at
  session start.

## Open questions

- Where does this guidance live? Advice-only in `guide.md`, a discipline in the
  `## Agent operating guidance` section of `AGENTS.md`, and/or its own ADR?
- Is this purely advisory (no mechanism change), or does it motivate a small
  mechanism — e.g. a stable "read me first" ordering, or a machine-terse resume
  header — to make cheap operation the default path?
- Does it belong in the canonical `starter/docs/working-method.md` so adopters
  inherit it, or is it home-repo commentary?
- How does it relate to the travel diary (0010) and the economical-overview idea
  (0008) — sibling advice, or should those be cross-referenced?
