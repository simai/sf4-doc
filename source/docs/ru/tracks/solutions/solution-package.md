# Решение как поставка

## Назначение
Фиксирует состав поставки решения SF4 и подтверждённые директории, которые входят в слой данных.

## Где применяется
Сборка/развёртывание решения на основе модуля `simai.framework` с данными сайта в `{site_dir}/simai.data`.

## Где находится
- Слой данных сайта `{site_dir}/simai.data` и его подкаталоги (`config`, `template`, `include`, `modal`, `image`, `grid`): `source/sf4-structure.enriched.json`.
- Системные шаблоны и файлы ядра (контекст для отделения кастомизаций): `source/structure.json`.

## Требования
Хранить все правки и данные решения в `{site_dir}/simai.data`; не изменять ядро `/simai` и системный шаблон `/bitrix/templates/simai.framework`.

## Как это работает
Не найдено в локальных данных. Искомое: процесс упаковки/распаковки поставки решения. Искали в `source/modules`, `source/file-functional.md`, `source/sf4-structure.enriched.json`.

## Настройка и параметры
Не найдено в локальных данных. Искомое: параметры сборки/версирования поставки. Искали в `source/modules`, `source/structure.json`.

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
  "id": "file:{site_dir}/simai.data/config/.asset.config.php",
  "kind": "file",
  "path": "{site_dir}/simai.data/config/.asset.config.php",
  "description": "Настройки ассетов для сайта."
}
```

## Типичные ошибки и диагностика
- Правки внесены в ядро `/simai` или системный шаблон → потеряются при обновлении; переносить их в `{site_dir}/simai.data`.
- Отсутствуют ключевые конфиги (`.asset.config.php`, `.font.config.php`, `.structure.config.php`) → проверить наличие файлов в `{site_dir}/simai.data/config`.

## Что должен уметь читатель после
- Определять состав слоя данных `{site_dir}/simai.data` по реестру.
- Размещать кастомизации в `{site_dir}/simai.data`, избегая правок ядра.
- Проверять наличие обязательных конфигов перед поставкой/развёртыванием.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/structure.json`
