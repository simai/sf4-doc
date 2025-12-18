# Структура фреймворка (Track A)

## Назначение
Дает обзор структуры фреймворка SF4: модуль `simai.framework`, системный шаблон и слой данных сайта. Опирается на дерево `source/structure.json`, аннотации `source/sf4-structure.enriched.json` и функциональные заметки.

## Где применяется
Ядро `/simai`, системный шаблон `/bitrix/templates/simai.framework`, слой сайта `{site_dir}/simai.data`, компоненты `/bitrix/components/simai`, actions `/simai/wizard/action`.

## Где находится
- Дерево модульной части и файлов: `source/structure.json`.
- Аннотации узлов (ядро, компоненты, wizard, конфиги): `source/sf4-structure.enriched.json`.
- Функциональная схема подсистем: `source/file-functional.md`.
- Фронтенд-конфиги и слои: `source/file-frontend.md`.

## Требования
- Не изменять файлы ядра `/simai` и системного шаблона; кастомизации — только в `{site_dir}/simai.data`.
- Наличие модулей `simai.framework` и `simai.property*` (упомянуто в функциональном файле).
- Конфиги ассетов/шрифтов присутствуют в `/simai/config/` и `{site_dir}/simai.data/config/`.

## Как это работает
1. Модуль `simai.framework` включает ядро `/simai`, компоненты (`install/bitrix/components/simai`), wizard actions (`/simai/wizard/action`) и конфиги (structure/enriched).
2. Системный шаблон `/bitrix/templates/simai.framework` подключает базовые ассеты; адаптации копируются в `{site_dir}/simai.data/template`.
3. `{site_dir}/simai.data` хранит конфиги уровней, ассеты сайта, шаблоны, гриды/view/block и прикладные каталоги (`include`, `modal`, `lang`, `image`).

## Настройка и параметры
| Путь/узел | Назначение | Источник |
| --- | --- | --- |
| `/simai/config/.asset.config.php` | Настройки ассетов фреймворка | `source/sf4-structure.enriched.json` |
| `/simai/wizard/action` | Набор действий мастера (file./iblock./site./…) | `source/sf4-structure.enriched.json` |
| `/bitrix/components/simai` | Компоненты SF4 (iblock, grid, feedback, wizard и др.) | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/config/.asset.config.php` | Ассеты уровня сайта | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/template` | Override системного шаблона | `source/sf4-structure.enriched.json` |

## Примеры из репозитория
Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "file:/simai/config/.asset.config.php",
  "kind": "file",
  "path": "/simai/config/.asset.config.php",
  "title": "Настройки ассетов",
  "description": "Настройки ассетов фреймворка (версии/пакеты)."
}
```

Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "dir:/simai/wizard/action",
  "kind": "directory",
  "path": "/simai/wizard/action",
  "title": "Действия мастера (wizard)"
}
```

## Типичные ошибки и диагностика
- Правки в системных файлах `/simai`/`/bitrix/templates/simai.framework` → переносить в `{site_dir}/simai.data`.
- Отсутствуют конфиги ассетов/шрифтов → проверить наличие файлов в `/simai/config` и `{site_dir}/simai.data/config`.
- Не найден action/компонент → свериться с узлами enriched.json и деревом `structure.json`.

## Что должен уметь читатель после
- Ориентироваться в слое ядра, системном шаблоне и данных сайта.
- Находить компоненты и actions по путям из enriched/structure.
- Разносить правки в правильный слой (`simai.data`).

## Источники истины
- `source/structure.json`
- `source/sf4-structure.enriched.json`
- `source/file-functional.md`, `source/file-frontend.md`
