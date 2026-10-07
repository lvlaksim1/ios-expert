# K-IOS-003 — BootKC presence != runtime binding

Тип: knowledge candidate
Класс: G0
Статус: `source-project-observed`

## Утверждение-кандидат
Наличие IONVMeFamily/APFS/AppleEmbeddedPCIE/AppleT8140PCIe в исследованном BootKC не было достаточным доказательством появления guest-visible block device. В source project одновременно наблюдались соответствующие компоненты и отсутствие `/dev/disk*`; filtered IORegistry не показывал ожидаемого PCIe/NVMe provider binding.

Следовательно, диагностика должна отдельно проверять runtime IOService instantiation/matching, а не заключать о доступности устройства только по составу BootKC.

## Provenance
`.context/manager/beliefs.md@05508e6e...`, `.context/current/blockers.md@91f2793d...`.

## Ограничение
Требуется независимое подтверждение новым Экспертом; текущая запись не обобщается на все iOS versions/hardware profiles.
