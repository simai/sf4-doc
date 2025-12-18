# Блоки и view

## Назначение
Описывает, где лежат блоки и view для `simai:sf.grid`, как их переопределять и на что опираться при конфигурации.

## Где применяется
Слой сайта `{site_dir}/simai.data/grid` (view/block), ядро `/simai` содержит системные блоки (не править).

## Где находится
- Каталоги блоков/view в данных сайта: `source/sf4-structure.enriched.json` (узлы `{site_dir}/simai.data/grid/block` и `.../view`).
- Реестры: `source/block.json`, `source/view.json` (при наличии — `blocks_registry.json`, `views_index.json`).
- Структура и пути: `source/structure.json`.

## Требования
- Все пользовательские блоки/view размещать в `{site_dir}/simai.data/grid`.
- Использовать коды (латиница, без пробелов/кириллицы).
- Не изменять системные блоки в `/simai`.

## Как это работает
1. Грид выбирает view из `{site_dir}/simai.data/grid/view`.
2. View ссылается на блоки в `{site_dir}/simai.data/grid/block/<code>`.
3. Рендер блока выполняет `template.php`; параметры задаются в `.parameters.php`, метаданные — в `.description.php`.

## Настройка и параметры
| Элемент | Назначение | Источник |
| --- | --- | --- |
| `{site_dir}/simai.data/grid/block/<code>` | Шаблон блока (template/parameters/description) | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/grid/view/<code>` | Пресет view с набором блоков | `source/sf4-structure.enriched.json` |
| `source/block.json` | Сырой список блоков и параметров | `source/block.json` |
| `source/view.json` | Список view | `source/view.json` |

## Примеры из репозитория
Источник: `source/block.json` (блок `feedback/complex_field`)
```json
{
  "file": "simai/block/feedback/complex_field/.description.php",
  "content": "<?\nif (!defined(\"B_PROLOG_INCLUDED\") || B_PROLOG_INCLUDED!==true) die();\n\nuse Bitrix\\Main\\Localization\\Loc;\nLoc::loadMessages(__FILE__); \n\n$nameTemplate = strtoupper(basename(__DIR__));\n\nreturn array(\n\t\"NAME\" => Loc::getMessage(\"SF_GRID__\" . $nameTemplate . \"__NAME\"),\n\t\"DESCRIPTION\" => Loc::getMessage(\"SF_GRID__\" . $nameTemplate . \"__DESCRIPTION\"),\n\t\"SORT\" => 100,\n\t\"VERSION\" => \"1.0.0\",\n\t);\n?>"
}
```

## Типичные ошибки и диагностика
- Правка системных блоков в `/simai` → переносить в `{site_dir}/simai.data/grid/block`.
- Отсутствует блок или view, на который ссылается грид → создать каталог и `template.php`.
- Неверные коды (пробелы/кириллица) → переименовать в латиницу.

## Что должен уметь читатель после
- Создавать и переопределять блоки/view в `simai.data/grid`.
- Использовать реестры `block.json`/`view.json` как источник параметров.
- Проверять пути и структуру по enriched/structure.

## Источники истины
- `source/block.json`, `source/view.json`
- `source/sf4-structure.enriched.json`
- `source/structure.json`
