# Локализация

## Назначение
Описывает подтверждённые пути для языковых файлов и доступные действия по выбору языка.

## Где применяется
Слой данных сайта `{site_dir}/simai.data` и wizard actions модуля `simai.framework`.

## Где находится
- Директория языковых файлов: `{site_dir}/simai.data/lang` (`source/sf4-structure.enriched.json`).
- Устаревший action выбора языка: `action:language.choice` (`source/sf4-structure.enriched.json`).

## Требования
Хранить переводные строки в `{site_dir}/simai.data/lang`; не изменять системные файлы ядра `/simai` и шаблона `/bitrix/templates/simai.framework`.

## Как это работает
Не найдено в локальных данных. Искомое: механизм подключения lang-файлов в компонентах/блоках SF4. Искали в `source/file-functional.md`, `source/file-frontend.md`, `source/modules`.

## Настройка и параметры
Не найдено в локальных данных. Искомое: параметры выбора языка или привязки lang-файлов к компонентам. Искали в `source/structure.json`, `source/sf4-structure.enriched.json`.

## Примеры из репозитория
Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "dir:{site_dir}/simai.data/lang",
  "kind": "directory",
  "path": "{site_dir}/simai.data/lang",
  "title": "Языковые файлы (lang)"
}
```

Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "action:language.choice",
  "kind": "action",
  "code": "language.choice",
  "title": "Выбор языка (устарело)",
  "description": "Выбор языка (устарел)."
}
```

## Типичные ошибки и диагностика
- Переводы пропали после обновления ядра → убедиться, что overrides лежат в `{site_dir}/simai.data/lang`, а не в `/simai`.
- Попытка использовать `language.choice` в мастере → action помечен как устаревший.

## Что должен уметь читатель после
- Найти каталог `{site_dir}/simai.data/lang` и хранить там переводы.
- Избегать правок системных lang-файлов.
- Знать о наличии устаревшего action `language.choice`.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/structure.json`
