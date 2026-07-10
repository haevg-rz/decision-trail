# Idea: cross-cutting concerns have no navigable home — is a "spine" missing?

- Date: 2026-07-03
- Status: promoted
- Promoted to: [ADR-0017](../decisions/0017-optional-tags-axis-for-cross-cutting-navigation.md)

## Observation

As the number of decisions and the number of parallel threads grow, a gap
appears: the **cross-cutting, shared aspects** of the decisions have nowhere to
live, and no way to be navigated as a whole. The connective tissue — the
standing invariants, principles, and concerns that span many ADRs — has to be
reconstructed by reading every ADR in order (O(n)).

`overview.md` cannot serve here, and by construction never will. It is a
*derived, wholesale-regenerated snapshot* (ADR-0011) holding only
`name / date / state` per artifact. Its virtue is that it is **never authored**
and carries **no synthesis**. The thing that feels missing is the opposite: an
authored, cross-cutting *synthesis* — a "spine."

The human's question is therefore twofold:

1. Should there be a **spine concept**?
2. Or would that be **over-engineering** that destroys the still lightweight,
   straightforward decision-trail (2.2)?

## Framing — three things are actually being conflated

- **Content**: a cross-cutting concern *is a decision*. "Mandatory `Date:`"
  (ADR-0011) and "ordinal-only numbering" (ADR-0015) are already standing
  invariants recorded as ADRs. So the *content* of a spine already has a home:
  `decisions/`.
- **Connective tissue**: the cross-link graph (`Amends` / `Superseded by` /
  `Implements` / `Promoted from`) *is* a partial spine already. The pain is that
  reading it is O(n), not that it is missing.
- **Navigation**: what is genuinely absent is a *view* that re-slices the
  existing artifacts along a shared-theme axis, so parallel threads become
  findable ("everything touching adoption / cross-linking / rendering-sync").

The gap is largely **navigational**, not conceptual.

## Candidate directions

1. **No spine (record the rejection).** Decide explicitly that cross-cutting
   concerns are ADRs, full stop; reading `decisions/` in order is the spine.
   Cheapest; preserves the contract untouched. Recording *why not* is itself
   valuable.

2. **A derived `Themes:` / `Topics:` axis.** Add an optional, greppable header
   field to ideas/decisions/plans; extend the *derived* overview with a
   "by theme" grouping. Still regenerated wholesale, still never hand-patched,
   still zero synthesis — it just re-slices existing headers along a second
   axis. Closes the *navigation* gap while honoring Economy (#2) and
   Transparency (#3).

3. **A single "principles" ADR as one front door.** Standing principles get one
   ADR that other ADRs `Amend` over time — a spine expressed inside the existing
   vocabulary, no new artifact type.

4. **A hand-authored `spine.md` document.** A fourth artifact family holding
   authored synthesis. **Likely over-engineering**: it drifts the moment any
   decision changes, reintroducing exactly the disease the *derived* overview
   was designed to cure (ADR-0011). This is the one option that actively fights
   the contract.

## Open questions

- Is the felt gap really *navigation* (findability across threads), or genuinely
  *content* that ADRs cannot hold?
- Can any spine stay **derived**, or does synthesis inherently require authoring
  (and therefore drift)?
- Does adding a `Themes:` axis erode "straightforward," or is one optional field
  cheap enough to stay in-spirit?
- Should the answer differ between the method's own repo and adopting repos?
- Borrow, don't invent (#8): is there a portable prior art to lean on (e.g.
  arc42 "cross-cutting concepts")?
