# Админ-инструменты и редакторы (решение)

## Назначение
Описывает административные скрипты SF4 для конфигов, работы с инфоблоками и редактор грида/блоков, а также требования к правам.

## Где применяется
Backend-скрипты в слое сайта/ядра (админка), публичный редактор инфоблоков, файловый менеджер для `simai.data`.

## Где находится
- Админ-скрипты по настройкам и инфоблокам: `source/file-functional.md` (`/simai/site/<site_code>/admin/`).
- Узлы редакторов/файлового менеджера — см. `source/sf4-structure.enriched.json` (каталоги `grid`, `config`, `include` и др. в `{site_dir}/simai.data`).

## Требования
- Права на запись в `{site_dir}/simai.data` (config/template/grid/include).
- Доступ к админ-страницам конфигов (site/section/page/demo) и редакторам грида/блоков.
- Универсальные свойства модулей `simai.property*` для форм.

## Как это работает
1. Админ-скрипты в `/simai/site/<site_code>/admin/` позволяют редактировать конфиги site/section/page/demo и формы инфоблоков.
2. Файловый менеджер создаёт/редактирует шаблоны grid/view/block прямо в `{site_dir}/simai.data`.
3. Публичный редактор инфоблоков использует уровни настроек (site/section/page/user) и типы свойств `simai.property*`.

## Настройка и параметры
| Инструмент | Путь/описание | Источник |
| --- | --- | --- |
| Админ-страницы настроек | `/simai/site/<site_code>/admin/config.site.php`, `config.section.php`, `config.page.php`, `config.demo.php` | `source/file-functional.md` |
| Управление инфоблоками | `iblock.section.edit.php`, `iblock.section.delete.php`, `iblock.element.edit.php`, `iblock.element.delete.php` | `source/file-functional.md` |
| Файловый менеджер grid/view/block | Работает с `{site_dir}/simai.data/grid` | `source/file-functional.md`, `source/sf4-structure.enriched.json` |

## Примеры из репозитория
Источник: `source/file-functional.md`
```md
**`/simai/site/<site_code>/admin/` → backend-скрипты управления**
Файлы (как на схеме):

* `config.site.php`, `config.section.php`, `config.page.php`, `config.demo.php` — страницы/скрипты админки для редактирования настроек (по уровням). 
* `iblock.section.edit.php`, `iblock.section.delete.php` — управление секциями IB. 
* `iblock.element.edit.php`, `iblock.element.delete.php` — управление элементами IB. 
```

## Типичные ошибки и диагностика
- Нет прав записи в `{site_dir}/simai.data` → появляется 403/404 при сохранении конфигов/шаблонов.
- Изменения внесены вне `simai.data` → переносить в слой данных.
- Универсальные свойства недоступны → проверить установку модулей `simai.property*`.

## Что должен уметь читатель после
- Использовать админ-страницы для настройки уровней.
- Редактировать шаблоны grid/view/block через файловый менеджер в `simai.data`.
- Проверять права и наличие модулей свойств для работы редакторов.

## Источники истины
- `source/file-functional.md`
- `source/sf4-structure.enriched.json`
- `source/structure.json`
