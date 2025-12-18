# Ассеты ядра

## Назначение
Описывает базовые ассеты SF4 и подтверждённые точки их подключения.

## Где применяется
Системный шаблон `simai.framework` и подключение пакетов через `Asset`.

## Где находится
- Базовые файлы: `source/sf-full.css`, `source/sf-full.js`.
- Конфиги ассетов/шрифтов: `source/sf4-structure.enriched.json` (узлы `.asset.config.php`, `.font.config.php`), дерево в `source/structure.json`.

## Требования
Базовые ассеты не править; overrides и новые пакеты добавлять в `{site_dir}/simai.data/config/.asset.config.php` и файлы `{site_dir}/simai.data/template`.

## Как это работает
Не найдено в локальных данных. Искомое: механизм сборки пакетов из `.asset.config.php`. Искали в `source/modules`, `source/file-frontend.md`.

## Настройка и параметры
Не найдено в локальных данных. Искомое: структура массива пакетов в `.asset.config.php`. Искали в `source/structure.json`, `source/sf4-structure.enriched.json`.

## Примеры из репозитория
Источник: `source/modules/simai_framework_251213040901_6.json`
```php
Asset::getInstance()->load("lazysizes");
Asset::getInstance()->load("jquery");
Asset::getInstance()->load("simai.framework");
Asset::getInstance()->load("font-awesome");
Asset::getInstance()->load("swiper");
```

## Типичные ошибки и диагностика
- Правка базовых ассетов в `/simai` → переносить в `{site_dir}/simai.data`.
- Дубли библиотек → сверить конфиг ядра и проекта (`.asset.config.php`).

## Что должен уметь читатель после
- Находить базовые ассеты SF4.
- Подключать пакеты через `Asset::getInstance()->load(...)`.
- Размещать overrides в `{site_dir}/simai.data`.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/structure.json`
- `source/modules/simai_framework_*.json`
