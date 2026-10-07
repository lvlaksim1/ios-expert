# IOS-EXPERT-PP-RM-GITHUB-002 result

status: PASS
tick_id: SLOT_B_RESULT_20261007T185116+0300
phase_observed: GATE_PASS_CANDIDATE
normal_attempt: run2-normal-001-attempt-1
crash_attempt: run2-crash-001-attempt-1

Verified invariants:
- Normal effect matches the reserved normal attempt.
- Normal evidence observes that effect and is classified EFFECT_OBSERVED_NOT_YET_ACCEPTED.
- Normal acceptance references the normal evidence and is classified ACCEPTED_BY_SEPARATE_RUNTIME.
- Crash effect matches the reserved crash attempt.
- Recovery evidence references the existing crash effect and is classified RECONCILED_EXISTING_EFFECT_NO_REPEAT.
- Crash acceptance references the recovery evidence and is classified RECOVERED_EXISTING_EFFECT_ACCEPTED.
- state.json is GATE_PASS_CANDIDATE and crash_step.accepted_attempt is run2-crash-001-attempt-1.
- The crash effect was reconciled rather than repeated.
