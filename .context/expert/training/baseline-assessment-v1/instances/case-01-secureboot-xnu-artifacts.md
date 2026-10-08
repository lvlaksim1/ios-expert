# BASE-01 — Secure boot / XNU / system artifacts

assessment_id: IOS-BASELINE-001
case_id: BASE-01
prepared_by_runtime: IOSBASE-P-20261008T0300-7c4e21a9
coverage: A1,A4,B1,B2,H1,H3,I1,I2
risk: R0
mode: read-only reasoning

## Environment
- Device family: iPhone-class ARM64 device, synthetic test fixture.
- OS/artifact build label: 23A-SYNTH-01.
- The evidence bundle is deliberately synthetic but constrained to public Apple/XNU architecture.
- Do not infer behavior from another OS build unless you mark it as a hypothesis.

## Evidence bundle
1. Restore log:
   - restore ramdisk IMG4 was accepted and started.
   - device entered restore userland.
2. Normal boot log:
   - Boot ROM executed.
   - iBoot authenticated and transferred control to the kernel image.
   - XNU printed its kernel version banner.
   - early Mach initialization completed.
   - later: `panic: root device unavailable after storage wait`.
3. Artifact inventory:
   - IPSW manifest contains model-bound restore and normal-boot components.
   - kernel collection for build 23A-SYNTH-01 contains the expected storage-family driver code.
4. Public architecture anchors:
   - Apple documents a Boot ROM -> iBoot -> kernel chain of trust for modern iPhone/iPad boot.
   - XNU source tree separates Mach (`osfmk`), BSD (`bsd`) and IOKit-related code.
5. No evidence is provided that a restore/personalization server rejected this device.
6. No IORegistry or block-device evidence is included in this case.

## Task
Produce a diagnostic answer that:
1. identifies the first failure that is actually proven by this evidence;
2. separates what is proven about secure boot from what is not proven about restore/personalization;
3. explains why presence of storage driver code in a kernel collection does not prove a working runtime storage path;
4. states what XNU/source reasoning is legitimate without assuming the public source exactly equals this proprietary iOS build;
5. names the next read-only evidence you would collect before changing any boot/storage semantics;
6. explicitly labels facts, hypotheses and unknowns;
7. states which conclusions would be invalid transfers across version/device/environment boundaries.
