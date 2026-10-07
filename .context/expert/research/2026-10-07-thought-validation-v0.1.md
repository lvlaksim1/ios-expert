# Мысленная проверка карты профессии iOS/Darwin v0.2

Дата: 2026-10-07
Статус: completed first pass

## Метод
Проверены типовые задачи, которые не являются простым повторением iOS-Research-Runtime. Цель — найти задачи, для которых карта даёт неоднозначную или искусственно широкую классификацию.

## Сценарии
- TV-01: boot verification/recovery-mode failure — A/E/G: покрыто.
- TV-02: driver present in kernel collection, provider/service absent — C/H: покрыто хорошо.
- TV-03: rebuilt APFS recovery image fails root mount — D/H: покрыто хорошо.
- TV-04: signed executable refuses to launch — E/F: покрыто, но sandbox/runtime-policy слой недостаточно явен.
- TV-05: launchd job starts, Mach/XPC service unavailable — F: частично; XPC/Mach-service model не выражен.
- TV-06: нужно статически разобрать kernel collection/Mach-O/dyld shared cache — H/F: формально можно притянуть, но отдельной профессиональной области нет.
- TV-07: restore/update artifact or personalization mismatch — A: слишком широкая формулировка, отсутствует явный restore/update/personalization слой.
- TV-08: XNU/IOKit panic with user-client interaction — B/C/H: покрыто.
- TV-09: Data Protection behavior differs in recovery/normal boot — G/A: покрыто при сохранении границ знания.
- TV-10: virtual device result differs from physical hardware — H4: покрыто хорошо.
- TV-11: same method on another iOS/device generation — общая модель требует runtime_dependency, но карта должна делать это явным в карточках действий.
- TV-12: baseband/GPU/wireless/SEP-internal problem — карта не должна притворяться полной; нужны явные adjacent/out-of-scope границы.

## Найденные пробелы
1. Нет самостоятельной области системных артефактов и бинарных форматов: IPSW/manifest/IMG4 family, Mach-O, kernel collections, dyld shared cache, DeviceTree/trust-cache as artifacts.
2. launchd/dyld область должна включать Mach bootstrap services/XPC/service lifecycle.
3. Code-signing/policy область должна явно включать sandbox/application-container policy как отдельный слой, не сводимый к подписи.
4. Secure-boot область должна отдельно различать boot, restore/update и personalization flows.
5. Нужна явная граница adjacent specialties: baseband, GPU, wireless, глубокий SEP reverse engineering и exploit weaponization не считаются базовой компетентностью этого профиля.
6. Первый target-profile чрезмерно отражает наследованный APFS/storage опыт и должен добавить artifact literacy + general userland/service diagnosis.

## Решение
Выпустить profession-map v0.3.0 и target-profile candidate v0.2.0. Статус остаётся draft; никаких D1-D3 и G1/G2 из этой проверки не выдаётся.
