# K-IOS-004 — DeviceTree -> IOService -> PCIe/NVMe storage path

Тип: knowledge candidate
Класс: G0
Статус: `hypothesis-structure-supported-by-project-evidence`

## Модель-кандидат
При наличии source DeviceTree `apcie` hierarchy, DART/IOMMU relationships и PCIe ranges, но отсутствии guest-visible disk, полезная последовательность локализации включает:
1. живое присутствие ожидаемого DeviceTree узла;
2. provider/class/property matching;
3. создание PCIe bridge/provider service;
4. endpoint/device-model compatibility;
5. interrupts и DART/IOMMU relationships;
6. IONVMe-related service binding;
7. появление block device;
8. только затем filesystem/SystemOS staging.

## Provenance
`.context/current/blockers.md@91f2793d...`, `.context/current/next.md@f69cef45...`, `.context/manager/beliefs.md@05508e6e...`.

## Ограничение
Это диагностическая карта зависимостей, а не доказательство причины конкретного сбоя без runtime evidence.
