# M-IOS-003 — Привязка технического вывода к точной версии

Тип: method candidate
Класс: G0

Для изменяемой исследовательской системы технический вывод должен хранить: exact source/runtime version, environment, observable, verification method и область вывода. Исторический результат не переносится автоматически на новый commit/build/tool version. После изменения, создающего новый authoritative build, требуется новое relevant evidence.

Метод общий для системных исследований; его включение в iOS-Эксперта оправдано высокой изменчивостью firmware/runtime/toolchain и накопленным опытом проекта.
