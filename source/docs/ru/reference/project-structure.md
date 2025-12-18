# Структура проекта SF4

## Назначение
2–5 предложений: описывает, как разложены файлы SF4: модуль, шаблон и слой данных сайта. Является канонической точкой для путей и деревьев директорий.

## Где применяется
Слой сайта (структура данных `{site_dir}/simai.data`), ядро (модуль `simai.framework`), системный шаблон `/bitrix/templates/simai.framework`.

## Где находится
- Дерево модульной части и установочных файлов: `source/structure.json` (узлы `/simai.framework/...`).
- Аннотации по узлам: `source/sf4-structure.enriched.json`.
- Слои проекта: `/simai` (ядро внутри модуля), `/bitrix/templates/simai.framework` (системный шаблон), `{site_dir}/simai.data` (данные сайта).

## Требования
- Наличие модулей `simai.framework` и `simai.property*` (используются слоями структуры; подтверждено `source/sf4-structure.enriched.json`).
- Права на запись в `{site_dir}/simai.data` (хранение кастомизаций).
- Понимание путей из `source/structure.json`.

## Как это работает
1. Модуль `simai.framework` содержит ядро `/simai`, компоненты (`install/bitrix/components/simai`), actions мастера (`/simai/wizard/action`), классы и конфиги (см. `source/structure.json`).
2. Системный шаблон `/bitrix/templates/simai.framework` подключает базовые ассеты и layout (пути в enriched-узлах).
3. Все пользовательские данные/override хранятся в `{site_dir}/simai.data` (config/template/grid/include/modal/lang/image и др.).
4. Обновления ядра не трогают `{site_dir}/simai.data`, поэтому все кастомизации живут там.

## Настройка и параметры
| Имя | Где задано | Назначение | Источник |
| --- | --- | --- | --- |
| `project_name` | `source/structure.json` (ключ) | Название проекта в снимке структуры | `source/structure.json` |
| `/simai.framework/install/bitrix/components/simai` | `source/structure.json` (path) | Каталог компонентов SIMAI в модуле | `source/structure.json` |
| `{site_dir}/simai.data/config/.asset.config.php` | `source/sf4-structure.enriched.json` (узлы config) | Конфиги ассетов уровня сайта | `source/sf4-structure.enriched.json` |

## Примеры из репозитория
Источник: `source/structure.json` (фрагмент корня модуля)
```json
{
    "name": "simai.framework",
    "type": "folder",
    "path": "\/simai.framework",
    "children": [
        {
            "name": "admin",
            "type": "folder",
            "path": "\/simai.framework\/admin"
        }
    ]
}
```

## Типичные ошибки и диагностика
- Не найден путь в структуре → сверить `source/structure.json` и аннотации enriched.json.
- Пользовательские правки сделаны в `/simai` → нарушено правило кастомизаций; перенести в `{site_dir}/simai.data`.

## Что должен уметь читатель после
- Понимать, где лежат модуль, шаблон и слой данных.
- Находить конфиги/компоненты/мастера по путям из структуры.
- Знать, что кастомизации делаются только в `{site_dir}/simai.data`.
- Проверять структуру по `source/structure.json` и enriched-аннотациям.

## Источники истины
- `source/structure.json`
- `source/sf4-structure.enriched.json`
