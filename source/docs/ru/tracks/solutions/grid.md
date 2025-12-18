# Грид (sf.grid)

## Назначение
Описывает грид `simai:sf.grid`: модель строк/колонок, источники конфигураций и параметров, а также связь с view и блоками.

## Где применяется
Слой сайта `{site_dir}/simai.data/grid` (view/block), компонент `simai:sf.grid` из модуля `simai.framework`.

## Где находится
- Поведение и паттерны параметров: `source/grid.md`.
- Конфиги строк/колонок: `source/sf_grid.json`.
- Реестры view/block: `source/view.json`, `source/block.json` (и `sf_grid_parameter_patterns.json`, если есть).
- Узлы грида в структуре: `source/sf4-structure.enriched.json`.

## Требования
- VIEW и блоки должны существовать в `{site_dir}/simai.data/grid/view|block`.
- Параметры соответствуют паттернам из `grid.md` и `sf_grid_parameter_patterns.json`.
- Пути без пробелов/кириллицы; правки только в `simai.data`.

## Как это работает
1. Компонент `simai:sf.grid` читает параметры (паттерны в `grid.md`).
2. VIEW выбирает набор блоков; оба хранятся в `{site_dir}/simai.data/grid`.
3. Конфигурации строк/колонок (если используются) можно брать из `sf_grid.json`.
4. Рендер блоков происходит по `template.php` в каталогах блоков.

## Настройка и параметры
| Источник | Назначение | Источник файла |
| --- | --- | --- |
| `sf_grid_parameter_patterns.json` | Паттерны ключей `$arParams` | `source/grid.md` (указано как источник) |
| `sf_grid.json` | Готовые конфигурации строк/колонок | `source/sf_grid.json` |
| `view.json` / `block.json` | Реестр view и блоков | `source/view.json`, `source/block.json` |
| `{site_dir}/simai.data/grid/view` | Хранение шаблонов view | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/grid/block` | Хранение шаблонов блоков | `source/sf4-structure.enriched.json` |

## Примеры из репозитория
Источник: `source/grid.md`
```md
* `blocks_registry.json` — допустимые блоки, их область (`BLOCK_SECTION`) и параметры.
* `views_index.json` — готовые пресеты (для подбора похожего варианта).
* `sf_grid_parameter_patterns.json` — **паттерны имён ключей `$arParams`** (включая `ROW_*_USE_CONDITION`, `ROW_ORDER`, `COMPOSITE_*`, фон, модификаторы, серии).
```

## Типичные ошибки и диагностика
- VIEW или блок отсутствует в `simai.data/grid` → добавить/скопировать шаблон.
- Параметры не соответствуют паттернам → свериться с `grid.md` и `sf_grid_parameter_patterns.json`.
- Неверные пути или пробелы в именах каталогов → использовать латиницу/подчёркивание.

## Что должен уметь читатель после
- Подобрать view/block и разместить их в `simai.data/grid`.
- Использовать паттерны параметров из `grid.md` при вызове компонента.
- Проверять конфигурации строк/колонок по `sf_grid.json`.

## Источники истины
- `source/grid.md`
- `source/sf_grid.json`
- `source/view.json`, `source/block.json`
- `source/sf4-structure.enriched.json`
