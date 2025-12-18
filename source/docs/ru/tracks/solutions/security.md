# Права и безопасность (практика)

## Назначение
Фиксирует подтверждённые точки доступа, которые требуют прав записи и администрирования в решениях на SF4.

## Где применяется
Админ-скрипты в `/simai/site/<site_code>/admin`, слои данных `{site_dir}/simai.data`, wizard actions `/simai/wizard/action`.

## Где находится
- Админ-страницы управления конфигами и инфоблоками: `source/file-functional.md`.
- Слой данных `{site_dir}/simai.data` с конфигами/шаблонами: `source/structure.json`, `source/sf4-structure.enriched.json`.
- Список wizard actions: `source/sf4-structure.enriched.json`.

## Требования
Права администратора на выполнение админ-скриптов и на запись в `{site_dir}/simai.data`; установленные модули `simai.framework` и `simai.property`.

## Как это работает
Не найдено в локальных данных. Искомое: модель прав и проверки безопасности в компонентах/мастере SF4. Искали в `source/file-functional.md`, `source/sf4-structure.enriched.json`, `source/modules`.

## Настройка и параметры
Не найдено в локальных данных. Искомое: параметры разграничения прав для мастера и редакторов. Искали в `source/structure.json`, `source/file-functional.md`.

## Примеры из репозитория
Источник: `source/file-functional.md`
```
**`/simai/site/<site_code>/admin/` → backend-скрипты управления**
Файлы (как на схеме):

* `config.site.php`, `config.section.php`, `config.page.php`, `config.demo.php` — страницы/скрипты админки для редактирования настроек (по уровням). 
* `iblock.section.edit.php`, `iblock.section.delete.php` — управление секциями IB. 
* `iblock.element.edit.php`, `iblock.element.delete.php` — управление элементами IB. 
```

## Типичные ошибки и диагностика
- 403/404 при запуске actions → проверить наличие файлов в `/simai/wizard/action` и права на выполнение.
- Конфиги/шаблоны не сохраняются → нет записи в `{site_dir}/simai.data`.
- Редакторы инфоблоков недоступны → нет прав на админ-скрипты в `/simai/site/<site_code>/admin`.

## Что должен уметь читатель после
- Определять, какие каталоги требуют прав записи (`{site_dir}/simai.data`).
- Проверять наличие и доступность админ-скриптов в `/simai/site/<site_code>/admin`.
- Понимать, что запуск wizard actions требует прав и наличия файлов в `/simai/wizard/action`.

## Источники истины
- `source/file-functional.md`
- `source/structure.json`
- `source/sf4-structure.enriched.json`
