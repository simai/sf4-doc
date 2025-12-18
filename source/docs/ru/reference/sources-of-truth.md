# Карта источников истины

## Назначение
Фиксирует, какие файлы из каталога `source/` являются «истиной» для структуры, параметров и примеров SF4. Помогает не смешивать уровни данных и всегда ссылаться на подтвержденные артефакты при написании документации и примеров.

## Где применяется
Слой документации; используется при описании ядра, шаблона, слоя сайта, компонентов, грида, блоков, свойств и ассетов.

## Где находится
- Перечни и пути истинных файлов лежат в самом каталоге `source/` (см. список ниже).
- Структура проекта: `source/structure.json`.
- Аннотации по узлам: `source/sf4-structure.enriched.json`.

## Требования
- Опираемся только на файлы из `source/`.
- Приоритет: структуры (`structure.json`), аннотации (`sf4-structure.enriched.json`), точные фрагменты (`content.json`), далее методические тексты (`*.md`, JSON-выгрузки).
- Никаких внешних или не подтверждённых путей.

## Как это работает
1. Структура путей/директорий берется из `source/structure.json`.
2. Назначения узлов и подсистем — из `source/sf4-structure.enriched.json`.
3. Точные вставки кода/JSON — из `source/content.json` (или конкретных файлов `source/*.md/json/css/js`).
4. Поведение подсистем и описательные тексты — из профильных `source/*.md` (например, `grid.md`, `sf4doc.md`, `sf4bx.md`).
5. Если есть агрегаты (`sf_grid.json`, `view.json`, `block.json`, `blocks_registry.json`, `views_index.json`, `sf_grid_parameter_patterns.json`), их используют как индексы, но не вместо структуры.

## Настройка и параметры
| Имя/файл | Назначение | Приоритет | Источник |
| --- | --- | --- | --- |
| `source/structure.json` | Истина по дереву путей | 1 | `source/structure.json` |
| `source/sf4-structure.enriched.json` | Аннотации узлов/назначения | 2 | `source/sf4-structure.enriched.json` |
| `source/content.json` | Точные фрагменты кода/JSON | 3 | `source/content.json` |
| `source/grid.md`, `source/sf_grid.json`, `source/view.json`, `source/block.json` | Поведение и реестры грида/view/block | 4 | соответствующие файлы |

## Примеры из репозитория
Источник: `source/structure.json` (корневой фрагмент структуры)
```json
{
    "project_name": "Название Проекта",
    "generated_at": "2025-10-20T17:32:13+03:00",
    "structure": {
        "name": "simai.framework",
        "type": "folder",
        "path": "\/",
        "children": [
            {
                "name": "simai.framework",
                "type": "folder",
                "path": "\/simai.framework"
            }
        ]
    }
}
```

## Типичные ошибки и диагностика
- Использование файлов вне `source/` как «истины» → невалидно, нужно ссылаться на `structure.json`/`sf4-structure.enriched.json`.
- Отсутствие примеров → искать в `content.json` или профильных `source/*.md`/`*.json`; если нет, помечать как «Не найдено в локальных данных».

## Что должен уметь читатель после
- Понимать порядок приоритета источников.
- Знать, какие файлы отвечают за структуру, аннотации и примеры.
- Проверять наличие нужного файла в `source/` перед ссылкой в документации.

## Источники истины
- `source/structure.json`
- `source/sf4-structure.enriched.json`
- `source/content.json`
