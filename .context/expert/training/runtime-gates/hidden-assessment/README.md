# Runtime-separated assessment preparation gate

Gate: `IOS-EXPERT-ASSESSMENT-RUNTIME-SEPARATION-001`
Status: `ARCHITECTURE_ACCEPTED_PENDING_RUNTIME_TEST`
Date: 2026-10-07

## Requirement
For each concrete assessment instance, no runtime that participated in preparing that instance may participate in solving it.

Preparation and solving may each span multiple ticks/runtimes.

Let:
- P = set of runtime identities/ticks that prepared, refined, froze or otherwise saw the concrete task before solver release;
- S = set of runtime identities/ticks that solve the task or continue the solver chain.

Required invariant:

`P ∩ S = ∅`

For current PP-RM semantics, one tick is one fresh execution runtime.

## Meaning
This is a runtime-independence requirement, not a claim of absolute repository secrecy. It prevents the same runtime from both constructing a task around its own context and then receiving credit for solving that task.

The concrete task may be prepared over P1 -> P2 -> ... -> Pn and solved over S1 -> S2 -> ... -> Sm, provided no runtime identity occurs in both sets.

## Additional rules
- the assessment specification and criteria may be known before the attempt;
- the concrete assessment instance is frozen before the first solver runtime;
- after freeze, preparer runtimes cannot join the solver chain;
- solver runtimes cannot retroactively become preparers for the same instance;
- evaluation may be performed by a third disjoint runtime chain E;
- all runtime identities participating in P, S and E are durably recorded with the assessment instance;
- a runtime identity collision invalidates the affected assessment instance;
- project-manager historical cases may inspire preparation, but the concrete task must require new work rather than verbatim replay.

## Stronger isolation
A separate technical access boundary may still be required later for high-risk certification or where leakage through shared storage would materially invalidate the assessment. It is not a prerequisite for the initial baseline diagnosis under this Owner-approved runtime-separation model.

## Next proof
Run a canary assessment lifecycle with:
1. at least two preparation ticks;
2. at least two solver ticks;
3. durable runtime/tick IDs;
4. automatic set-intersection verification.
