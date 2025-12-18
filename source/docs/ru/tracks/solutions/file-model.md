# Файловая модель SF4

## Назначение
Фиксирует, как разложены файлы SF4: ядро `/simai`, системный шаблон и слой данных сайта `{site_dir}/simai.data`. Используется как единый словарь путей для всех разделов документации.

## Где применяется
Ядро модуля `simai.framework`, системный шаблон `/bitrix/templates/simai.framework`, слой сайта `{site_dir}/simai.data` (config/template/grid/include/lang/modal/image/property overrides).

## Где находится
- Дерево путей и файлов: `source/structure.json`.
- Аннотации по узлам: `source/sf4-structure.enriched.json`.
- Реестры грида/view/block: `source/sf_grid.json`, `source/view.json`, `source/block.json`.

## Требования
- Хранить пользовательские правки только в `{site_dir}/simai.data`.
- Ядро `/simai` и системный шаблон не изменять (enriched-узлы отмечены как системные).
- Проверять пути по `structure.json` перед ссылкой в документации.

## Как это работает
1. `/simai` содержит системные файлы, ассеты и конфиги фреймворка (узлы enriched.json).
2. `/bitrix/templates/simai.framework` подключает базовый layout и ассеты; кастомизация идёт через копии в `{site_dir}/simai.data/template`.
3. `{site_dir}/simai.data` хранит конфиги (`config/.asset.config.php`, `.font.config.php`, `.framework.config.php`, `.structure.config.php`), шаблонные файлы, гриды/view/block и контентные каталоги.

## Настройка и параметры
| Путь | Назначение | Источник |
| --- | --- | --- |
| `/simai/config/.asset.config.php` | Настройки ассетов фреймворка (версии/пакеты) | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/config/.asset.config.php` | Настройки ассетов уровня сайта | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/config/.font.config.php` | Настройки шрифтов сайта | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/template` | Шаблонные override’ы (style/js/meta/panel/property) | `source/sf4-structure.enriched.json` |

## Примеры из репозитория
Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "dir:/simai",
  "kind": "directory",
  "path": "/simai",
  "title": "Системная папка фреймворка",
  "description": "Системная папка фреймворка; файлы/папки меняются только разработчиками фреймворка."
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
- Правки в `/simai` или системном шаблоне → перенести в `{site_dir}/simai.data`.
- Несогласованность путей → свериться с `structure.json` и enriched-узлами.
- Отсутствие конфигов `.asset.config.php`/`.font.config.php` → проверить наличие файлов в `{site_dir}/simai.data/config`.

## Что должен уметь читатель после
- Навигировать по слоям `/simai`, `/bitrix/templates/simai.framework`, `{site_dir}/simai.data`.
- Определять, где хранить конфиги, шаблоны и блоки.
- Проверять любые пути по `structure.json` и enriched-аннотациям.

## Источники истины
- `source/structure.json`
- `source/sf4-structure.enriched.json`
- `source/sf_grid.json`, `source/view.json`, `source/block.json`
