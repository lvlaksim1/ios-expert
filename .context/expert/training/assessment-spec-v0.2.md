# Публичная спецификация входной диагностики iOS-Эксперта v0.2

Статус: `DESIGN_ONLY_NO_HIDDEN_TASKS`
Карта профессии: `0.3.0`

Этот документ фиксирует измеряемые способности и критерии. Конкретные скрытые задачи запрещено хранить в readable-history `ios-expert`.

## Семейства проверки
1. A — secure boot/recovery/restore: причинная цепочка и различение boot/restore/personalization.
2. B — XNU: Mach/BSD/VM/IPC/process/kernel fault localization с version-aware source reasoning.
3. C — IOKit/DeviceTree: code availability -> provider publication -> matching/probe/start -> runtime service/device.
4. D — APFS/storage: конкурирующие гипотезы, documented-vs-empirical boundary, минимально вмешивающийся discriminator.
5. E — code signing/sandbox/policy: signature, trust, entitlement, sandbox, loader/runtime policy как разные слои.
6. F — launchd/dyld/Mach/XPC: ранний userland, loader и service-lifecycle diagnosis.
7. G — hardware security/Data Protection: точное знание документированного и корректная остановка на границе неизвестного.
8. H — research/evidence: выбор среды, version-bound evidence, observe-before-mutate, transfer boundary.
9. I — system artifacts: IPSW/IMG4-family, Mach-O, kernel collections, dyld shared cache, DeviceTree/trust-cache provenance and structure.

## Уровни проверки
- E1 знание: объяснить и применить к новому примеру;
- E2 навык: выполнить read-only анализ по заданным данным;
- E3 перенос: решить новую комбинацию условий;
- E4 интеграция: провести сквозную диагностику через несколько областей.

## Обязательные критерии
- локализация первого доказанного отказа, а не наиболее привычного;
- явное разделение факта, гипотезы и неизвестности;
- точная привязка к OS/device/artifact/tool version;
- различение нормативного/официального описания и эмпирического поведения;
- отсутствие необоснованного переноса между устройствами/версиями/виртуальной и физической средой;
- минимально вмешивающийся следующий тест;
- правильное распознавание задачи вне текущей специализации;
- отсутствие повышения G/D-статусов на основании одной удачной попытки.

## Независимость
`assessment-spec` открыт. `assessment-instance` с конкретными отложенными задачами должен существовать вне доступной Эксперту Git history и создаваться/предъявляться независимым контуром. До доказательства этого свойства итоговая аттестация остаётся BLOCKED.
