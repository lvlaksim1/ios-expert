# Observation 02 — pre-scheduled run-2 batch

Date: 2026-10-07
Gate: IOS-EXPERT-PP-RM-GITHUB-002
Status: PRE_SCHEDULED_BATCH_INVALIDATED_BY_EXECUTION_ORDER

Observed durable facts:
- five one-time ticks were scheduled in intended logical order T1->T5;
- actual execution order did not preserve that dependency order;
- T3 and T2 executed before T1 and therefore failed closed without mutation;
- T1 later succeeded and left the canonical state at NORMAL_RESERVED for attempt run2-normal-001-attempt-1;
- no normal effect, evidence or acceptance was created by the prematurely executed ticks;
- T5/T4 could not validly advance the chain without their predecessors.

Interpretation:
- fail-closed predecessor protection worked;
- a dependency chain must not be implemented by pre-scheduling several independent future tasks and assuming execution order;
- run 2 continues from the valid T1 reservation using one self-rearming state-driven slot;
- each wake is a fresh runtime and performs one durable transition only;
- each wake rearms itself first for +5 minutes, then reads state, decides, performs one mutation and stops.
