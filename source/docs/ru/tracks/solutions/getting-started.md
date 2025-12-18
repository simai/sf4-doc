# Quick Start (15 минут)

## Назначение
Дает минимальный сценарий запуска SF4: активировать шаблон, проверить модули, отрисовать страницу через `simai:sf.grid` и убедиться, что override работает из `{site_dir}/simai.data`.

## Где применяется
Слой сайта `{site_dir}/simai.data`, системный шаблон `/bitrix/templates/simai.framework`, компонент `simai:sf.grid` из модуля `simai.framework`.

## Где находится
- Путь компонента `simai:sf.grid`: `source/structure.json` (узел `install/bitrix/components/simai/sf.grid`).
- Узлы данных сайта (config/template/grid): `source/sf4-structure.enriched.json`.

## Требования
- Активные модули `simai.framework` и `simai.property*` (зафиксировано в функциональных заметках).
- Доступ к `{site_dir}/simai.data` для записи.
- Системный шаблон `/bitrix/templates/simai.framework` выбран для сайта.

## Как это работает
1. Активировать шаблон `/bitrix/templates/simai.framework` (системный, узлы enriched.json).
2. Убедиться, что модули `simai.framework` и `simai.property*` доступны.
3. Подключить компонент `simai:sf.grid` на странице с нужным VIEW (реестры view/block в `simai.data/grid`).
4. Проверить наличие шаблонов view/block в `{site_dir}/simai.data/grid/view` и `.../block`.
5. Добавить override блока в `{site_dir}/simai.data/grid/block/<code>/template.php` и убедиться в изменениях.
6. Подключить пользовательские ассеты через `{site_dir}/simai.data/config/.asset.config.php` и файлы в `simai.data/template/style|js`.

## Настройка и параметры
| Шаг | Путь/параметр | Источник |
| --- | --- | --- |
| Выбор шаблона | `/bitrix/templates/simai.framework` | `source/sf4-structure.enriched.json` |
| Компонент | `/simai.framework/install/bitrix/components/simai/sf.grid` | `source/structure.json` |
| VIEW | Папка `{site_dir}/simai.data/grid/view/<view>` | `source/sf4-structure.enriched.json` |
| Блок | `{site_dir}/simai.data/grid/block/<code>/template.php` | `source/sf4-structure.enriched.json` |
| Ассеты сайта | `{site_dir}/simai.data/config/.asset.config.php` | `source/sf4-structure.enriched.json` |

## Примеры из репозитория
Источник: `source/structure.json` (фрагмент компонента `simai:sf.grid`)
```json
{
    "name": "sf.grid",
    "type": "folder",
    "path": "\/simai.framework\/install\/bitrix\/components\/simai\/sf.grid",
    "children": [
        {
            "name": ".description.php",
            "type": "file",
            "path": "\/simai.framework\/install\/bitrix\/components\/simai\/sf.grid\/.description.php"
        }
    ]
}
```

## Типичные ошибки и диагностика
- VIEW отсутствует в `{site_dir}/simai.data/grid/view` → создать каталог/шаблон view.
- Блок не переопределён из ядра → скопировать шаблон блока в `{site_dir}/simai.data/grid/block/<code>/template.php`.
- Ассеты не подключаются → проверить записи в `{site_dir}/simai.data/config/.asset.config.php`.

## Что должен уметь читатель после
- Быстро поднять страницу с `simai:sf.grid`.
- Разместить или переопределить блоки/view в `simai.data`.
- Подключить свои ассеты через конфиг сайта.

## Источники истины
- `source/structure.json`
- `source/sf4-structure.enriched.json`
