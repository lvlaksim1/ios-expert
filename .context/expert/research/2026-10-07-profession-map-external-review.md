# Внешняя сверка карты профессии iOS/Darwin

Дата: 2026-10-07
Статус: research review

## Основной вывод
Версия 0.1 была корректным отражением накопленного опыта iOS-Research-Runtime, но недостаточной картой постоянной профессии: она была смещена к APFS и storage blocker текущего проекта.

## Что подтверждено первичными источниками
- Apple Platform Security выделяет secure boot iPhone/iPad, hardware root of trust, Secure Enclave, code signing и Data Protection как самостоятельные архитектурные слои.
- Apple OSS XNU описывает XNU как Darwin kernel для iOS/macOS с Mach, BSD и IOKit; следовательно XNU должен быть самостоятельной профессиональной областью.
- Apple IOKit documentation различает driver availability, provider publication, matching/probing/start и runtime IORegistry; это подтверждает существующий проектный урок «код в BootKC != runtime binding».
- Apple APFS documentation подтверждает APFS как базовую файловую систему и общие свойства, но старые APFS Guide материалы помечены retired; undocumented on-disk выводы нельзя выдавать за официальные.
- Apple security documentation и открытые XNU/CoreTrust структуры подтверждают необходимость отдельной области code signing/runtime policy.

## Что подтверждает профессиональная практика
Материалы Corellium по iOS reverse engineering и kernel research отделяют XNU architecture, IOKit/registry, kernel debugging и instrumented virtual environments как самостоятельные компетенции. Виртуальная среда ценна для наблюдения, но не доказывает автоматический перенос на физическое устройство.

## Изменение карты
Добавлены самостоятельные области XNU, code signing/runtime policy, launchd/dyld, hardware security/Data Protection и research/debugging methodology. Обычная UIKit/SwiftUI продуктовая разработка явно исключена из текущей специализации, чтобы карта соответствовала заявленному `iOS/Darwin systems research and engineering`.

## Использованные внешние источники
- Apple Platform Security: Boot process for iPad and iPhone devices; Hardware/System security; App code signing; Secure Enclave; Data Protection.
- Apple Developer: IOKit Fundamentals / Driver and Device Matching / I/O Registry; Apple File System Guide (retired, use cautiously).
- Apple OSS: `apple-oss-distributions/xnu`, `dyld`, CoreTrust headers.
- Corellium: iOS Reverse Engineering Course; XNU kernel debugging / device-tree and kernel research materials.
