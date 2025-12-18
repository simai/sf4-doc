# Права доступа и безопасность

## Назначение
Фиксирует подтверждённые точки, где требуются права для работы с SF4.

## Где применяется
Админ-скрипты `/simai/site/<site_code>/admin`, запись в `{site_dir}/simai.data`, выполнение wizard actions.

## Где находится
- Админ-скрипты управления конфигами и инфоблоками: `source/file-functional.md`.
- Структура данных и конфигов (для проверки прав записи): `source/structure.json`, `source/sf4-structure.enriched.json`.

## Требования
Администраторские права на выполнение скриптов в `/simai/site/<site_code>/admin` и запись в `{site_dir}/simai.data`; установлен `simai.framework`.

## Как это работает
Не найдено в локальных данных. Искомое: точная модель прав/ролей для админки SF4. Искали в `source/file-functional.md`, `source/sf4-structure.enriched.json`.

## Настройка и параметры
Не найдено в локальных данных. Искомое: параметры доступа к wizard actions. Искали в `source/modules`, `source/structure.json`.

## Примеры из репозитория
Источник: `source/file-functional.md`
```
**`/simai/site/<site_code>/admin/` → backend-скрипты управления**
* `config.site.php`, `config.section.php`, `config.page.php`, `config.demo.php` — страницы/скрипты админки для редактирования настроек (по уровням). 
* `iblock.section.edit.php`, `iblock.section.delete.php` — управление секциями IB. 
* `iblock.element.edit.php`, `iblock.element.delete.php` — управление элементами IB. 
```

## Типичные ошибки и диагностика
- Нет записи в `{site_dir}/simai.data` → правки конфигов не сохраняются; проверить права.
- 404/403 на админ-скрипты → убедиться в наличии файлов и правах на их выполнение.
- Wizard actions недоступны → проверить права и наличие файлов в `/simai/wizard/action`.

## Что должен уметь читатель после
- Проверять права на каталоги `{site_dir}/simai.data`.
- Находить и использовать админ-скрипты из `/simai/site/<site_code>/admin`.
- Диагностировать ошибки доступа к wizard actions.

## Источники истины
- `source/file-functional.md`
- `source/structure.json`
- `source/sf4-structure.enriched.json`
