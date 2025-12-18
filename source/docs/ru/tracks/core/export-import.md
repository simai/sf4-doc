# Экспорт/импорт и миграции

## Назначение
Описывает подтверждённые действия импорта/экспорта в SF4 через wizard actions.

## Где применяется
Мастер `/simai/wizard/action` в модуле `simai.framework`.

## Где находится
- Список действий: `source/sf4-structure.enriched.json` (узлы `action:*`).
- Код actions: `source/modules/simai_framework_*.json`.

## Требования
Доступ к `/simai/wizard/action`, установленный модуль `simai.framework`.

## Как это работает
Не найдено в локальных данных. Искомое: сценарии вызова actions из мастера. Искали в `source/modules/simai_framework_*.json`.

## Настройка и параметры
Не найдено в локальных данных. Искомое: параметры actions (например, пути архивов). Искали в `source/modules/simai_framework_*.json`.

## Примеры из репозитория
Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "action:iblock.import.archive.sveden",
  "kind": "action",
  "code": "iblock.import.archive.sveden",
  "title": "Импорт архива сведений",
  "description": "Импорт архива сведений об образовательной организации"
}
```

Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "action:file.create",
  "kind": "action",
  "code": "file.create",
  "title": "Создание файла",
  "description": "Создаёт файл с текстовым содержимым."
}
```

## Типичные ошибки и диагностика
- 404 на action → проверить наличие файла в `/simai/wizard/action` и права.
- Пакет не найден при импорте → убедиться в корректном пути к архиву в параметрах action.

## Что должен уметь читатель после
- Находить действия импорта/экспорта в `source/sf4-structure.enriched.json`.
- Проверять наличие файлов actions перед запуском мастера.
- Понимать, что параметры действий должны указывать на доступные архивы/конфиги.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/modules/simai_framework_*.json`
