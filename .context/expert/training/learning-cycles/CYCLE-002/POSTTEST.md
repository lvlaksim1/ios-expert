# iOS Expert — CYCLE-002 — POSTTEST (после учебной карточки)
Дата фиксации сценариев: 2026-10-14. **Только синтетические** наблюдения ARM64 iOS-подобной среды, не реальные устройства и не описание закрытых драйверов Apple.

Инструкция другому решателю: разрешены только PLAN.md, этот POSTTEST.md и впоследствии утверждённая карточка LEARN; **запрещено** читать PRETEST.md, PRETEST-RESULT.md и оценки до сдачи ответа. Для каждого A′/B′/C′ дать: (1) хронологию t0–t5 и происхождение, (2) FACT/HYPOTHESIS/UNKNOWN, (3) DeviceTree → provider → matching → probe → start → service → BSD, (4) первый доказанный разрыв либо невозможность его установить, (5) один минимальный запрос только чтением и ожидаемые альтернативы, (6) ограничения времени/сборки/синтетичности. Завершить RULE_KNOWN / RULE_APPLIED / COMPLIANCE_CHECKED.

## A′: 24C-SYNTH-QA — matching
- t0, inventory: есть FlashLinkController, personality требует `compatible=lab,flash-v6`.
- t1, IODeviceTree snapshot: endpoint `pcie@7/flash@1` описан с `compatible=lab,flash-v4`.
- t2, IOService snapshot: bridge и endpoint-provider с `compatible=lab,flash-v4` видимы. Тождество объектов двух плоскостей отдельными идентификаторами не подтверждено.
- t3, matching trace: personality из t0 явно отклонена по `compatible`; других подходящих личностей в доступной трассе не зарегистрировано.
- t4, lifecycle trace: для этого кандидата нет probe/start; искомый storage-сервис не наблюдается.
- t5, BSD+app snapshot: целевого `/dev/disk*` нет; служба пользователя ожидает накопитель.
За пределами временного окна сведения неполны.

## B′: 24C-SYNTH-QB — start
- t0, inventory: есть BlockPortDriver с `compatible=lab,block-v2`.
- t1, IODeviceTree snapshot: endpoint с `compatible=lab,block-v2`.
- t2, IOService snapshot: опубликованы bridge и соответствующий endpoint-provider.
- t3, matching+probe trace: matching успешен, probe создал экземпляр кандидата.
- t4, start trace: start **этого экземпляра** вернул false, запись `initialization request failed`, истинная причина отсутствует.
- t5, IOService+BSD snapshot: целевой сервис отсутствует; `/dev/disk*` нет; приложение не открывает том.
Другие экземпляры и первопричина ошибки неизвестны.

## C′: 24C-SYNTH-QC — неполная наблюдаемость
- t0, inventory: найден ExternalMediaDriver с подходящей personality.
- t1, IODeviceTree snapshot: совместимый endpoint описан.
- t2, IOService snapshot: endpoint-provider присутствует; целевой контроллер-сервис отсутствует.
- t3, trace coverage report: логирование matching/probe/start **не было включено** в интервале t1–t4; в данных нет этих событий.
- t4, IOService snapshot: целевого сервиса не наблюдается.
- t5, BSD snapshot: целевой `/dev/disk*` отсутствует.
Сообщений о конкретном отказе нет, и доказательств исполнения отдельных стадий нет.

Пары A/A′, B/B′ и C/C′ сопоставимы **по наблюдаемой структуре**, но это не доказывает одинаковую сложность. Не выводить из отсутствия данных свидетельство их отсутствия.
