# K-IOS-002 — Наблюдаемая загрузочная цепочка Darwin/iOS research runtime

Тип: knowledge candidate
Класс: G0
Статус: `scope_limited_project_evidence`

## Утверждение-кандидат
Исходный проект показал диагностически полезное разделение стадий firmware/runtime -> SPTM/TXM -> XNU -> filesystem/root mount -> launchd -> shell. Наблюдение более поздней стадии является доказательством прохождения ранних стадий в конкретной сборке, но не доказывает полноту GUI/SystemOS/user-device поведения.

## Ограничение
Это evidence model для исследованной qemu-sptm среды, а не утверждение эквивалентности физическому устройству iPhone.

## Provenance
`.context/memory/procedural.md@3cc7be7f...`, `.context/manager/beliefs.md@05508e6e...`, `ARCHITECTURE.md` исходного проекта.
