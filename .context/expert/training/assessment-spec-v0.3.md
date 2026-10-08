# Публичная спецификация входной диагностики iOS-Эксперта v0.3

Статус: `APPROVED_FOR_BASELINE_DIAGNOSTIC_EXECUTION`
Карта профессии: `0.3.0`
Целевой профиль: `0.2`
Нормативная база: `EXPERT-TRAINING-v0.3`
Инфраструктурные ворота: PP-RM/GitHub run-2 = PASS; runtime-separation canary = PASS.

## Назначение
Проверить фактическое исходное доказательное состояние `ios-expert` до обучения. Диагностика не наследует навыки от Project Manager, не повышает D-уровень и не принимает G0-кандидаты автоматически.

## Обязательное покрытие
- A1/A4: secure boot/recovery; различение boot/restore/personalization.
- B1/B2: XNU fault localization + version-aware source reasoning.
- C1/C2: IOKit matching, IORegistry/DeviceTree hierarchy.
- D1/D4: APFS/root-mount diagnosis; documented vs empirical.
- E1/E2/E4: code signing, trust/runtime policy, sandbox distinction.
- F1/F2/F4: early userland, dyld, launchd/Mach/XPC lifecycle.
- H1/H2/H3/H4: evidence discipline, tool selection, observe-before-mutate, transfer boundaries.
- I1/I2/I3: firmware/system artifacts and binary provenance.

Вторично: C3, D2/D3, E3, G1/G2/G3, I4.

## Уровни
- E1: объяснить и применить к новому примеру.
- E2: read-only анализ заданного evidence bundle.
- E3: перенос на новую комбинацию условий.
- E4: сквозная диагностика нескольких областей.

## Обязательные критерии
1. первый доказанный отказ локализуется по данным, а не по привычной гипотезе;
2. факт / гипотеза / неизвестность разделены;
3. версия ОС, устройство, артефакт и среда не теряются;
4. официальное/нормативное и эмпирическое разделены;
5. перенос между версиями/устройствами/виртуальной и физической средой не предполагается без доказательства;
6. следующий тест минимально вмешивающийся;
7. внепрофильная задача распознаётся;
8. один удачный случай не повышает G/D автоматически;
9. критичные исполнительные инварианты проходят `RULE_KNOWN -> RULE_APPLIED -> COMPLIANCE_CHECKED`.

## Независимость v0.3
Для каждой попытки:
- конкретный `assessment-instance` замораживается до solver-цепочки;
- фиксируются множества рантаймов подготовки `P`, решения `S` и, если используется, оценки `E`;
- обязательно `P ∩ S = ∅`;
- совпадение runtime ID между подготовкой и решением инвалидирует попытку;
- отдельный закрытый GitHub-контур НЕ является универсальным требованием;
- усиленная изоляция доступа применяется только если её заранее требует risk-profile/конкретная assessment-spec.

## Диагностический статус
Результат может подтверждать knowledge/skill/integration/transfer только в точной области конкретной попытки.
Профессиональная компетентность и D1–D3 этой диагностикой не присваиваются.
