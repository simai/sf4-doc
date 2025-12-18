# Модули SF4

## Назначение
Фиксирует подтверждённые модули экосистемы SF4 и их назначение по локальным источникам.

## Где применяется
Установка и обновление решений на базе SF4 в Bitrix.

## Где находится
- Реестр модулей: `source/sf4-structure.enriched.json` (узлы `module:*`).
- Снапшоты кода модулей: `source/modules/simai_framework_*.json`, `source/modules/simai_property_*.json`, `source/modules/simai_property4field_*.json`, `source/modules/simai_property4iblock_*.json`.

## Требования
Минимум: установлены `simai.framework` и `simai.property`. Дополнительно — модули `simai.property4field` и `simai.property4iblock`, если нужны расширенные типы свойств.

## Как это работает
Не найдено в локальных данных. Искомое: процесс инициализации модулей при установке. Искали в `source/modules`, `source/file-functional.md`.

## Настройка и параметры
Не найдено в локальных данных. Искомое: параметры установки модулей. Искали в `source/modules/simai_framework_*.json`, `source/sf4-structure.enriched.json`.

## Примеры из репозитория
Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "module:simai.framework",
  "kind": "module",
  "name": "simai.framework",
  "description": "Модуль фреймворка."
}
```

Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "module:simai.property",
  "kind": "module",
  "name": "simai.property",
  "description": "Модуль универсальных свойств."
}
```

## Типичные ошибки и диагностика
- Отсутствуют типы свойств → проверить установку `simai.property` и расширений `simai.property4field`/`simai.property4iblock`.
- Компоненты/мастер недоступны → убедиться, что `simai.framework` установлен.

## Что должен уметь читатель после
- Знать обязательные и дополнительные модули SF4.
- Находить описание модулей в `source/sf4-structure.enriched.json`.
- Проверять наличие модулей перед развёртыванием решения.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/modules/simai_framework_*.json`
- `source/modules/simai_property_*.json`
