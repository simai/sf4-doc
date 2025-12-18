# Чек-листы

## Назначение
Сводные проверки развёрнутого решения SF4 перед тестированием и поставкой: целостность модулей, доступность данных в `{site_dir}/simai.data`, базовые конфиги и шаблон.

## Где применяется
Решения на SF4 (слой `{site_dir}/simai.data`) и системный шаблон `/bitrix/templates/simai.framework` при ручной проверке готовности.

## Где находится
Системные файлы фреймворка — `/simai/config/.asset.config.php`, `/simai/config/.font.config.php`; шаблон `/bitrix/templates/simai.framework`; данные сайта `{site_dir}/simai.data` (пути перечислены в `source/file-functional.md` и `source/structure.json`).

## Требования
- Установлены модули `simai.framework` и `simai.property` (см. `source/file-functional.md`).
- Шаблон `simai.framework` подключён для сайта (`source/file-functional.md`).
- Папка `{site_dir}/simai.data` доступна на запись (`source/structure.json`).

## Как это работает
Не найдено в локальных данных. Искомое: процедура выполнения чек-листов. Искали в `source/file-functional.md`, `source/sf4doc.json`, `source/sf4bx.md`.

## Настройка и параметры
- Конфиги ассетов/шрифтов: `/simai/config/.asset.config.php`, `/simai/config/.font.config.php`, а также `{site_dir}/simai.data/config/.asset.config.php` и `.font.config.php` (описаны в `source/file-functional.md`).
- Структура данных сайта: `{site_dir}/simai.data` с подпапками `config/`, `template/`, `grid/`, `include/`, `modal/`, `lang/`, `image/` (`source/structure.json`).
- Шаблон: `/bitrix/templates/simai.framework` и копии/overrides в `{site_dir}/simai.data/template` (`source/file-functional.md`).

## Примеры из репозитория
Не найдено в локальных данных. Искомое: готовые чек-листы в исходниках. Искали в `source/file-functional.md`, `source/sf4doc.json`, `source/content.json`.

## Типичные ошибки и диагностика
Не найдено в локальных данных. Искомое: подтверждённые ошибки выполнения чек-листов. Искали в `source/sf4doc.json`, `source/sf4bx.md`, `source/modules/simai_framework_*.json`.

## Что должен уметь читатель после
- Знать, что проверять в `{site_dir}/simai.data` и `/simai/config/` перед релизом.
- Убедиться в подключении модулей `simai.framework` и `simai.property`.
- Проверять наличие и заполняемость `.asset.config.php` и `.font.config.php`.
- Подтверждать использование шаблона `/bitrix/templates/simai.framework`.

## Источники истины
- `source/file-functional.md`
- `source/structure.json`
