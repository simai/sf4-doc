# Конвенции и код-стайл

## Назначение
Зафиксировать подтверждённые правила оформления и размещения файлов SF4.

## Где применяется
Слой данных `{site_dir}/simai.data` и системный шаблон `simai.framework`.

## Где находится
- Пути и узлы каталога данных: `source/sf4-structure.enriched.json`.
- Структура каталога: `source/structure.json`.

## Требования
Не изменять ядро `/simai` и системный шаблон; все правки — в `{site_dir}/simai.data`.

## Как это работает
Не найдено в локальных данных. Искомое: формализованный код-стайл (PSR-12, D7). Искали в `source/file-functional.md`, `source/file-frontend.md`.

## Настройка и параметры
Не найдено в локальных данных. Искомое: обязательные соглашения по именованию. Искали в `source/sf4-structure.enriched.json`, `source/structure.json`.

## Примеры из репозитория
Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "dir:{site_dir}/simai.data",
  "kind": "directory",
  "path": "{site_dir}/simai.data",
  "title": "Папка данных сайта",
  "description": "Папка данных сайта. Может быть в корне или в папке сайта."
}
```

## Типичные ошибки и диагностика
- Правки сделаны в `/simai` → перенести в `{site_dir}/simai.data`.
- Неверное размещение конфигов → сверить с `source/structure.json`.

## Что должен уметь читатель после
- Размещать правки в `{site_dir}/simai.data`.
- Проверять структуру по `source/structure.json`.
- Избегать правок системного шаблона и ядра.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/structure.json`
