# Ассеты и шрифты (уровень решения)

## Назначение
Показывает, где объявляются и настраиваются ассеты и шрифты на уровне решения: конфиги, физические файлы и порядок подключения.

## Где применяется
Ядро `/simai` (базовые конфиги), слой сайта `{site_dir}/simai.data` (override/дополнения), системный шаблон.

## Где находится
- Конфиг ассетов ядра: `/simai/config/.asset.config.php` (узел enriched.json).
- Конфиги ассетов/шрифтов сайта: `{site_dir}/simai.data/config/.asset.config.php`, `.font.config.php`.
- Базовые ассеты: `source/sf-full.css`, `source/sf-full.js`.

## Требования
- Пути к файлам без пробелов/кириллицы (отмечено в функциональных заметках).
- Конфиги ассетов и шрифтов должны существовать в `{site_dir}/simai.data/config`.
- Правки не вносить в `/simai/config`, только в `simai.data/config`.

## Как это работает
1. Базовые пакеты CSS/JS описаны в `/simai/config/.asset.config.php`.
2. Проектные ассеты добавляются или переопределяются в `{site_dir}/simai.data/config/.asset.config.php`; файлы лежат в `simai.data/template/style|js`.
3. Шрифты описываются в `{site_dir}/simai.data/config/.font.config.php` с указанием источников.
4. Ассеты подключаются шаблоном, используя конфиги ядра + сайта.

## Настройка и параметры
| Файл | Назначение | Источник |
| --- | --- | --- |
| `/simai/config/.asset.config.php` | Реестр ассетов ядра (версии/пакеты) | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/config/.asset.config.php` | Ассеты уровня сайта | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/config/.font.config.php` | Шрифты сайта | `source/sf4-structure.enriched.json` |
| `simai.data/template/style|js` | Физические файлы кастомных ассетов | `source/sf4-structure.enriched.json` |

## Примеры из репозитория
Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "file:{site_dir}/simai.data/config/.font.config.php",
  "kind": "file",
  "path": "{site_dir}/simai.data/config/.font.config.php",
  "description": "Настройки шрифтов (наборы/параметры)."
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
- Изменение `/simai/config/.asset.config.php` вместо site-override → перенести правки в `{site_dir}/simai.data/config/.asset.config.php`.
- Отсутствие файлов `.asset.config.php`/`.font.config.php` в `simai.data/config` → создать по структуре.
- Пути к шрифтам содержат пробелы/кириллицу → исправить и перезапустить подключение.

## Что должен уметь читатель после
- Добавлять/переопределять ассеты и шрифты через `simai.data/config`.
- Размещать кастомные CSS/JS в `simai.data/template`.
- Проверять корректность подключений по конфигам и структуре.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/sf-full.css`, `source/sf-full.js`
- `source/structure.json`
