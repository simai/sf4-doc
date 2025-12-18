# Настройки и конфигурации (site/section/page/user)

## Назначение
Описывает уровни настроек SF4 (сайт/раздел/страница/пользователь), их хранение и приоритеты переопределения.

## Где применяется
Слой сайта `{site_dir}/simai.data/config`, публичный и административный интерфейсы, модули `simai.property*`.

## Где находится
- Конфиги: `{site_dir}/simai.data/config` (файлы `.asset.config.php`, `.font.config.php`, `.framework.config.php`, `.structure.config.php`, `.demo.config.php`).
- Узлы и описания: `source/sf4-structure.enriched.json`.
- Иерархия уровней: `source/file-functional.md`.

## Требования
- Файлы конфигов присутствуют на нужных уровнях (site/section/page/user).
- Используются коды сущностей (не ID) при переносе настроек.
- Права на запись в `{site_dir}/simai.data/config`.

## Как это работает
1. Настройки читаются снизу вверх: пользователь → страница → раздел → сайт (`file-functional.md`).
2. Конфиги лежат в `{site_dir}/simai.data/config` и переопределяют базовые значения.
3. Типы полей и шаблоны берутся из модулей `simai.property*`.

## Настройка и параметры
| Файл | Назначение | Источник |
| --- | --- | --- |
| `{site_dir}/simai.data/config/.framework.config.php` | Настройки фреймворка на уровне сайта | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/config/.structure.config.php` | Структура разделов/страниц | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/config/.demo.config.php` | Демо/пресеты интерфейса | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/config/.site.config.php` | Конфигурация сайта | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/config/.iblock.config.php` | Конфиги инфоблоков (админ-формы) | `source/sf4-structure.enriched.json` |

## Примеры из репозитория
Источник: `source/file-functional.md`
```md
2. **Иерархия уровней настроек**: сайт → раздел → страница → пользователь. 
```

Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "file:{site_dir}/simai.data/config/.framework.config.php",
  "kind": "file",
  "path": "{site_dir}/simai.data/config/.framework.config.php",
  "description": "Настройки фреймворка на уровне сайта."
}
```

## Типичные ошибки и диагностика
- Конфиг размещён вне `{site_dir}/simai.data/config` → переместить в корректный путь.
- Нарушен приоритет уровней (например, правка на уровне сайта вместо страницы) → учесть порядок User > Page > Section > Site.
- Отсутствуют файлы `.framework.config.php` или `.structure.config.php` → создать по структуре.

## Что должен уметь читатель после
- Понимать приоритет наследования настроек.
- Находить и редактировать конфиги в `{site_dir}/simai.data/config`.
- Использовать типы/шаблоны свойств из модулей `simai.property*`.

## Источники истины
- `source/file-functional.md`
- `source/sf4-structure.enriched.json`
- `source/structure.json`
