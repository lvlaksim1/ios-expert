# Current state

Updated: 2026-10-07

- agent: `ios-expert`
- role: persistent Expert
- specialization: iOS/Darwin systems research and engineering
- service-agent base: `lvlaksim1/service-agent-base@ce8106cb97c18e352bb87326563d8f04a5a1bfa3`
- Expert Base overlay: synchronized to `0.1.3-research` from `lvlaksim1/expert-base@47d26b7b208155ddd196e196d1eeba7c8e0d6d53`
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
- PP-RM/GitHub atomicity/recovery gate: run 1=`NOT_PROVEN` with single-winner reservation proven; run 2=`PASS` with one-tick/one-transition, separate evidence/acceptance, and unknown-outcome reconciliation without repeat
- PP-RM/GitHub run 2 result: `RESULT.md status: PASS`; crash effect reconciled by a fresh runtime without duplicate effect
- assessment preparation/solver separation: canary `IOS-EXPERT-RUNTIME-SEPARATION-001` active; requires P1/P2 + S1/S2 fresh runtimes and `P ∩ S = ∅`
- real summative assessment: BLOCKED until runtime-separation canary `IOS-EXPERT-RUNTIME-SEPARATION-001` reaches durable PASS
- lifecycle state: `ASSESSMENT_RUNTIME_SEPARATION_CANARY_RUNNING`

The source Project Manager remains a separate active/project-local identity and was not replaced or modified.
