# Шаблоны

## Назначение
Описывает системный шаблон SIMAI и место для пользовательских override в `{site_dir}/simai.data/template`.

## Где применяется
Системный шаблон сайта, слой данных `{site_dir}/simai.data/template`, конфиги ассетов `{site_dir}/simai.data/config`.

## Где находится
- Единый системный шаблон: упомянут в `source/SIMAI-SF4 Курс разработчика.md` как `/bitrix/templates/simai.framework`.
- Путь override шаблона в данных сайта: `source/sf4-structure.enriched.json` (узел `{site_dir}/simai.data/template`).

## Требования
- Не править системный шаблон напрямую; все изменения — через `{site_dir}/simai.data/template`.
- Пути без пробелов/кириллицы.
- Конфиги ассетов/шрифтов в `{site_dir}/simai.data/config`.

## Как это работает
1. Системный шаблон рендерит layout и подключает базовые ассеты.
2. Override и добавления (meta/style/js/panel/property/template.php) размещаются в `{site_dir}/simai.data/template`.
3. Ассеты подключаются через `{site_dir}/simai.data/config/.asset.config.php` и файлы `template/style|js`.

## Настройка и параметры
| Путь | Назначение | Источник |
| --- | --- | --- |
| `/bitrix/templates/simai.framework` | Системный шаблон (layout/ассеты) | `source/SIMAI-SF4 Курс разработчика.md` |
| `{site_dir}/simai.data/template` | Override шаблона (style/js/meta/panel/property/template.php) | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/config/.asset.config.php` | Подключение кастомных ассетов | `source/sf4-structure.enriched.json` |

## Примеры из репозитория
Источник: `source/SIMAI-SF4 Курс разработчика.md`
```md
Это единый системный шаблон для всех решений на базе SIMAI Framework 4. Находится по адресу **/bitrix/templates/simai.framework**
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
- Правки в системном шаблоне → перенести в `{site_dir}/simai.data/template`.
- Ассеты подключены напрямую без конфига → добавить в `.asset.config.php` и разместить файлы в `template/style|js`.
- Пробелы/кириллица в путях override → исправить.

## Что должен уметь читатель после
- Находить системный шаблон и слой override.
- Подключать кастомные ассеты и файлы шаблона через `simai.data`.
- Соблюдать правило «ядро/системный шаблон не править».

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/SIMAI-SF4 Курс разработчика.md`
- `source/structure.json`
