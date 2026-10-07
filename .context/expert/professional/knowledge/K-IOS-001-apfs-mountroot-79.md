# K-IOS-001 — APFS mountroot error 79 / extentref accounting

Тип: knowledge candidate
Класс: G0
Доказательный статус: `candidate_reproduced_by_source_manager`
Область: исследование rebuilt APFS recovery images в зафиксированных условиях исходного проекта.

## Ограниченное утверждение
В исследованном случае raw divergence количества physical-extent reference records `719 vs 1360` сама по себе не доказывала дефект APFS writer. Для source сумма физических extent length совпала с APSB net allocation. Для rebuilt оставшийся allocation delta был согласуем с writer-owned filesystem metadata и фиксированными allocations. Следовательно, следующая диагностическая ценность была выше у полного APSB/root-tree/file-extent сравнения, чем у ещё одной мутации extentref semantics.

Это НЕ утверждение, что writer был mount-correct, и НЕ универсальное правило APFS.

## Provenance
- source manager-state: `bd55608c...`
- `.context/dialogues/2026-09-24-apfs-error79-reconciliation.md@09555cbb...`
- historical baseline: `docs/agent-migration-baseline.md@6c51341e...`

## Повторная проверка
Новый Эксперт должен воспроизвести вывод на независимом/новом APFS case либо на сохранённом evidence без доступа к готовому заключению до анализа.
