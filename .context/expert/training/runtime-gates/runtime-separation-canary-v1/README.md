# Runtime separation canary v1

Gate: IOS-EXPERT-RUNTIME-SEPARATION-001
Purpose: prove the concrete PP-RM runtime topology required by EXPERT-TRAINING-v0.3 without changing qualification.

This is an infrastructure canary, not a professional assessment.

Required topology:
- exactly two preparation runtimes: P1, P2;
- exactly two solving runtimes: S1, S2;
- every wake is a fresh runtime;
- durable unique runtime_id is recorded on every transition;
- the concrete task is frozen by P2 before any solver runtime participates;
- set(P) ∩ set(S) must be empty;
- verifier runs in another fresh runtime V1;
- any collision, missing predecessor, mutation conflict, or ambiguous state => NOT_PROVEN / fail closed.

Synthetic frozen task:
Sort the tokens in ascending ASCII order and join them with "-".
The concrete token list is created/frozen during preparation and is not used for any qualification claim.

No D-level, skill, competence, G-resource or professional-memory promotion is allowed.
