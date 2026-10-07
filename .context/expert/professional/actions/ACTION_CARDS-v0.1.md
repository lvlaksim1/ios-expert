# Карточки обязательных профессиональных действий — кандидат v0.1

Статус: `DRAFT_FOR_BASELINE_ASSESSMENT`
Карта профессии: `0.3.0`
Все действия: текущий допуск D0. Риски указаны для read-only диагностического варианта; любое внешнее/привилегированное изменение требует отдельной переоценки риска.

## Общие поля
Для каждой карточки: цель; граница; предварительные знания/навыки; наблюдаемый результат; допустимые доказательства; зависимости; runtime_dependency; risk-profile; триггеры повторной проверки.

### A1 — Secure-boot/recovery chain analysis
- Цель: локализовать первый доказанный отказ по цепочке доверенной загрузки.
- Граница: не выводить закрытые детали из отсутствия наблюдения.
- Результат: version/device-bound causal chain + first proven failure.
- Evidence: Apple Platform Security, boot/serial evidence, artifact metadata.
- Зависимости: I1, H1.
- Runtime dependency: device generation, iOS build, boot mode, artifact set.
- Risk: R1.
- Revalidate: новая SoC/boot architecture или крупная версия iOS.

### A4 — Boot/restore/personalization distinction
- Цель: различать отказ загрузки, restore/update и personalization/signing flow.
- Граница: не моделировать недокументированную серверную логику Apple как факт.
- Результат: локализованный flow + проверяемый следующий discriminator.
- Evidence: official security/update docs, manifests/artifact metadata, restore logs.
- Зависимости: I1, E1, H1.
- Runtime dependency: device, iOS build, restore tooling, signing state.
- Risk: R1 read-only; R2 при реальном restore/mutation.

### B1 — XNU subsystem fault localization
- Цель: отнести наблюдаемый kernel symptom к минимально доказанной Mach/BSD/VM/IPC/process subsystem boundary.
- Результат: competing hypotheses + ruled-in/out evidence.
- Evidence: panic/serial/runtime traces, XNU source, debugger output.
- Зависимости: B2, H1.
- Runtime dependency: exact XNU/iOS build, architecture.
- Risk: R1 read-only.

### B2 — Version-aware XNU source reasoning
- Цель: использовать открытый XNU как источник, не приравнивая его автоматически к конкретной закрытой сборке iOS.
- Результат: source-to-runtime applicability statement with limits.
- Evidence: exact source revision, symbol/behavior evidence, version metadata.
- Зависимости: I2, H1.
- Runtime dependency: XNU source release vs target build.
- Risk: R1.

### C1 — Driver availability vs runtime binding
- Цель: отличить наличие driver code/personality от provider publication, match, probe/start и зарегистрированного сервиса.
- Результат: точная стадия, на которой цепочка прекращается.
- Evidence: BootKC/kernel collection, IORegistry/IOService evidence, matching properties.
- Зависимости: B2, H1, I2.
- Runtime dependency: kernel collection, DeviceTree, device model, iOS build.
- Risk: R1.

### C2 — IODeviceTree/IOService analysis
- Цель: восстановить provider/client hierarchy и matching evidence.
- Результат: registry-grounded topology + missing/mismatched property/provider hypothesis.
- Evidence: IORegistry planes, DeviceTree, IOKit primary docs/source.
- Зависимости: C1, H1, I1.
- Runtime dependency: device tree version, OS/device model.
- Risk: R1.

### D1 — APFS/root-mount diagnosis
- Цель: локализовать mount/container/volume/root failure без преждевременной мутации writer.
- Результат: bounded hypotheses + least-destructive discriminator.
- Evidence: mount logs, image/container metadata, fs structures, controlled comparisons.
- Зависимости: D4, H1, I1.
- Runtime dependency: iOS/APFS generation, image build, tooling.
- Risk: R1 read-only; R2 при изменении образа, влияющем на boot.

### D4 — Documented vs empirical APFS boundary
- Цель: явно отделять Apple-documented APFS свойства от reverse-engineered on-disk claims.
- Результат: claim classification + provenance + uncertainty.
- Evidence: Apple APFS docs (с актуальностью), reproducible structural observations.
- Зависимости: H1.
- Runtime dependency: APFS/iOS version.
- Risk: R1.

### E1 — Code-signing/trust model analysis
- Цель: объяснить CodeDirectory/CMS/trust/entitlements chain в подтверждённой области.
- Результат: layer-specific verification model.
- Evidence: Apple security docs, XNU code-signing structures, CoreTrust/dyld sources.
- Зависимости: I2, I3, H1.
- Runtime dependency: OS build, code-signature format/policy version.
- Risk: R1.

