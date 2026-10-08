# Source basis for IOS-BASELINE-001

Date: 2026-10-08
Purpose: provenance for construction/evaluation of the synthetic diagnostic fixtures. These sources constrain architecture and terminology; they are not copied answer keys.

Primary/public anchors reviewed before freezing the instances:
- Apple Platform Security, current 2026 guide: secure boot, system security, app security, Data Protection, Secure Enclave.
  https://support.apple.com/en-by/guide/security/welcome/web
- Apple Platform Security — iPhone/iPad boot process.
  https://support.apple.com/en-gb/guide/security/secb3000f149/web
- Apple Platform Security — app code signing process.
  https://support.apple.com/guide/security/app-code-signing-process-sec7c917bf14/web
- Apple Platform Security — encryption and Data Protection overview.
  https://support.apple.com/guide/security-pdf/encryption-and-data-protection-overview-sece3bee0835/web
- Apple Developer Documentation — IOServiceMatching / IOServiceNameMatching.
  https://developer.apple.com/documentation/iokit/1514687-ioservicematching
  https://developer.apple.com/documentation/iokit/1514416-ioservicenamematching
- Apple OSS XNU source distribution.
  https://github.com/apple-oss-distributions/xnu
- Apple File System / File System documentation.
  https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/APFS_Guide/Introduction/Introduction.html

Design rule:
- evidence bundles are synthetic and novel;
- migrated Project Manager cases were not copied as assessment instances;
- evaluator rubrics encode only bounded expected reasoning, not hidden project-state facts;
- exact-version transfer remains something the solver must justify, not assume.
