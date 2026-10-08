# BASE-04 — Code signing / dyld / sandbox / hardware security

assessment_id: IOS-BASELINE-001
case_id: BASE-04
prepared_by_runtime: IOSBASE-P-20261008T0300-7c4e21a9
coverage: E1,E2,E3,E4,F2,F4,G1,G2,G3,H1,H4,I3
risk: R0
mode: read-only reasoning

## Environment
Synthetic iOS-like process launch fixture. No exploit development and no policy bypass requested.

## Evidence bundle
1. Main executable:
   - structurally valid Mach-O;
   - CodeDirectory hash calculated;
   - signature validation reports valid for the main executable.
2. Embedded dynamic library:
   - signed by a different team identity than the main executable.
3. Launch trace:
   - dyld rejects mapping the embedded library because process and mapped library do not satisfy the expected signing/team policy.
   - process exits before application main executes.
4. Sandbox trace:
   - no sandbox denial is present for this launch attempt.
5. Trust-cache query:
   - the main executable's CodeDirectory hash is not shown in the supplied static trust-cache sample.
   - no evidence establishes whether another allowed trust path applies.
6. Data Protection:
   - fixture notes that the device is locked, but no file-access attempt or protection-class evidence is supplied.
7. Apple public security material distinguishes mandatory code signing, runtime sandbox/entitlements, trust mechanisms, Data Protection and Secure Enclave-backed key handling.

## Task
1. Localize the first proven launch failure and identify the layer responsible.
2. Explain why “main executable signature is valid” does not prove the process can successfully launch.
3. Explain what can and cannot be concluded about sandbox policy from the evidence.
4. Explain what the supplied trust-cache observation proves and does not prove.
5. Explain why the locked-device fact alone does not prove a Data Protection failure.
6. State the documented boundary around Secure Enclave/Data Protection that you would not exceed without evidence.
7. Give the smallest next read-only evidence needed if you had to distinguish signing/trust policy from sandbox/container policy in a later attempt.
8. Mark facts, hypotheses and unknowns.
