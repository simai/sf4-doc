# Данные сайта (`simai.data`)

## Назначение
Фиксирует содержимое и правила работы с `{site_dir}/simai.data`, единственным слоем для проектных правок (конфиги, шаблон, гриды, включаемые области).

## Где применяется
Слой сайта `{site_dir}/simai.data` (config/template/grid/include/modal/lang/image/property overrides).

## Где находится
- Узлы каталога данных: `source/sf4-structure.enriched.json` (id `dir:{site_dir}/simai.data` и подпапки).
- Дерево: `source/structure.json`.

## Требования
- Все пользовательские правки — только в `{site_dir}/simai.data`.
- Пути без пробелов/кириллицы.
- Не менять ядро `/simai` и системный шаблон.

## Как это работает
1. `{site_dir}/simai.data/config` хранит конфиги ассетов/шрифтов и уровней site/section/page/user.
2. `{site_dir}/simai.data/template` содержит override шаблона (style/js/meta/panel/property/template.php).
3. `{site_dir}/simai.data/grid` хранит view и block для `simai:sf.grid`.
4. Дополнительные каталоги (`include`, `modal`, `lang`, `image`) используются как ресурсы страниц.

## Настройка и параметры
| Путь | Назначение | Источник |
| --- | --- | --- |
| `{site_dir}/simai.data/config/.asset.config.php` | Ассеты уровня сайта | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/config/.font.config.php` | Шрифты сайта | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/config/.framework.config.php` | Настройки фреймворка на уровне сайта | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/template` | Override шаблона (style/js/meta/panel/property) | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/grid/view` / `block` | Шаблоны view и блоков грида | `source/sf4-structure.enriched.json` |

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

Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "dir:{site_dir}/simai.data/template",
  "kind": "directory",
  "path": "{site_dir}/simai.data/template",
  "title": "Шаблон (ветка template в схеме)"
}
```

## Типичные ошибки и диагностика
- Правки в `/simai` вместо `{site_dir}/simai.data` → перенести в слой данных.
- Отсутствуют конфиги в `simai.data/config` → создать по структуре.
- Путь содержит пробелы/кириллицу → переименовать.

## Что должен уметь читатель после
- Размещать конфиги, шаблоны и гриды в правильных каталогах `simai.data`.
- Проверять структуру по enriched/structure.
- Обновлять ассеты/шрифты и блоки без изменения ядра.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/structure.json`
