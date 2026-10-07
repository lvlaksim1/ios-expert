# E-IOS-001 — APFS mountroot error 79

Источник: `iOS-Research-Runtime`, migration/reconciliation work 2026-09-24.
Фактический исполнитель исторического действия: Project Manager / predecessor research chain, не `ios-expert`.

Наблюдение: Windows E2E доходил до XNU/APFS root mounting; rebuilt recovery APFS завершался error 79. Подозрение на extentref count divergence было проверено структурным reconciliation; вывод был сужен, а следующим шагом выбрано расширение APSB/root-tree evidence.

Класс записи: G0 experience episode.
Не является прямым доказательством компетентности `ios-expert`.
