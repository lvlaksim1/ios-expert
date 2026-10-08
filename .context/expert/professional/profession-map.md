# Карта профессии iOS/Darwin — после мысленной проверки

Статус: `APPROVED_OWNER_BASELINE`
Версия: `0.3.0`
Дата: 2026-10-07

Карта основана на Apple Platform Security, Apple Developer/IOKit, Apple OSS XNU/dyld/launchd, воспроизводимых наблюдениях и профессиональной практике iOS kernel/reverse-engineering. Утверждена Владельцем 2026-10-07 как начальная защищённая карта профессии. Утверждение карты не создаёт навыков, компетентности или операционных допусков.

## A. Secure boot, firmware, recovery и restore
- A1: восстановить цепочку Boot ROM -> bootloader/iBoot -> kernel и точки проверки доверия для конкретной модели/версии.
- A2: различать normal/recovery/DFU и их доказательные признаки.
- A3: проверить состав firmware/recovery bundle и доказать достижение контрольной точки загрузки.
- A4: различать boot flow, restore/update flow и personalization/signing flow; локализовать несовместимость артефакта без недоказанных выводов о закрытой серверной логике Apple.

## B. XNU: Mach/BSD и ядро
- B1: локализовать отказ внутри XNU по подсистемам Mach/BSD/VM/IPC/process lifecycle.
- B2: сопоставлять поведение с открытым XNU-кодом с учётом различий версии и закрытых компонентов iOS.
- B3: строить безопасный план kernel debugging/instrumentation и отделять наблюдение от изменения поведения.
- B4: анализировать version-specific kernel integrity/protection mechanisms только в пределах первичных источников и воспроизводимого evidence.

## C. IOKit, DeviceTree и аппаратное сопоставление
- C1: отличать наличие driver code/personality от публикации provider и успешного matching/probe/start.
- C2: анализировать IODeviceTree/IOService planes, provider/client hierarchy и matching properties.
- C3: локализовать разрыв DeviceTree -> bridge/endpoint -> DART/IOMMU/interrupt -> device family -> BSD-visible device.

## D. APFS, storage и системные образы
- D1: исследовать APFS mount/container/volume/root failure через on-disk и runtime evidence.
- D2: сравнивать source/rebuilt структуры без преждевременного изменения writer semantics.
- D3: различать file-data accounting, filesystem metadata и container/volume allocation через структурные инварианты.
- D4: отделять официально документированный APFS от воспроизводимого исследования недокументированного on-disk поведения.

## E. Code signing, sandbox и runtime security policy
- E1: объяснить CodeDirectory/CMS/entitlements/trust-policy цепочку в пределах Apple/XNU/CoreTrust evidence.
- E2: локализовать отказ запуска между signature validation, trust/policy, entitlement, library validation/dyld и иными проверяемыми слоями.
- E3: анализировать trust-cache/platform-policy с привязкой к версии ОС и источнику.
- E4: отделять code-signing решение от sandbox/application-container/runtime policy и не считать валидную подпись доказательством разрешённого поведения процесса.

## F. launchd, dyld, Mach services и системный userland
- F1: анализировать переход kernel -> launchd и ранний userland как отдельную стадию.
- F2: диагностировать dynamic-loader/image/dependency ограничения с привязкой к версии.
- F3: отделять kernel policy, dyld policy и process configuration.
- F4: диагностировать launchd job / Mach bootstrap service / XPC service lifecycle и отличать отсутствие сервиса от невозможности клиента подключиться к существующему сервису.

## G. Аппаратная безопасность и Data Protection
- G1: объяснить hardware root of trust, Secure Enclave и отдельные secure-boot цепочки без недоказанных внутренних деталей.
- G2: анализировать Data Protection/ключевую архитектуру и влияние boot mode в пределах первичных данных.
- G3: для закрытых аппаратных подсистем явно фиксировать предел знания.

## H. Исследовательская среда, reverse engineering и доказательность
- H1: собирать version-bound evidence из serial/runtime/registry/debugger/CI traces.
- H2: выбирать физическое устройство, виртуализацию, эмуляцию, статический анализ или отладчик по проверяемому свойству.
- H3: сначала расширять наблюдаемость, затем менять семантику, если данных недостаточно.
- H4: подтверждать перенос вывода между средами отдельно.

## I. Системные артефакты и бинарные форматы
- I1: идентифицировать и прослеживать IPSW/manifest и IMG4-family артефакты, DeviceTree и связанные version/device bindings без смешения контейнера, содержимого и подписи.
- I2: анализировать Mach-O и kernel collections/BootKC как version-bound бинарные артефакты; извлекать структуру, зависимости и проверяемые метаданные.
- I3: анализировать dyld shared cache, trust-cache и сходные системные артефакты с проверкой происхождения, версии и целостности.
- I4: при преобразовании/пересборке артефакта сохранять доказуемую связь source -> transformation -> output и отдельно доказывать семантическую эквивалентность там, где она заявляется.

## Смежные области, не являющиеся базовой компетентностью
Baseband/modem, GPU, wireless firmware, глубокий reverse engineering Secure Enclave и разработка эксплуатационных цепочек уязвимостей не считаются автоматически частью базовой компетентности этого профиля. Они требуют отдельного расширения target profile и доказательной базы.

Обычная UIKit/SwiftUI продуктовая разработка также вне текущей специализации.

## Общие требования к каждой карточке действия
Для последующей формализации каждое действие должно получить: область применимости, risk-profile, runtime_dependency (OS/device/model/tool), необходимые знания/навыки, критерий результата и допустимые виды доказательств.

Все действия стартуют D0. Read-only анализ обычно кандидат R0/R1; security-policy, privileged mutation, sensitive data или protected-baseline operations считаются R2/R3 до отдельной оценки.
