# Observation 01 — first scheduled contention run

Date: 2026-10-07
Gate: IOS-EXPERT-PP-RM-GITHUB-001
Status: NOT_PROVEN

Observed durable facts:
- contender B successfully performed the SHA-fenced reservation;
- canonical state moved from CONCURRENCY_READY to CONCURRENCY_IN_PROGRESS;
- reservation attempt is atomic-step-001-B;
- contender A did not replace the reservation;
- after both contender tasks completed, no effects directory existed;
- no evidence directory existed;
- no acceptance directory existed.

Interpretation:
- single-winner canonical reservation is supported by this run;
- post-reservation continuation to effect/evidence is NOT proven;
- the missing effect must not be repaired manually and cannot be credited;
- subsequent verifier must fail closed.

This is a real negative runtime result, not a specification defect by itself. A later experiment should isolate the post-reservation continuation mechanism and avoid assuming that one Scheduled-Task wake can reliably execute a multi-request chain with pacing.
