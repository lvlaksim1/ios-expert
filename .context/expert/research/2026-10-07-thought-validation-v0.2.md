# Мысленная проверка карты профессии iOS/Darwin v0.3 — проход 2

Дата: 2026-10-07
Статус: PASS_WITH_PREASSESSMENT_WORK

## Новые сценарии
- TV2-01 restore/personalization artifact mismatch -> A4 + I1: PASS.
- TV2-02 wrong-version dyld shared cache -> I3 + F2 + H1: PASS.
- TV2-03 executable has valid signature but sandbox denies operation -> E4: PASS.
- TV2-04 launchd job exists but client cannot reach Mach/XPC service -> F4: PASS.
- TV2-05 static analysis of unfamiliar kernel collection/Mach-O -> I2 + B2: PASS.
- TV2-06 driver/personality exists but provider is never published -> C1/C2: PASS.
- TV2-07 APFS on-disk field is not documented by Apple -> D4 + H1/H3: PASS only if claim remains empirical.
- TV2-08 Data Protection behavior differs in recovery -> G2 + A2: PASS with explicit knowledge boundary.
- TV2-09 virtual result differs from physical device -> H4: PASS; no automatic transfer.
- TV2-10 rebuilt boot artifact preserves syntax but changes behavior -> I4 + A3 + H3: PASS; semantic equivalence must be proven separately.
- TV2-11 baseband/GPU/wireless deep-internal failure -> correctly classified as adjacent specialization, not falsely claimed competence: PASS.
- TV2-12 SwiftUI/App Store product issue -> outside current low-level profile: PASS.
- TV2-13 exploit-chain engineering -> not assumed by base profile; requires explicit extension: PASS.
- TV2-14 same IOKit hypothesis on another device/iOS generation -> map requires version-aware reasoning, but concrete action cards must record `runtime_dependency`: PREASSESSMENT GAP.
- TV2-15 cross-domain boot failure requiring A+C+D+H -> map supports integration, but E4 assessment needs explicit dependency graph: PREASSESSMENT GAP.

## Вывод
No critical/high conceptual gap found in profession-map v0.3 for the declared specialization `iOS/Darwin systems research and engineering`.

Перед baseline assessment обязательно:
1. создать полные action cards для обязательных действий target-profile;
2. связать зависимости между ними;
3. назначить предварительный risk-profile;
4. определить допустимые evidence types;
5. не создавать скрытые assessment-instance в readable-history.

## Scope boundary
Текущий профиль сознательно не является «экспертом по всему, что связано с iPhone». Продуктовая UIKit/SwiftUI-разработка, глубокие baseband/GPU/wireless/SEP-internals и exploit weaponization не входят автоматически. Расширение потребует новой версии profession-map.
