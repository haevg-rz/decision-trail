# Idea 0023: name the resume-time economy practices as a stated discipline

- Date: 2026-07-11
- Status: promoted
- Parent: [0020](0020-use-the-method-economically-and-token-saving.md)
- Promoted to: [ADR-0030](../decisions/0030-resume-economy-as-a-human-facing-guide-discipline.md)

## Why this budded from 0020

This is the *resume-discipline* axis of the decomposed parent idea 0020. It is the
cost an agent pays **only when it reads the trail** — and can already avoid,
because the artifacts are deliberately structured for cheap resume. Where the
sibling ideas 0021 (shrink always-loaded weight) and 0022 (procedures as skills)
change *mechanism*, this axis is largely **advisory**: it names existing mechanics
as a token-saving discipline.

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

Most of these were settled in the 2026-07-11 discussion (see **Scoping note**
below); resolved answers are marked, with only the promote/drop call still open.

- ~~Where does this guidance live?~~ **Resolved:** `guide.md` only (human-facing,
  read on demand) — *not* the always-loaded `AGENTS.md` block, whose weight
  sibling 0021 exists to shrink.
- ~~Purely advisory, or does it motivate a small mechanism?~~ **Resolved (leaning):**
  purely advisory — human-facing resume levers, no mechanism change.
- ~~Canonical `working-method.md` (adopters inherit) or home-repo commentary?~~
  **Resolved:** advice in `guide.md`, not the canonical spec.
- ~~Relation to the travel diary (0010) and economical-overview (0008)?~~
  **Resolved:** cross-reference them rather than restate their mechanics.
- **Still open — the actual decision:** promote (as the narrowed, human-facing
  `guide.md` ADR described below) or drop as too thin?

## Scoping note (2026-07-11, from discussion)

If promoted, **narrow the scope to the human-facing resume levers** and keep the
guidance in `guide.md` only (read on demand) — *not* in the always-loaded
`AGENTS.md` block, whose weight promoted sibling 0021 exists to shrink; putting
resume-economy advice into every-session custom instructions would be
self-defeating. The valuable, human-controlled levers are:

- **How you re-open the session is the biggest lever** — "resume plan 0007, read
  its file and `overview.md`" costs a few reads; "catch me up on the project"
  invites reading the whole corpus.
- **Name the artifact, not the topic** — "what does ADR-0021 decide?" opens one
  file; "what did we decide about token weight?" searches across bodies.
- **Ask narrow** — a scoped question maps to a header grep, not a synthesis over
  everything.
- **Invest at pause-time, not resume-time** — a regenerated `overview.md` and a
  one-paragraph travel-diary chapter, written while context is fresh, make every
  future resume cheap (the diary's stated purpose, 0010).
- **Terseness is a human write/approve discipline** — you author and green-light
  artifacts; terse ones are cheaper to write *and* to resume (Economy #2).

**Explicitly exclude the agent-mechanic restatements** (grep headers vs. bodies,
header-only `overview.md` regeneration) — those are already stated in ADR-0011 /
idea 0008 and would be filler in a human guide; cross-reference them instead of
repeating them. Without this narrowing the idea risks being a raised finger
("be thrifty"); with it, it earns its own ADR.
