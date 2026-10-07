# PP-RM / GitHub infrastructure gate — run 2

Status: RUNNING
Gate: IOS-EXPERT-PP-RM-GITHUB-002

Run 1 is preserved unchanged and contributes the already-observed single-winner SHA-fenced reservation property.

Run 2 tests the missing property: reliable continuation across fresh runtimes when each tick performs only one durable transition.

## Tick chain
T1 reserve normal step.
T2 create normal effect.
T3 create separate normal evidence.
T4 create separate independent acceptance.
T5 reserve crash/unknown-outcome step.
T6 create crash effect and terminate without confirmation.
T7 reconcile existing crash effect without repeating it and write one recovery/acceptance record.
T8 read-only final verifier.

Each tick:
- is a fresh Scheduled-Task runtime;
- checks its required predecessor;
- makes no repair if predecessor is missing;
- performs at most one durable GitHub mutation;
- waits >=5 seconds between sequential external requests.

Pass requires run-1 single-winner evidence plus all run-2 topology invariants.
