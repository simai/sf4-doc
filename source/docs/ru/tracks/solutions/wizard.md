# Мастер (wizard) и actions

## Назначение
Описывает пошаговый мастер SF4, его компоненты и actions, а также паттерны файлов для шагов и действий.

## Где применяется
Компоненты `sf.wizard`, `sf.wizard.stage`, actions в `/simai/wizard/action`, конфиги мастера (если используются) в слое сайта.

## Где находится
- Каталог действий мастера: `source/sf4-structure.enriched.json` (узел `/simai/wizard/action`).
- Паттерн action: `.description.php`, `action.php` (enriched.json).
- Паттерн мастера: `.wizard.config.php`, `index.php` (enriched.json).
- Структура компонентов: `source/structure.json`.

## Требования
- Actions присутствуют в `/simai/wizard/action`.
- Компоненты `sf.wizard` и `sf.wizard.stage` доступны.
- При конфигурировании шагов соблюдать паттерн файлов.

## Как это работает
1. Контейнер `sf.wizard` выводит мастер.
2. Шаг `sf.wizard.stage` исполняет один или несколько actions из `/simai/wizard/action`.
3. Каждый action следует паттерну (`.description.php`, `action.php`); при необходимости используются lang-файлы.
4. Конфигурация мастера может описывать последовательность шагов и параметры (по паттерну enriched.json).

## Настройка и параметры
| Узел/паттерн | Назначение | Источник |
| --- | --- | --- |
| `/simai/wizard/action` | Каталог действий | `source/sf4-structure.enriched.json` |
| `pattern:/simai/wizard/action/<action_code>` | Файлы `.description.php`, `action.php` (опц. `lang`) | `source/sf4-structure.enriched.json` |
| `pattern:/simai/wizard/<wizard_code>` | Файлы мастера: `.wizard.config.php`, `index.php` | `source/sf4-structure.enriched.json` |
| Компоненты `sf.wizard`, `sf.wizard.stage` | Рендер мастера и шагов | `source/structure.json` |

## Примеры из репозитория
Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "pattern:/simai/wizard/action/<action_code>",
  "kind": "pattern",
  "title": "Паттерн action для мастера",
  "fields": {
    "required_files": [
      ".description.php",
      "action.php"
    ],
    "optional_dirs": [
      "lang"
    ]
  }
}
```

Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "pattern:/simai/wizard/<wizard_code>",
  "kind": "pattern",
  "title": "Паттерн мастера (wizard)",
  "fields": {
    "required_files": [
      ".wizard.config.php",
      "index.php"
    ]
  }
}
```

## Типичные ошибки и диагностика
- Отсутствует один из файлов паттерна action → добавить `.description.php` и `action.php`.
- Правки в системных actions без копии → оформлять новые действия отдельно.
- Не найден компонент `sf.wizard`/`sf.wizard.stage` → проверить пути в `structure.json`.

## Что должен уметь читатель после
- Находить и описывать actions в `/simai/wizard/action`.
- Конфигурировать мастер по паттерну файлов.
- Использовать компоненты `sf.wizard` и `sf.wizard.stage` для шагов.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/structure.json`
- `source/modules/simai_framework_*.json`
