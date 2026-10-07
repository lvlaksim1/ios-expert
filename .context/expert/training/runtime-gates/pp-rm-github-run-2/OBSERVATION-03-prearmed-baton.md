# Observation 03 — scheduler rearm semantics and prearmed baton

Date: 2026-10-07
Gate: IOS-EXPERT-PP-RM-GITHUB-002

## Observed runtime behavior
Two variants were exercised after the normal run-2 reservation/effect/evidence/acceptance path:

1. self-rearm first;
2. partner-slot rearm first.

In both cases the Scheduled Task mutation itself succeeded, but the current runtime did not proceed to the planned GitHub transition after that scheduler mutation.

Durable evidence remained at:
- normal step reserved/effect/evidence/acceptance present;
- crash step reserved;
- crash effect absent.

Therefore the exact sequence
`wake -> mutate Scheduled Task -> continue substantive GitHub work in the same runtime`
is NOT_PROVEN and should not be relied on.

## Revised continuity property under test
A/B slots are now prearmed before either begins substantive work.

For every wake:
1. first read Scheduled Tasks;
2. prove the partner slot is already enabled and scheduled in the future;
3. only then perform at most one durable GitHub transition;
4. as the final tool action, rearm SELF for the next alternating cycle.

Thus, at the moment substantive work begins, the next independent wake is already guaranteed by the scheduler.

This is called the prearmed-baton invariant.

It is functionally aimed at the same continuity property as "rearm first": do not begin a bounded work transition unless a future recovery/continuation runtime is already scheduled.

## Status
Prearmed-baton runtime proof: RUNNING.
No qualification claim follows from this observation.
