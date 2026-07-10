# Plan: promote and teach the method — didactical guide with Mermaid visuals

- Date: 2026-07-05
- Status: done
- Implements: [ADR-0023](../decisions/0023-promote-and-teach-the-method.md)

## Goal

Rework the guide from a *narrative introduction* into a genuinely **didactical
tutorial** — motivate the problem before the mechanics, build the lifecycle up
progressively, and walk one canonical worked example (*"add dark mode to a small
app"*) from a first idea all the way to ticking execution checkboxes. Visualize the
mechanics with **Mermaid** where a picture teaches faster than prose. Apply the
rework to **both** guide renderings (this repo's `guide.md` and
`starter/docs/guide.md`).

> **German translation dropped.** ADR-0023's second thread — a `guide.de.md` German
> translation — was attempted and then **dropped**: the first machine-drafted
> translation was clumsy and uninspiring, and refining it was judged not worth the
> cost. The file was removed and this plan trimmed accordingly (revised in place
> while still uncommitted). Translation may return as a future idea, done properly.

## Design notes (placement)

- The rework touches **documentation only** — the guides. It changes nothing in the
  contract, lifecycle, artifact families, cross-link vocabulary, `AGENTS.md` /
  `working-method.md` method bodies, or `overview.md`'s structure.
- **Two guide renderings** get the same didactical treatment (ADR-0014 pattern):
  this repo's `guide.md` and the adopter-facing `starter/docs/guide.md`. Per-context
  path/framing deltas are preserved (repo-root families here; `docs/`-prefixed for
  adopters).
- **Mermaid** is used only where it earns its place (lifecycle flow, cross-link
  vocabulary) — plain-text, GitHub-rendered, no decorative diagrams.

## Tasks

### Rework this repo's guide (`guide.md`)
- [x] Restructure `guide.md` into a didactical tutorial: (1) **motivate first** — the
      continuity/economy/transparency pain the method removes, before naming the
      eight promises; (2) **introduce the lifecycle progressively** — one stage at a
      time (idea → proposal → decision → plan → execution), each earned before the
      next; (3) **walk the canonical worked example end to end** — *"add dark mode to
      a small app"*: capture the idea, promote to a proposal/ADR, accept it, write a
      plan that `Implements:` it, execute by ticking checkboxes.
- [x] Add a **Mermaid lifecycle diagram** (stages + status transitions:
      seed→promoted→…; proposed→accepted/rejected; draft→active→done/abandoned) and a
      **Mermaid cross-link vocabulary diagram** (Parent / Promoted to↔from / Amends↔
      Amended by / Supersedes↔Superseded by / Implements), placed where they teach.
- [x] Keep it a **guide** (human-facing narrative); do not absorb the terse reference
      (`AGENTS.md`). Preserve the "read the reference next" pointer.

### Rework the adopter guide (`starter/docs/guide.md`)
- [x] Apply the same didactical rework, worked example, and Mermaid diagrams to
      `starter/docs/guide.md`, preserving adopter deltas (`docs/`-prefixed paths,
      provenance framing, no construction-ADR references).

### German translation (attempted, then dropped)
- [x] ~~Create `guide.de.md` as a derived German translation~~ — **dropped**: the
      machine-drafted first pass was clumsy and uninspiring; refining it was judged
      not worth the cost. `guide.de.md` was created then removed.

### Release
- [x] Add a `[2.8.0]` entry to `CHANGELOG.md` (Added: ADR-0023 — didactical guide
      rework with Mermaid visuals). Include the mandatory **`Adopter migration:`**
      line — required migration is **"none"**: the reworked `starter/docs/guide.md`
      reaches adopters via the copy-driven "bring me current" update (ADR-0022).
- [x] Bump the provenance citation to **v2.8** in `starter/docs/working-method.md`
      and `starter/AGENTS.md`.

### Overview
- [x] Regenerate `overview.md` to include idea 0015, ADR-0023, and this plan;
      restamp "as of".

## Out of scope

- A German translation of the guide — attempted and dropped (see above); may return
  as a future idea.
- Any change to the contract, lifecycle, artifact families, cross-link vocabulary,
  or `overview.md`'s structure — this is documentation-only.
- decision-trail's own construction as the *primary* teaching example — the worked
  example is the generic "dark mode" project; the real ADRs remain further reading.
