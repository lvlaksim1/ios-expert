# Целевой профессиональный профиль iOS/Darwin — кандидат 0.2

Статус: `APPROVED_OWNER_BASELINE`
Карта профессии: `0.3.0`

## Назначение
Первая диагностика должна широко проверить базовые системные области профессии, а не продолжать наследованный проектный уклон. Конкретная первая учебная программа выбирается только после диагностики по доказанным пробелам.

## Обязательное покрытие исходной диагностики
- A1/A4 — secure boot/recovery и различение boot/restore/personalization flows;
- B1/B2 — XNU fault localization и version-aware source reasoning;
- C1/C2 — IOKit matching + IORegistry/DeviceTree analysis;
- D1/D4 — APFS/root-mount diagnosis и граница documented/empirical;
- E1/E2/E4 — code signing, runtime policy и sandbox-layer distinction;
- F1/F2/F4 — early userland, dyld и launchd/Mach/XPC service diagnosis;
- H1/H2/H3/H4 — evidence discipline, tool selection, observe-before-mutate и transfer boundaries;
- I1/I2/I3 — firmware/binary/system-artifact literacy.

## Вторичная диагностика
- C3 full hardware/storage transport chain;
- D2/D3 structural APFS comparisons;
- E3 trust-cache/platform-policy;
- G1/G2/G3 hardware security/Data Protection boundaries;
- I4 source -> transformation -> output semantic-equivalence reasoning.

## Допуск
Все действия остаются D0 до отдельного решения. Диагностические read-only упражнения не являются операционным D1-D3.

## Доказательства
Для подтверждения способности нужны новые задачи, не являющиеся простым повторением мигрированных кейсов. История старого Project Manager может формировать гипотезы, тренировочные примеры и регрессии, но не заменяет новую демонстрацию `ios-expert`.

## Выбор первой учебной программы
После baseline-assessment строится gap-map. Первая программа выбирается по зависимости, величине пробела, профессиональной значимости и риску; частота старого проектного опыта не является самостоятельным приоритетом.

Профессиональная компетентность реальной устойчивой работы на этом этапе не заявляется; для неё требуется отдельная заранее определённая `competence-evidence-spec` и реальные независимые случаи.

## Утверждение
Утверждено Владельцем 2026-10-07 как начальный целевой профессиональный профиль для первой baseline-диагностики. Утверждение профиля не является подтверждением знаний, навыков или компетентности Эксперта.
