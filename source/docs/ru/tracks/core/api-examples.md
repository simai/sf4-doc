# API-примеры (ядро)

## Назначение
2–5 показательных вызовов API из ядра SF4 для ссылок в другой документации: работа с настройками `Property`, загрузка ассетов `Asset`, использование констант путей.

## Где применяется
Ядро (`/bitrix/modules/simai.framework`), системный шаблон `/bitrix/templates/simai.framework`, слой сайта `{site_dir}/simai.data` при вызовах `Property::getValue` и `Asset::getInstance()->add*`.

## Где находится
Классы `SIMAI\\Main\\Configuration\\Property`, `Bitrix\\Main\\Page\\Asset` — см. узлы `/bitrix/modules/simai.framework/lib` в `source/sf4-structure.enriched.json`. Конкретные вызовы — в снапшоте `source/modules/simai_framework_251213040901_6.json` (шаблон `/bitrix/templates/simai.framework`).

## Требования
Активен модуль `simai.framework`; системный шаблон `simai.framework` подключён. Доступ к `{site_dir}/simai.data` для чтения настроек по кодам.

## Как это работает
1. Модуль `simai.framework` загружает классы конфигурации (`Property`), утилиты (`Path`) и менеджер ассетов (`Asset`).
2. Значения конфигурации читаются по кодам и уровню (`SF_SITE_DIR`, `user` и т.д.) через `Property::getValue(...)`.
3. Результаты подставляются в параметры компонентов или в HTML/атрибуты.
4. Для подключения JS/CSS используется `Asset::getInstance()->addJs/addCss`.

## Настройка и параметры
- `Property::getValue(<scope>, <code>)` — возвращает значение свойства уровня (site/user/section/page). Источник: `source/modules/simai_framework_251213040901_6.json`.
- `Asset::getInstance()->addJs|addCss(<path>)` — регистрирует ассеты для шаблона. Источник: тот же снапшот шаблона.

## Примеры из репозитория

Источник: `source/modules/simai_framework_251213040901_6.json` (вставка компонента уведомления о cookie из системного шаблона).
```php
<? if (Property::getValue(SF_SITE_DIR, 'use_cookie') == "Y"): ?>
    <? $APPLICATION->IncludeComponent(
        "simai:sf.cookie.notification",
        ".default",
        array(
            "COMPONENT_TEMPLATE" => ".default",
            "COOKIE_NAME" => "COOKIE_ARGEE",
            "COOKIE_TITLE" => Property::getValue(SF_SITE_DIR, 'title_cookie'),
            "COOKIE_TEXT" => Property::getValue(SF_SITE_DIR, 'text_cookie'),
            "SUCCESS_BUTTON_TEXT" => Property::getValue(SF_SITE_DIR, 'success_button_text'),
            "COOKIE_AGREE_LINK" => Property::getValue(SF_SITE_DIR, 'cookie_agree_link'),
            "COOKIE_EXPIRES" => Property::getValue(SF_SITE_DIR, 'cookie_expires'),
```

Источник: `source/modules/simai_framework_251213040901_6.json` (панель разработчика в шаблоне).
```php
use Bitrix\Main\Page\Asset;
use SIMAI\Main\Configuration\Property;

$show_bitrix_panel = Property::getValue(SF_SITE_DIR, 'show_bitrix_panel');

if(Property::getValue("user", "show_bitrix_panel")!="")
    $show_bitrix_panel = Property::getValue("user", 'show_bitrix_panel');

if($show_bitrix_panel != "Y"){
    Asset::getInstance()->addJs("/bitrix/js/main/utils.js");
    Asset::getInstance()->addJs("/bitrix/js/main/sidepanel/manager.min.js");
    Asset::getInstance()->addCss("/bitrix/themes/.default/pubstyles.css");
}
```

## Типичные ошибки и диагностика
Не найдено в локальных данных. Искомое: распространённые ошибки вызовов Property/Asset. Искали в `source/sf4-structure.enriched.json`, `source/modules/simai_framework_*.json`, `source/sf4doc.json`.

## Что должен уметь читатель после
- Находить подтверждённые вызовы API в снапшотах модуля.
- Подставлять значения настроек через `Property::getValue` по кодам и уровням.
- Подключать ассеты шаблона через `Asset::getInstance()->addJs/addCss`.
- Сохранять ссылку на исходный файл при цитировании примеров.

## Источники истины
- `source/modules/simai_framework_251213040901_6.json`
- `source/sf4-structure.enriched.json`
