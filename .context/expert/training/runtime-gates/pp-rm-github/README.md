# PP-RM / GitHub infrastructure gate 001

Purpose: prove the execution semantics required by EXPERT-TRAINING-v0.2 without touching project/product state.

## Phase 1 — concurrent reservation
Two independent scheduled workers A/B target the same canonical state and logical step.
Only a successful SHA-fenced update of `state.json` from `CONCURRENCY_READY` to `CONCURRENCY_IN_PROGRESS` authorizes the effect.
A loser must perform no effect.

The winner creates exactly one logical effect marker and separate evidence.
A verifier, not the winner, creates acceptance.

## Phase 2 — injected unknown outcome
After Phase 1 acceptance, an independent dispatcher reserves `crash-step-001`, creates exactly one effect marker, then intentionally stops before evidence/acceptance/final state transition.
A later recovery worker must reconcile GitHub state, observe the existing effect, and must not repeat it. It creates recovery evidence and acceptance.
A final verifier performs read-only classification.

## Pass criteria
- exactly one accepted concurrency attempt;
- exactly one `atomic-step-001` logical effect;
- loser never creates an effect;
- crash effect exists once;
- recovery does not recreate crash effect;
- evidence and acceptance are separate durable records;
- canonical state ends `GATE_PASS_CANDIDATE`;
- final independent verifier observes a coherent topology;
- every scheduled prompt requires >=5 seconds between sequential GitHub requests.

This gate proves only the tested GitHub/Scheduled-Task execution contour. It does not prove hidden-assessment access separation.
