# T-IOS-001 — qemu-sptm Windows Darwin research runtime

Тип: tool candidate
Класс: G0

Исходный проект использует pinned/bundled QEMU fork with Darwin machine support как среду для boot/provisioning/serial evidence на Windows. Инструмент полезен для воспроизводимых исследовательских задач, но его поведение зависит от точной версии fork/build и не считается эквивалентом физического устройства автоматически.

Перед повышением статуса нужны: точная версия/происхождение, интерфейс запуска, разрешения/побочные эффекты, проверка воспроизводимости и rollback path.
