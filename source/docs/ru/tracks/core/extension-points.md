# Публичные точки расширения vs внутренние подсистемы

## Назначение
Отделяет подтверждённые места расширения SF4 от внутренних подсистем, которые не должны изменяться.

## Где применяется
Кастомизация фронтенда и настроек через `{site_dir}/simai.data`, расширение свойств и ассетов.

## Где находится
- Структура данных и шаблона: `source/sf4-structure.enriched.json` (узлы `{site_dir}/simai.data/*`).
- Файлы конфигов/шаблонов в слое данных: `source/structure.json`.

## Требования
Все правки выполнять в `{site_dir}/simai.data`; ядро `/simai` и системный шаблон `/bitrix/templates/simai.framework` не изменять.

## Как это работает
Не найдено в локальных данных. Искомое: список событий/обработчиков SF4 для расширений. Искали в `source/modules`, `source/file-functional.md`.

## Настройка и параметры
Не найдено в локальных данных. Искомое: параметры включения расширений или точек override. Искали в `source/structure.json`, `source/sf4-structure.enriched.json`.

## Примеры из репозитория
Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "dir:{site_dir}/simai.data/template",
  "kind": "directory",
  "path": "{site_dir}/simai.data/template",
  "title": "Шаблон (ветка template в схеме)"
}
```

Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "file:{site_dir}/simai.data/config/.asset.config.php",
  "kind": "file",
  "path": "{site_dir}/simai.data/config/.asset.config.php",
  "description": "Настройки ассетов для сайта."
}
```

## Типичные ошибки и диагностика
- Правки внесены в `/simai` → потеряются при обновлении; переносить в `{site_dir}/simai.data`.
- Ассеты правятся в ядре → использовать `{site_dir}/simai.data/config/.asset.config.php` для overrides.

## Что должен уметь читатель после
- Находить каталоги для расширений в `{site_dir}/simai.data`.
- Разделять кастомизации и внутренние файлы ядра.
- Выбирать корректные точки override для шаблонов и ассетов.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/structure.json`
