# Константы и базовые пути

## Назначение
Сводит используемые в коде константы путей и настройки решения SF4.

## Где применяется
Компоненты и шаблоны модуля `simai.framework`, доступ к данным и конфигам сайта.

## Где находится
- Употребление констант в коде: `source/modules/simai_framework_*.json`.
- Пути к данным/шаблонам: `source/sf4-structure.enriched.json`.

## Требования
Использовать константы для доступа к путям вместо захардкоженных строк.

## Как это работает
Не найдено в локальных данных. Искомое: определения констант (`define(...)`). Искали в `source/modules/simai_framework_*.json`.

## Настройка и параметры
Не найдено в локальных данных. Искомое: способ переопределения констант. Искали в `source/modules/simai_framework_*.json`.

## Примеры из репозитория
Источник: `source/modules/simai_framework_251213040901_6.json`
```php
if(Property::getValue(SF_SITE_DIR, 'use_cookie') == "Y"):
    $APPLICATION->IncludeComponent(
        "simai:sf.cookie.notification",
        ".default",
        [
            "COOKIE_NAME" => "COOKIE_ARGEE",
            "COOKIE_TITLE" => Property::getValue(SF_SITE_DIR, 'title_cookie'),
            "COOKIE_TEXT" => Property::getValue(SF_SITE_DIR, 'text_cookie')
        ]
    );
endif;
```

## Типичные ошибки и диагностика
- Жёсткие пути вместо констант → риск несоответствия структуре `{site_dir}`; использовать `SF_SITE_DIR`/`SF_DATA_DIR`.
- Неинициализированные константы → проверить подключение модуля `simai.framework`.

## Что должен уметь читатель после
- Распознавать константы путей в коде SF4.
- Привязывать доступ к настройкам через `SF_SITE_DIR`.
- Искать употребления констант в снапшотах модуля.

## Источники истины
- `source/modules/simai_framework_*.json`
- `source/sf4-structure.enriched.json`
