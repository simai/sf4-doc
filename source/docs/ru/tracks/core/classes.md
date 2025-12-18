# Классы и подсистемы ядра

## Назначение
Фиксирует подтверждённые группы классов ядра SF4 и пример их использования.

## Где применяется
Модуль `simai.framework`: работа с конфигами, ассетами, утилитами и поиском.

## Где находится
- Узлы классов и подсистем: `source/sf4-structure.enriched.json`.
- Реализация: `source/modules/simai_framework_*.json`.

## Требования
Использовать публичные классы модуля `simai.framework`; не модифицировать файлы ядра.

## Как это работает
Не найдено в локальных данных. Искомое: полный перечень классов и их методов. Искали в `source/sf4-structure.enriched.json`, `source/modules/simai_framework_*.json`.

## Настройка и параметры
Не найдено в локальных данных. Искомое: параметры инициализации классов ядра. Искали в `source/modules/simai_framework_*.json`.

## Примеры из репозитория
Источник: `source/modules/simai_framework_251213040901_6.json`
```php
use SIMAI\Main\Configuration\Property;
use SIMAI\Main\Page\Asset;

Asset::getInstance()->load("simai.framework");
if(Property::getInstance()->get(SF_SITE_DIR, "animate_mode") == 'Y')
    Asset::getInstance()->load("animate");
```

## Типичные ошибки и диагностика
- Попытка править классы в `/simai` → использовать API без модификации ядра.
- Отсутствующий класс/namespace → сверить наличие в `source/modules/simai_framework_*.json` и автозагрузку Bitrix.

## Что должен уметь читатель после
- Находить группы классов в `source/sf4-structure.enriched.json`.
- Использовать API `Asset` и `Property` без правки ядра.
- Проверять наличие нужных классов в снапшотах модуля.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/modules/simai_framework_*.json`
