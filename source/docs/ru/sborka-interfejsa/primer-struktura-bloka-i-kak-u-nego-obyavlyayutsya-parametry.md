Ниже — показательный пример “проектного” блока `custom.button` (размещается как папка блока и подключается из view по коду).

# `template.php` — вывод блока

```php
<?
if (!defined("B_PROLOG_INCLUDED") || B_PROLOG_INCLUDED !== true) {
    die();
}

$nameTemplate = strtoupper(basename(__DIR__));
?>

<a class="<?= $arBlockProperty[$nameTemplate . "__BUTTON_MODIFIER"] ?>"
   href="<?= $arBlockProperty[$nameTemplate . "__BUTTON_LINK"] ?>"
   target="<?= $arBlockProperty[$nameTemplate . "__BUTTON_TARGET__BLANK"] == "Y" ? "_blank" : "_self" ?>">
    <?= $arBlockProperty[$nameTemplate . "__BUTTON_TEXT"] ?>
</a>
```

Здесь важны две вещи:

1. Блок читает параметры из `$arBlockProperty[...]`.  
2. Ключи параметров формируются как `<КОД_БЛОКА>__<ИМЯ_ПАРАМЕТРА>`, где “код блока” берётся из имени папки (например, `CUSTOM.BUTTON`).

# `.parameters.php` — объявление параметров блока (то, что увидит редактор/грид)

```php
<?
use Bitrix\Main\Localization\Loc;

Loc::loadMessages(__FILE__);

$nameTemplate = strtoupper(basename(__DIR__));

return [
    $nameTemplate . "__BUTTON_LINK" => [
        "NAME" => Loc::getMessage("SF_GRID__" . $nameTemplate . "__BUTTON_LINK"),
        "TYPE" => "STRING",
        "DEFAULT" => "https://simai.studio",
    ],
    $nameTemplate . "__BUTTON_TEXT" => [
        "NAME" => Loc::getMessage("SF_GRID__" . $nameTemplate . "__BUTTON_TEXT"),
        "TYPE" => "STRING",
        "DEFAULT" => "simai.studio",
    ],
    $nameTemplate . "__BUTTON_TARGET__BLANK" => [
        "NAME" => Loc::getMessage("SF_GRID__" . $nameTemplate . "__BUTTON_TARGET__BLANK"),
        "TYPE" => "CHECKBOX",
        "DEFAULT" => "Y",
    ],
    $nameTemplate . "__BUTTON_MODIFIER" => [
        "NAME" => Loc::getMessage("SF_GRID__" . $nameTemplate . "__BUTTON_MODIFIER"),
        "TYPE" => "STRING",
        "DEFAULT" => "btn btn-primary",
    ],
];
```

# Как эти параметры “попадают” из view в блок

Грид читает `.parameters.php` блока, а затем забирает значения из параметров view. При этом для совместимости с именованием параметров Bitrix **в view точки заменяются на подчёркивания**:

* ключ блока: `CUSTOM.BUTTON__BUTTON_TEXT`  
* в view он хранится как: `...__CUSTOM_BUTTON__BUTTON_TEXT`

Это полезно явно прописать в документации как правило именования параметров area.
