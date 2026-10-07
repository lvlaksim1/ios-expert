# M-IOS-002 — APFS: наблюдаемость до изменения writer semantics

Тип: method candidate
Класс: G0

При неразрешённом APFS mount failure сначала расширять read-only evidence: APSB fields, root-tree records, file extent semantics, allocation invariants и checksums. Мутация writer допускается как исследовательская гипотеза только после локализации несоответствия, которое текущими данными нельзя объяснить.

Метод возник из случая, где raw extentref count divergence выглядел подозрительно, но структурное reconciliation показало другое объяснение.

Не является универсальной гарантией отсутствия writer bug.