### E2 — Runtime code-policy failure localization
- Цель: локализовать отказ между signature validation, trust, entitlement, loader/library validation и иными policy layers.
- Результат: first proven rejecting layer + next test.
- Evidence: launch/runtime logs, signature/entitlement metadata, dyld/XNU evidence.
- Зависимости: E1, F2, H1.
- Runtime dependency: iOS build, binary/signature, device state.
- Risk: R2.

### E4 — Sandbox/application-container distinction
- Цель: не смешивать валидность подписи с разрешённым доступом процесса.
- Результат: distinction between signing/trust and sandbox/container/runtime policy.
- Evidence: entitlement/container data, process/runtime evidence, Apple security docs.
- Зависимости: E1, H1.
- Runtime dependency: app/process entitlements, OS build, container state.
- Risk: R2.

### F1 — Kernel-to-launchd transition analysis
- Цель: отделить завершение kernel boot от раннего userland/launchd failure.
- Результат: evidence-bound transition state.
- Evidence: serial/init/launch traces, process evidence.
- Зависимости: A1, B1, H1.
- Runtime dependency: iOS build, boot mode/rootfs.
- Risk: R1.

### F2 — dyld/image/dependency diagnosis
- Цель: локализовать dynamic-loader/image/dependency failure.
- Результат: loader-specific cause or bounded unknown.
- Evidence: Mach-O/dyld cache metadata, loader logs, dyld source/docs.
- Зависимости: I2, I3, E1, H1.
- Runtime dependency: dyld/shared-cache build, binary architecture, OS build.
- Risk: R1.

### F4 — launchd/Mach/XPC service lifecycle diagnosis
- Цель: отличить отсутствие job/service, failure to publish, lookup failure и client connection failure.
- Результат: service-lifecycle stage + evidence.
- Evidence: launchd/service metadata, bootstrap/Mach/XPC observations, logs.
- Зависимости: F1, H1.
- Runtime dependency: OS build, service definitions/entitlements.
- Risk: R1.

### H1 — Version-bound evidence discipline
- Цель: каждый значимый вывод связать с точной версией артефакта/среды.
- Результат: traceable evidence package.
- Evidence: hashes/SHAs/build IDs/log provenance/tool versions.
- Зависимости: none.
- Runtime dependency: evidence/tooling itself.
- Risk: R0/R1.

### H2 — Research-environment selection
- Цель: выбрать physical/virtual/emulated/static/debugger environment, способную проверить нужное свойство.
- Результат: environment rationale + known blind spots.
- Evidence: capability documentation and observed behavior.
- Зависимости: H1.
- Runtime dependency: tool/platform version.
- Risk: R1.

### H3 — Observe before mutate
- Цель: расширять наблюдаемость до семантической мутации, если причина не доказана.
- Результат: least-destructive next experiment.
- Evidence: competing hypotheses and missing discriminators.
- Зависимости: H1, H2.
- Runtime dependency: experiment environment.
- Risk: R1; mutation may escalate.

### H4 — Transfer-boundary validation
- Цель: отдельно доказывать перенос между версиями, устройствами и виртуальной/физической средой.
- Результат: explicit supported/not-supported transfer claim.
- Evidence: paired/independent cases, environmental differences.
- Зависимости: H1, H2.
- Runtime dependency: both source and target environments.
- Risk: R1.

### I1 — Firmware/system artifact identification
- Цель: различать IPSW/manifest, IMG4-family containers/payloads, DeviceTree и version/device bindings.
- Результат: provenance-preserving artifact map.
- Evidence: manifests, headers/metadata, official security/update evidence, reproducible parsing.
- Зависимости: H1.
- Runtime dependency: device/iOS/artifact format generation.
- Risk: R1.

### I2 — Mach-O and kernel collection analysis
- Цель: разбирать Mach-O/kernel collections/BootKC как version-bound artifacts.
- Результат: structure/dependency/metadata extraction with provenance.
- Evidence: binary headers, load commands, symbols where available, Apple OSS structures/tools.
- Зависимости: H1.
- Runtime dependency: architecture, format and OS generation.
- Risk: R1.

### I3 — dyld shared cache / trust-cache artifact analysis
- Цель: анализировать системные caches без смешения структуры, содержимого и policy meaning.
- Результат: versioned artifact inventory and bounded claims.
- Evidence: cache headers/metadata, Apple dyld sources, integrity/version data.
- Зависимости: H1.
- Runtime dependency: OS/platform/cache format.
- Risk: R1.

## Интеграционный шлюз
Наличие карточек и компонентных знаний не подтверждает действие. Для каждого действия требуется отдельная E2/E3 проверка, а для сквозных задач — E4. До baseline assessment все карточки остаются проектом требований, а не подтверждённой квалификацией.
