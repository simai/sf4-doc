# Универсальные свойства (SIMAI Property)

## Назначение
Фиксирует, как описываются типы данных и шаблоны отображения для форм/настроек SF4, где лежат файлы свойств и какие модули отвечают за их реализацию.

## Где применяется
Модули `simai.property*`, шаблоны свойств в `/simai/property`, конфиги уровней `{site_dir}/simai.data/config`, публичный/админ интерфейсы.

## Где находится
- Каталог свойств: `/simai/property` (узел enriched.json).
- Паттерн файлов свойства: `.description.php`, `edit.php`, `filter.php`, `view.php` (enriched.json).
- Модули: `source/modules/simai_property_*.json`, `simai_property4field_*.json`, `simai_property4iblock_*.json`.

## Требования
- Активные модули `simai.property` (и дополнения при необходимости).
- Файлы свойств следуют паттерну (описание/редактор/фильтр/view).
- Не изменять системные файлы `/simai/property`; расширения — отдельно.

## Как это работает
1. Модуль `simai.property` ставит каталог `/simai/property` с шаблонами свойств.
2. Каждое свойство описывается набором файлов по паттерну из enriched.json.
3. Формы настроек (site/section/page/user) и публичный редактор используют эти типы/шаблоны.

## Настройка и параметры
| Узел/паттерн | Назначение | Источник |
| --- | --- | --- |
| `/simai/property` | Каталог универсальных свойств | `source/sf4-structure.enriched.json` |
| `pattern:/simai/property/<property_code>` | Требуемые файлы свойства (`.description.php`, `edit.php`, `filter.php`, `view.php`) | `source/sf4-structure.enriched.json` |
| Модули `simai.property*` | Реализация типов/шаблонов свойств | `source/sf4-structure.enriched.json`, `source/modules/simai_property_*.json` |

## Примеры из репозитория
Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "dir:/simai/property",
  "kind": "directory",
  "path": "/simai/property",
  "title": "Универсальные свойства",
  "notes": [
    "Ставится модулем simai.property."
  ]
}
```

Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "pattern:/simai/property/<property_code>",
  "kind": "pattern",
  "title": "Паттерн универсального свойства",
  "fields": {
    "required_files": [
      ".description.php",
      "edit.php",
      "filter.php",
      "view.php"
    ]
  }
}
```

## Типичные ошибки и диагностика
- Отсутствует один из файлов паттерна → добавить `.description.php`, `edit.php`, `filter.php`, `view.php`.
- Правки в системных файлах `/simai/property` → выносить в отдельные расширения/модули.
- Модуль `simai.property` не установлен → установить, иначе формы настроек не работают.

## Что должен уметь читатель после
- Определять структуру и файлы свойства по паттерну.
- Использовать модули `simai.property*` для типов/шаблонов.
- Расширять свойства без изменений системного каталога.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/modules/simai_property_*.json`, `source/modules/simai_property4field_*.json`, `source/modules/simai_property4iblock_*.json`
- `source/structure.json`
