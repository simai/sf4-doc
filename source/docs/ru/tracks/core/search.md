# Интеграция с поиском Bitrix

## Назначение
Фиксирует подтверждённый обработчик поиска SF4 для корректировки URL результатов.

## Где применяется
Модуль `simai.framework`, обработка событий поиска Bitrix.

## Где находится
- Код обработчика `OnSearchGetURL`: `source/modules/simai_framework_*.json`.
- Расположение компонента/модуля: `source/sf4-structure.enriched.json`.

## Требования
Модуль `simai.framework` должен быть подключён, чтобы обработчик был доступен.

## Как это работает
При событии `OnSearchGetURL` проверяется тип результата и для инфоблоков подставляется корректный URL (в т.ч. с `UF_SECTION_URL`).

## Настройка и параметры
Не найдено в локальных данных. Искомое: регистрация обработчика в init.php или module.php. Искали в `source/modules/simai_framework_*.json`.

## Примеры из репозитория
Источник: `source/modules/simai_framework_251213040901_6.json`
```php
public static function OnSearchGetURL($arFields){
    $url = $arFields["URL"];
    if($arFields['MODULE_ID'] == 'iblock'){
        if($arFields['ITEM_ID'] == intval($arFields['ITEM_ID'])){
            \CModule::IncludeModule("iblock");
            $res = \CIBlock::GetByID($arFields['PARAM2']);
            if($ar_res = $res->GetNext()){
                $arFields["URL"] = $ar_res["DETAIL_PAGE_URL"];
            }
            if(strpos($arFields['URL'],'#UF_SECTION_URL#') !==false){
              $res = \CIBlockElement::GetByID($arFields["ITEM_ID"]);
              if($ar_res = $res->GetNext()){
                  $rsSections = \CIBlockSection::GetList(array(), array('IBLOCK_ID' => $ar_res["IBLOCK_ID"], "ID" => $ar_res["IBLOCK_SECTION_ID"]), false, array("ID","IBLOCK_ID","UF_*"));
                  if ($arSection = $rsSections->Fetch())
                  {
                        $url = str_replace('#UF_SECTION_URL#', $arSection["UF_SECTION_URL"], $arFields["URL"]);
                  }
              }
            }
        }
    }
    return $url;
}
```

## Типичные ошибки и диагностика
- URL поиска не подставляется → проверить, что `simai.framework` загружен и обработчик зарегистрирован.
- Поле `UF_SECTION_URL` пустое → результат останется без подстановки, нужна проверка данных инфоблока.

## Что должен уметь читатель после
- Найти обработчик `OnSearchGetURL` в снапшотах модуля.
- Понимать логику подстановки `DETAIL_PAGE_URL` и `UF_SECTION_URL`.
- Проверять наличие данных разделов при отладке поиска.

## Источники истины
- `source/modules/simai_framework_*.json`
- `source/sf4-structure.enriched.json`
