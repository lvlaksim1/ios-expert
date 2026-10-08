# BASE-02 — IOKit / DeviceTree / early userland

assessment_id: IOS-BASELINE-001
case_id: BASE-02
prepared_by_runtime: IOSBASE-P-20261008T0300-7c4e21a9
coverage: C1,C2,C3,F1,F4,H1,H2,H3,H4
risk: R0
mode: read-only reasoning

## Environment
Synthetic ARM64 iOS-like boot fixture, build 23A-SYNTH-02.

## Evidence bundle
1. Kernel collection inventory contains classes named for an NVMe controller family.
2. DeviceTree snapshot contains a PCIe storage endpoint node with compatible/name properties.
3. IORegistry IODeviceTree plane contains that node.
4. IORegistry IOService plane contains the upstream PCIe bridge but no published storage-controller service below it.
5. No BSD `/dev/disk*` node is observed.
6. A later launchd job `com.example.storage-dependent` repeatedly waits for a Mach service whose server normally starts only after storage initialization.
7. There is no crash from that launchd job and no evidence that its plist is malformed.
8. Apple IOKit documentation distinguishes service matching criteria from mere class/name existence; DeviceTree-derived services may use compatible/name/model properties for matching.

## Task
1. Localize the earliest proven break in the chain DeviceTree -> provider publication -> matching/probe/start -> BSD-visible storage -> dependent userland.
2. Explain separately what is and is not proved by:
   - driver/class presence in the kernel collection;
   - DeviceTree node presence;
   - IODeviceTree plane presence;
   - absence from IOService plane;
   - absence of /dev/disk*;
   - launchd waiting.
3. Give the smallest read-only next evidence set that discriminates provider-publication failure from matching/probe/start failure.
4. Explain why fixing launchd first would or would not be justified.
5. State whether this result transfers automatically to physical hardware if obtained in virtualization, and what would be required to support transfer.
6. Mark facts, hypotheses and unknowns.
