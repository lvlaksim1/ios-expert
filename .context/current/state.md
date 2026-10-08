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
- public baseline assessment spec: v0.3 prepared; concrete instances are frozen before solver runtimes and use `P ∩ S = ∅`
- training baseline materialized: `EXPERT-TRAINING-v0.3`; all 8 locked normative files synchronized from Supervisor exact blob SHAs
- execution invariants: active; `RULE_KNOWN` / `RULE_APPLIED` / `COMPLIANCE_CHECKED` separated; known-but-unapplied mandatory rule = `EXECUTION_INVARIANT_VIOLATION`
- training standard: `EXPERT-TRAINING-v0.3`; static audit PASS; runtime separation canary PASS
- confirmed skills: none yet
- confirmed competence: none yet
- operational entrustment: D0
- PP-RM/GitHub atomicity/recovery gate: run 1=`NOT_PROVEN` with single-winner reservation proven; run 2=`PASS` with one-tick/one-transition, separate evidence/acceptance, and unknown-outcome reconciliation without repeat
- PP-RM/GitHub run 2 result: `RESULT.md status: PASS`; crash effect reconciled by a fresh runtime without duplicate effect
- assessment preparation/solver separation: `IOS-EXPERT-RUNTIME-SEPARATION-001` = PASS; P1/P2 and S1/S2 unique; `P ∩ S = ∅`; verifier 18/18
- real baseline assessment: infrastructure gate unblocked; assessment instances may now run under v0.3
- lifecycle state: `BASELINE_ASSESSMENT_RUNNING`

The source Project Manager remains a separate active/project-local identity and was not replaced or modified.

- baseline assessment: `IOS-BASELINE-001` frozen at commit `50d239f4f4cf6b5a2af089072479652e8f97c26d`; 4 synthetic read-only cases; separate solver/evaluator Scheduled Task runtimes; no automatic qualification effect.
