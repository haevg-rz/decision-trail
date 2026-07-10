# Idea: stamp the overview with a date-time, not just a date

- Date: 2026-07-03
- Status: dropped

## Why dropped

Dropped at seed (2026-07-03): the intended payoff — letting the agent *skip*
redundant regenerations — doesn't hold up, because the agent has no in-repo
"latest change" time to compare a precise stamp against (artifact `Date:` fields
are day-granular creation dates). Without that, a date-time stamp adds ceremony
without reliably preventing regeneration, so it fails its own Economy (#2)
rationale. Kept as a dated record rather than deleted.

## Observation

`overview.md` carries an `As of: <date>` stamp. Its job is to signal how current
the snapshot is (ADR-0011, reinforced by ADR-0016 when regeneration became
explicit-request-only). But a pure *date* is too coarse to prove currency: when
several artifact changes happen on the same day, the agent cannot tell from
`As of: 2026-07-03` whether the overview already reflects the latest change — so
it may **regenerate again "to be safe,"** doing work that changes nothing.

The real cost this idea targets is that **unnecessary regeneration** — a bare
date leaves the agent unable to conclude "already current, skip it," which cuts
against Economy (#2), the very promise ADR-0016 leaned on.

## Candidate direction

Change the overview's `As of:` stamp from a date to an ISO 8601 **date-time**
(e.g. `2026-07-03T13:45+02:00`) — borrowing the portable standard (#8). A precise
stamp lets the agent compare it against the latest artifact change and decide a
regeneration is **unnecessary**, avoiding redundant rewrites. Keep the change
**narrowly scoped to the stamp only**:

- The artifacts' `Date:` header fields are **creation dates**; day granularity is
  correct there and feeds the overview's *Created* column. They stay date-only.
- Only the single `As of:` line changes format, plus the wording of ADR-0011's
  convention (and the refresh procedure that emits the stamp).

This would be a use-phase refinement of the method, made decision-trail as an ADR
that **amends ADR-0011**.

## Open questions

- Does a finer stamp actually let the agent *skip* work reliably, given artifact
  files' own change times may not be tracked in-repo? (It may still need the
  human's word, or a git timestamp, to know "latest change.")
- Timezone: require an explicit offset (as ISO 8601 allows), or accept local time
  without one? An offset is unambiguous but slightly more to write.
- Is the extra ceremony of stamping a precise time each regeneration cheaper than
  the redundant regenerations it prevents (net Economy #2)?
- Does a date-time stamp sitting above date-only `Created` cells read as an
  inconsistency, or is it clearly fine because the two mean different things
  (snapshot moment vs creation day)?
