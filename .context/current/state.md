# Current state

Updated: 2026-10-07

- agent: `ios-expert`
- role: persistent Expert
- specialization: iOS/Darwin systems research and engineering
- service-agent base: installed
- Expert Base overlay: original install `0.1.0-research` from `lvlaksim1/expert-base@3d61aefda1b2e617c365a92f3b2a33a648f832f5`; execution-invariant layer synchronized from `expert-base` `0.1.1-research` on 2026-10-07
- migration source: `lvlaksim1/iOS-Research-Runtime manager-state@bd55608c6c411e86014f9fbd2feaab999812ca13`
- migration: completed as G0 candidate import
- profession map: v0.3.0; Owner-approved initial baseline after external-source reconciliation + two thought-validation passes
- target professional profile: v0.2; Owner-approved initial baseline
- action cards: candidate v0.1 created for mandatory baseline actions
- public baseline assessment spec: v0.2 design complete; hidden assessment-instance not created
- training baseline materialized: all 8 locked `EXPERT-TRAINING-v0.2` files present with expected blob SHAs
- execution invariants: active; `RULE_KNOWN` / `RULE_APPLIED` / `COMPLIANCE_CHECKED` separated; known-but-unapplied mandatory rule = `EXECUTION_INVARIANT_VIOLATION`
- training standard evolution: `EXPERT-TRAINING-v0.3-DRAFT-DELTA` recorded in Supervisor; training lock remains v0.2 until integration and re-audit
- confirmed skills: none yet
- confirmed competence: none yet
- operational entrustment: D0
- PP-RM/GitHub atomicity/recovery gate: run 1=`NOT_PROVEN` with single-winner reservation proven; run 2 wave 1 scheduled under `one tick = one durable transition`
- PP-RM/GitHub run 2 wave 1: T1 reserve -> T2 effect -> T3 evidence -> T4 independent acceptance -> T5 crash-step reservation; each fail-closed and limited to one durable GitHub mutation
- assessment preparation/solver separation: architecture accepted; runtime proof pending (`P ∩ S = ∅`)
- real summative assessment: BLOCKED until PP-RM transition gate and runtime-separation canary pass
- lifecycle state: `INFRASTRUCTURE_GATE_RUN_2_WAVE_1_SCHEDULED`

The source Project Manager remains a separate active/project-local identity and was not replaced or modified.
