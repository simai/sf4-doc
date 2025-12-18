# Интеграции с Bitrix

## Назначение
Собирает подтверждённые точки интеграции SF4 с Bitrix: правила ЧПУ, меню, поиск. Использует только найденные узлы и код из локальных источников.

## Где применяется
Wizard actions для urlrewrite, компоненты меню, обработчик поиска в модуле `simai.framework`.

## Где находится
- Actions `urlrewrite.add` и `prepare.urlrewrite`: `source/sf4-structure.enriched.json`.
- Компоненты меню: узлы `/bitrix/components/simai` в `source/sf4-structure.enriched.json`.
- Обработчик поиска `SIMAI\Main\Search\Iblock::OnSearchGetURL`: `source/modules/simai_framework_*.json`.

## Требования
- Доступ к wizard actions из `/simai/wizard/action`.
- Правильная структура меню/инфоблоков и include-областей.
- Зарегистрированный обработчик поиска (модуль `simai.framework`).

## Как это работает
1. Правила ЧПУ можно добавлять через actions `urlrewrite.add`/`prepare.urlrewrite` (wizard).
2. Меню строится компонентами `sf.menu.list`, `sf.menu.sections`, `menu.list`, `breadcrumb`.
3. Поиск: обработчик `OnSearchGetURL` корректирует URL результатов для инфоблоков.

## Настройка и параметры
| Интеграция | Что использовать | Источник |
| --- | --- | --- |
| Правила ЧПУ | Actions `urlrewrite.add`, `prepare.urlrewrite` | `source/sf4-structure.enriched.json` |
| Меню | Компоненты `sf.menu.list`, `sf.menu.sections`, `menu.list`, `breadcrumb` | `source/sf4-structure.enriched.json` |
| Поиск | Обработчик `SIMAI\Main\Search\Iblock::OnSearchGetURL` | `source/modules/simai_framework_*.json` |

## Примеры из репозитория
Источник: `source/sf4-structure.enriched.json`
```json
{
  "id": "action:urlrewrite.add",
  "kind": "action",
  "code": "urlrewrite.add",
  "title": "Добавление правил ЧПУ",
  "description": "Добавляет правила ЧПУ."
}
```

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
- 404 в меню/поиске → проверить ЧПУ (actions urlrewrite.*), права инфоблоков, очистить кэш.
- Обработчик поиска не срабатывает → убедиться в регистрации модуля `simai.framework`.

## Что должен уметь читатель после
- Применять actions urlrewrite.* для правил ЧПУ.
- Настраивать меню через компоненты SIMAI.
- Проверять работу поиска и обработчика `OnSearchGetURL`.

## Источники истины
- `source/sf4-structure.enriched.json`
- `source/modules/simai_framework_*.json`
- `source/structure.json`
