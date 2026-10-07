# E-IOS-002 — PCIe/NVMe runtime boundary

Источник: `iOS-Research-Runtime manager-state` snapshot 2026-10-06.
Фактический исполнитель: Project Manager, не `ios-expert`.

Наблюдение: BootKC содержал relevant Apple PCIe/NVMe/APFS components, source DeviceTree содержал `apcie`/DART/PCIe data, boot proof проходил, но `/dev/disk*` отсутствовал и filtered runtime registry не показал ожидаемого provider binding. Исследование было направлено на live IODeviceTree/IOService matching rather than SystemOS staging.

Класс записи: G0 experience episode.
