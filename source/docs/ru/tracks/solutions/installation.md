# Установка и базовая структура (решения)

## Назначение
Описывает минимальные шаги по установке модулей SF4, активации шаблона и проверке структуры данных сайта.

## Где применяется
Модуль `simai.framework` (ядро `/simai`), модуль `simai.property*`, системный шаблон `/bitrix/templates/simai.framework`, слой сайта `{site_dir}/simai.data`.

## Где находится
- Пути модульной части и компонента `simai:sf.grid`: `source/structure.json`.
- Аннотации узлов (конфиги, шаблон, данные сайта): `source/sf4-structure.enriched.json`.
- Общая схема подсистем: `source/file-functional.md`, `source/file-frontend.md`.

## Требования
- Bitrix (D7) с инфоблоками и при необходимости HL-блоками.
- Активные модули: `simai.framework`, `simai.property`; при расширении типов — `simai.property4field`, `simai.property4iblock`.
- Права на запись в `{site_dir}/simai.data`.

## Как это работает
1. Установить модуль `simai.framework` (структура в `structure.json`).
2. Подключить модуль `simai.property*` для работы настроек и свойств.
3. Выбрать системный шаблон `/bitrix/templates/simai.framework`.
4. Проверить наличие конфигов и шаблонов в `{site_dir}/simai.data` (config/template/grid).

## Настройка и параметры
| Шаг | Путь/файл | Источник |
| --- | --- | --- |
| Установка ядра | `/bitrix/modules/simai.framework` | `source/structure.json` |
| Активация шаблона | `/bitrix/templates/simai.framework` | `source/sf4-structure.enriched.json` |
| Ассеты сайта | `{site_dir}/simai.data/config/.asset.config.php` | `source/sf4-structure.enriched.json` |
| Шрифты сайта | `{site_dir}/simai.data/config/.font.config.php` | `source/sf4-structure.enriched.json` |
| Гриды/блоки | `{site_dir}/simai.data/grid/view` и `.../block` | `source/sf4-structure.enriched.json` |

## Примеры из репозитория
Источник: `source/structure.json` (фрагмент модуля `simai.framework`)
```json
{
    "name": "simai.framework",
    "type": "folder",
    "path": "\/simai.framework",
    "children": [
        {
            "name": "install",
            "type": "folder",
            "path": "\/simai.framework\/install"
        }
    ]
}
```

## Типичные ошибки и диагностика
- Не активирован шаблон `/bitrix/templates/simai.framework` → включить в настройках сайта.
- Конфиги ассетов/шрифтов отсутствуют в `{site_dir}/simai.data/config` → добавить файлы.
- Модули `simai.property*` не установлены → установить для корректной работы настроек.

## Что должен уметь читатель после
- Установить и активировать ядро и зависимые модули.
- Настроить шаблон и каталоги `{site_dir}/simai.data`.
- Выполнить минимальную проверку запуска страницы с `simai:sf.grid`.

## Источники истины
- `source/structure.json`
- `source/sf4-structure.enriched.json`
- `source/file-functional.md`
