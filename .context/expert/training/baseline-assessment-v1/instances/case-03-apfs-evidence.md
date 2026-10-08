# BASE-03 — APFS / root mount / evidence discipline

assessment_id: IOS-BASELINE-001
case_id: BASE-03
prepared_by_runtime: IOSBASE-P-20261008T0300-7c4e21a9
coverage: D1,D2,D3,D4,H1,H3,H4,I4
risk: R0
mode: read-only reasoning

## Environment
Two synthetic APFS container images produced from the same source fixture. No live user data.

## Evidence bundle
Source image S:
- container superblock checksum valid;
- object map traversal valid;
- system volume UUID = SYS-111;
- preboot metadata references SYS-111;
- read-only checker reports no structural checksum error.

Rebuilt image R:
- container superblock checksum valid;
- object map traversal valid;
- system volume UUID = SYS-222;
- preboot metadata still references SYS-111;
- extent totals differ from S by a small amount;
- read-only checker reports no checksum error;
- boot-time mount path reports `root volume reference not resolved`.

Additional facts:
- public Apple documentation establishes APFS as the platform filesystem and describes high-level features, but does not document every iOS on-disk boot invariant used here.
- no evidence shows that the small extent-total difference is itself the cause of mount failure.
- no write/mutation test has been performed.

## Task
1. Identify the strongest first causal hypothesis supported by the bundle and distinguish it from merely correlated differences.
2. Explain which claims are official/documented and which are empirical in this fixture.
3. Propose a read-only sequence to discriminate UUID/preboot reference inconsistency from extent-accounting issues.
4. State what evidence would be required before changing writer/allocation semantics.
5. Explain why valid checksums/object-map traversal do not by themselves prove boot-mount correctness.
6. State what can and cannot be generalized from this synthetic fixture to another iOS build/device.
7. Mark facts, hypotheses and unknowns.
