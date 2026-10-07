# Карта профессии iOS/Darwin — внешний пересмотр

Статус: `DRAFT_EXTERNAL_SOURCES_RECONCILED`
Версия: `0.2.0`
Дата: 2026-10-07

Карта перестроена после независимой сверки исходного проектно-ориентированного черновика с Apple Platform Security, Apple Developer/IOKit, открытым XNU и профессиональной практикой iOS kernel/reverse-engineering community. Она ещё не утверждена Владельцем и не создаёт допусков.

## A. Secure boot, firmware и recovery
- A1: восстановить и объяснить цепочку Boot ROM -> bootloader/iBoot -> kernel и точки проверки доверия для конкретной модели/версии.
- A2: различать normal/recovery/DFU и их доказательные признаки без смешения с проектными допущениями.
- A3: проверить состав firmware/recovery bundle и доказать достижение конкретной контрольной точки загрузки.

## B. XNU: Mach/BSD и ядро
- B1: локализовать отказ внутри XNU по наблюдаемым подсистемам Mach/BSD/VM/IPC/process lifecycle, не делая вывод из одного симптома.
- B2: сопоставлять наблюдаемое поведение с открытым XNU-кодом с учётом различий версии и закрытых компонентов iOS.
- B3: строить безопасный план kernel debugging/instrumentation и отделять наблюдение от изменения поведения.

## C. IOKit, DeviceTree и аппаратное сопоставление
- C1: отличать присутствие driver code/personality от фактической публикации provider и успешного matching/probe/start.
- C2: анализировать IODeviceTree/IOService planes, provider/client hierarchy, matching properties и runtime registry evidence.
- C3: локализовать разрыв DeviceTree -> bridge/endpoint -> DART/IOMMU/interrupt -> device family -> BSD-visible device.

## D. APFS, storage и системные образы
- D1: исследовать APFS mount/container/volume/root failure через on-disk и runtime evidence.
- D2: сравнивать source/rebuilt структуры без преждевременного изменения writer semantics.
- D3: различать file-data accounting, filesystem metadata, container/volume allocation и проверять гипотезы структурными инвариантами.
- D4: явно маркировать, где вывод основан на официально документированном APFS, а где — на воспроизводимом исследовании недокументированного on-disk поведения.

## E. Code signing и runtime security policy
- E1: объяснить CodeDirectory/CMS/entitlements/trust-policy цепочку на уровне, поддержанном открытыми Apple/XNU/CoreTrust источниками.
- E2: локализовать отказ запуска/загрузки кода между подписью, entitlement/policy, library validation/dyld и другими проверяемыми слоями, не сводя всё к слову «AMFI».
- E3: анализировать trust-cache и platform-policy утверждения с явной привязкой к версии ОС и источнику.

## F. launchd, dyld и пользовательский системный runtime
- F1: анализировать переход kernel -> launchd и ранний userland как отдельную стадию загрузки.
- F2: диагностировать dynamic loader / image loading / dependency и entitlement-mediated runtime ограничения с привязкой к версии.
- F3: отделять kernel policy, dyld policy и app/process configuration при причинном анализе.

## G. Аппаратная безопасность и Data Protection
- G1: объяснить роль hardware root of trust, Secure Enclave и отдельных secure-boot цепочек без приписывания недоказанных внутренних деталей.
- G2: анализировать Data Protection/ключевую архитектуру и влияние boot mode только в пределах доступных первичных данных и воспроизводимых наблюдений.
- G3: для закрытых аппаратных подсистем явно фиксировать предел знания и не выдавать reverse-engineering гипотезу за документированный факт.

## H. Исследовательская среда, reverse engineering и доказательность
- H1: собирать version-bound evidence из serial/runtime/registry/debugger/CI traces.
- H2: выбирать между физическим устройством, виртуализацией, эмуляцией, статическим анализом и отладчиком по тому, какое свойство нужно доказать.
- H3: сначала расширять наблюдаемость, затем менять исследуемую семантику, если текущих данных недостаточно.
- H4: подтверждать перенос вывода между средами отдельно; виртуальная среда не считается автоматически эквивалентной устройству.

## Риск и допуск
Все действия стартуют D0. Read-only анализ обычно кандидат R0/R1; действия, затрагивающие security policy, чувствительные данные, privileged mutation или защищённую основу, по умолчанию R2/R3 до отдельной оценки.

## Источниковая дисциплина
1. Apple Platform Security / Apple Developer / Apple OSS — первичная основа.
2. Воспроизводимое наблюдение может опровергать применимость документа к конкретной версии, но не стирает исходный источник.
3. Профессиональные материалы Corellium/Project Zero и сходного уровня используются как вторичная практическая основа, особенно для debugging/reverse engineering.
4. Старые/retired Apple документы используются только с явной пометкой актуальности.
