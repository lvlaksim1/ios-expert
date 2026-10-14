# iOS Expert — CYCLE-002 — PRETEST (до учебной карточки)
Дата фиксации сценариев: 2026-10-14. **Только синтетические наблюдения** модели ARM64 iOS-подобной среды. Это не описание реального iPhone или проприетарного драйвера.

Инструкция отдельному решателю: **не читать POSTTEST.md, материалы LEARN и прежние ответы до завершения**. Для каждого A/B/C дать: (1) хронологию t0–t5 с указанием источника, (2) раздельные факты/гипотезы/неизвестное, (3) схему DeviceTree → provider → matching → probe → start → service → BSD, (4) первый доказанный разрыв **или честно заявленную неопределённость**, (5) один минимальный запрос только чтением с развилкой по ответу, (6) ограничения по времени, сборке и реальным устройствам. Закончить RULE_KNOWN / RULE_APPLIED / COMPLIANCE_CHECKED; не заявлять наблюдений вне исходных данных.

## A: 24B-SYNTH-PA — matching
- t0, inventory: в коллекции ядра есть StorageBridgeDriver, personality требует `compatible=vendor,storage-rev3`.
- t1, IODeviceTree snapshot: endpoint `pcie@4/storage@0` описан с `compatible=vendor,storage-rev2`.
- t2, IOService snapshot: опубликованы PCIe bridge и endpoint-provider c `compatible=vendor,storage-rev2`. Отдельных идентификаторов, доказывающих тождество объектов в двух плоскостях, нет.
- t3, matching trace: **именно** personality из t0 явно отвергнута по `compatible`; в доступной трассе нет иной подходящей personality.
- t4, lifecycle trace: для этого кандидата нет записей probe/start; соответствующий контроллер-сервис не наблюдается.
- t5, BSD + пользовательский срез: целевого `/dev/disk*` нет; потребитель ожидает блочное устройство.
О других событиях за окном t0–t5 неизвестно.

## B: 24B-SYNTH-PB — start
- t0, inventory: есть MediaNodeDriver с `compatible=vendor,media-rev5`.
- t1, IODeviceTree snapshot: endpoint описан с `compatible=vendor,media-rev5`.
- t2, IOService snapshot: bridge и соответствующий endpoint-provider опубликованы.
- t3, matching+probe trace: matching успешен, probe вернул экземпляр этого кандидата.
- t4, start trace: start **этого же экземпляра** вернул false; запись `resource request unsuccessful`, внутренней первопричины нет.
- t5, service+BSD snapshot: целевой контроллер-сервис не появился; `/dev/disk*` нет; зависимый процесс сообщает о недоступном томе.
Причина ошибки ресурса и события за временным окном неизвестны.

## C: 24B-SYNTH-PC — неполная наблюдаемость
- t0, inventory: присутствуют код MassMediaController и подходящая personality.
- t1, IODeviceTree snapshot: совместимый endpoint описан.
- t2, IOService snapshot: endpoint-provider опубликован; целевой контроллер-сервис в срезе отсутствует.
- t3, trace coverage report: трассирование matching, probe и start **отключено** на всём интервале t1–t4. Сообщений об этих стадиях нет.
- t4, IOService snapshot: целевой сервис не наблюдается.
- t5, BSD snapshot: соответствующий `/dev/disk*` не наблюдается.
Нет явного события отказа или доказательства, что соответствующие вызовы вообще выполнялись.

**Обязательное методическое ограничение:** отсутствие записи в неполной трассе не доказывает, что событие не произошло. Ответ решателя не должен содержать «угаданную» причину.
