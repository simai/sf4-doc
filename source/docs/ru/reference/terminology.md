# Термины SF4

## Назначение
Собирает канонические термины SF4 по путям, слоям и сущностям, чтобы выравнивать словарь при описании модулей, шаблона и данных сайта. Опирается только на зафиксированные узлы в `source/sf4-structure.enriched.json` и дереве `source/structure.json`.

## Где применяется
Ядро (`/simai`), слой сайта (`{site_dir}/simai.data`), системный шаблон, грид/view/block, мастер и конфиги (уровни site/section/page).

## Где находится
- Узлы и их заголовки: `source/sf4-structure.enriched.json`.
- Дерево директорий: `source/structure.json`.
- Реестры грида и блоков: `source/sf_grid.json`, `source/view.json`, `source/block.json`.

## Требования
- Использовать только термины, подтверждённые узлами в `source/sf4-structure.enriched.json` и деревом `source/structure.json`.
- Не вводить новые термины без источника.

## Как это работает
1. Базовые пути (`/simai`, `{site_dir}/simai.data`) и конфиги фиксируются в enriched-узлах.
2. Сущности грида (view/block) берутся из соответствующих JSON-реестров.
3. Компоненты и действия мастера определяются по путям в enriched.json (`/bitrix/components/simai`, `/simai/wizard/action`).

## Настройка и параметры
| Термин | Значение/описание | Где зафиксировано | Источник |
| --- | --- | --- | --- |
| `/simai` | Системная папка фреймворка; правится только разработчиками ядра | Узел `dir:/simai` | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data` | Папка данных сайта (config/template/grid/include/…) | Узел `dir:{site_dir}/simai.data` | `source/sf4-structure.enriched.json` |
| `sf.grid` | Грид: сборка страниц из строк/колонок и блоков | Узлы компонентов `simai/sf.grid` | `source/sf4-structure.enriched.json` |
| `view` / `block` | Реестры представлений и блоков для грида | JSON-списки | `source/view.json`, `source/block.json` |
| `wizard action` | Исполняемые действия мастера в `/simai/wizard/action` | Узлы `file:/simai/wizard/action/*.php` | `source/sf4-structure.enriched.json` |

## Примеры из репозитория
Источник: `source/sf4-structure.enriched.json` (фрагмент про слои данных сайта)
```json
{
  "id": "dir:{site_dir}/simai.data",
  "kind": "directory",
  "path": "{site_dir}/simai.data",
  "title": "Папка данных сайта",
  "description": "Папка данных сайта. Может быть в корне или в папке сайта."
}
```

Источник: `source/sf4-structure.enriched.json` (базовый каталог ядра)
```json
{
  "id": "dir:/simai",
  "kind": "directory",
  "path": "/simai",
  "title": "Системная папка фреймворка",
  "description": "Системная папка фреймворка; файлы/папки меняются только разработчиками фреймворка."
}
```

## Типичные ошибки и диагностика
- Использование терминов, не зафиксированных в enriched.json → проверить наличие узла и заголовка.
- Смешение слоёв (`/simai` vs `{site_dir}/simai.data`) → свериться с путями в `source/sf4-structure.enriched.json`.

## Что должен уметь читатель после
- Отвечать, что означает каждый базовый путь и сущность грида/wizard.
- Быстро находить подтверждение термина в `source/sf4-structure.enriched.json`.
- Разграничивать ядро и слой данных сайта при описании задач.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/structure.json`
- `source/view.json`, `source/block.json`, `source/sf_grid.json`
