# Компоненты SIMAI (использование в решении)

## Назначение
Перечень компонентов SIMAI и их размещение в модуле `simai.framework`, с указанием основных групп и путей.

## Где применяется
Компоненты Bitrix в `/bitrix/components/simai`, используемые на страницах решения и в гриде.

## Где находится
- Узлы компонентов и аннотации: `source/sf4-structure.enriched.json` (ветка `/bitrix/components/simai`).
- Структура файлов: `source/structure.json`.
- Примеры страниц: `source/sf4doc.json`, `source/sf4bx.json`.

## Требования
- Компоненты берутся из модуля `simai.framework`; правки делаются через шаблоны в `{site_dir}/simai.data` при необходимости.
- Использовать коды компонентов (префикс `sf.`).

## Как это работает
1. Компоненты размещены в `/bitrix/components/simai` (подтверждено структура.json).
2. Шаблоны компонентов могут быть переопределены в `simai.data` по правилам Bitrix.
3. Назначения компонентов описаны в enriched-узлах.

## Настройка и параметры
| Группа | Компоненты | Источник |
| --- | --- | --- |
| iblock | `sf.iblock.list`, `sf.iblock.detail`, `sf.iblock.section`, `sf.iblock.table`, `sf.iblock.calendar`, `sf.iblock.filter` | `source/sf4-structure.enriched.json` |
| hlblock | `sf.highloadblock.grid` | `source/sf4-structure.enriched.json` |
| grid/block | `sf.grid`, `sf.block`, `sf.block.view`, `sf.block.property`, `sf.block.edit`, `sf.block.row.property`, `sf.block.col.property` | `source/sf4-structure.enriched.json` |
| feedback/forms | `sf.feedback`, `sf.feedback.appeal`, `sf.feedback.vote`, `sf.message` | `source/sf4-structure.enriched.json` |
| navigation | `sf.menu.list`, `sf.menu.sections`, `breadcrumb` | `source/sf4-structure.enriched.json` |
| content/ui | `sf.share`, `sf.cookie.notification`, `sf.rss.show`, `sf.weather`, `sf.up`, `sf.pdf.viewer`, `sf.swiper.nav`, `sf.promo`, `sf.banner.main` | `source/sf4-structure.enriched.json` |
| wizard | `sf.wizard`, `sf.wizard.stage`, `task.selector` | `source/sf4-structure.enriched.json` |

## Примеры из репозитория
Источник: `source/structure.json` (фрагмент компонента `sf.grid`)
```json
{
    "name": "sf.grid",
    "type": "folder",
    "path": "\/simai.framework\/install\/bitrix\/components\/simai\/sf.grid"
}
```

## Типичные ошибки и диагностика
- Правка системных шаблонов компонента в модуле → копировать шаблон в `{site_dir}/simai.data` и менять там.
- Использование неизвестного кода компонента → свериться с enriched-узлами.
- Проблемы с параметрами → смотреть `.parameters.php` в структуре компонента (по пути из `structure.json`).

## Что должен уметь читатель после
- Находить компоненты и их пути в модуле.
- Выбирать нужный компонент по группе и назначению.
- Понимать, где переопределять шаблоны компонентов.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/structure.json`
- `source/sf4doc.json`, `source/sf4bx.json`
