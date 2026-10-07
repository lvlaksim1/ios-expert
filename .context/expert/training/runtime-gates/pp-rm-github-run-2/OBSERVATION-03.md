# Observation 03 — self-rearm of the current slot terminates useful continuation

Date: 2026-10-07
Gate: IOS-EXPERT-PP-RM-GITHUB-002
Status: NEGATIVE_RUNTIME_FINDING

Observed:
- a single state-driven task was instructed to rearm itself as its first tool action and then continue to GitHub;
- the task successfully updated/rearmed itself;
- the current runtime then ended without performing the GitHub transition;
- repeated self-rearm wakes did not advance the canonical gate state.

Conclusion:
- in this Scheduled-Task runtime, changing the currently executing task cannot be assumed to permit useful continuation in the same runtime;
- therefore the tested PP-RM pattern uses two alternating slots;
- each current slot first rearms the OTHER slot, then performs at most one durable GitHub transition;
- this preserves the required order: rearm -> read state -> decide -> one action -> report, without relying on self-update continuation.
