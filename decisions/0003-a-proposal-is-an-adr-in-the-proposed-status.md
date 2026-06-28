# 3. A proposal is an ADR in the `proposed` status

- Status: accepted
- Date: 2026-06-28
- Amends: ADR-0001 (extends the status vocabulary)

## Context

The lifecycle runs idea → proposal → decision → plan → execution (promise #4).
ADR-0002 gave the **idea** stage a home and said a matured idea is *promoted to
a proposal*. ADR-0001 gave the **decision** stage a home. But the **proposal**
stage in between was only described "partially": a proposal was loosely an ADR
with `Status: proposed`, never actually decided.

We need to settle two questions:

1. Is a proposal a *separate artifact* (its own directory/file type), or just a
   phase of the decision artifact?
2. What distinguishes the proposal phase from the accepted decision?

Relevant promises:

- **Economy** (#2): every new artifact type is a cost to learn and maintain. We
  should not add one without need.
- **Lifecycle** (#4): the hand-off idea → proposal → decision must be smooth and
  the trail continuous.
- **Agility** (#5): while a proposal is live, competing options and the reasons
  for choosing between them should be visible, so the decision can be revisited.
- **Borrow, don't invent** (#8): both Nygard ADRs (adopted in ADR-0001) and MADR
  ("Markdown Any Decision Records") already model exactly this phase.

## Decision

A proposal is **not** a separate artifact. It is an ADR in the `proposed`
status.

- There is no `proposals/` directory. Promoting an idea (ADR-0002) opens a new
  `decisions/NNNN-kebab-title.md` with `Status: proposed`. The single file then
  carries the thought across the proposal → decision boundary:
  - if accepted, its status flips to `accepted` — the proposal *becomes* the
    decision in place;
  - if it does not survive deliberation, its status flips to `rejected` and the
    file is kept as a record (append-only, Agility #5).
- **Status vocabulary** (amending ADR-0001): the allowed values are now
  `proposed`, `accepted`, `rejected`, `superseded`, `deprecated`. `rejected`
  marks a proposal that was considered and turned down.
- **Deliberation (optional MADR borrow):** when a proposal weighs competing
  options, it may include MADR's optional sections — **Decision Drivers** (the
  forces that matter) and **Considered Options** (the alternatives with their
  pros and cons) — above the **Decision** section. A straightforward decision
  with no live alternatives keeps Nygard's plain shape (Context / Decision /
  Consequences). This optional structure is the proposal stage's only
  distinction: it captures alternatives while they are still open.
- The promoting idea links to this ADR regardless of outcome; if the proposal is
  later rejected, the idea may return to `seed` or move to `dropped`.

## Consequences

- The lifecycle's first three stages now share **one** artifact family under
  `decisions/`: an ADR moves `proposed` → (`accepted` | `rejected`). No fourth
  file type is introduced (economy #2).
- The status vocabulary is defined in two places now (ADR-0001 plus this
  amendment); a reader of ADR-0001 must follow the `Amends` link to see the full
  set. This is the accepted cost of append-only records.
- Borrowing MADR's optional sections lets a proposal show its alternatives
  without forcing that weight onto simple decisions — the template scales with
  the difficulty of the choice.
- Stages still unassigned: **plan** and **execution**. Those are future ADRs.
