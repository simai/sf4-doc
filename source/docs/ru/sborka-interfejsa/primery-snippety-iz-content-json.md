# Выбрать по одному примеру на секцию (footer/header/home/main/sidebar) и показать код блока и ключевые параметры (type/default/multiple)

Ниже — 5 «паспортов» блоков (по одному на секцию). В каждом примере показано:

* **код блока** (он же имя папки блока в `{site_dir}/simai.data/grid/block/...`)  
* **несколько ключевых параметров** в том виде, как они объявлены в `.parameters.php`  
* где уместно — пример того, как реализуется **“множественность”** не через `MULTIPLE`, а через паттерн `*_FILTER_COUNT` \+ `*_CODE_i`/`*_VALUE_i`.

Примечание по ключам: во всех примерах имя набора параметров начинается с `$nameTemplate = strtoupper(basename(__DIR__))`, то есть код папки блока берётся как есть и переводится в верхний регистр.

## Header: `display.search.icon`

Папка блока: `{site_dir}/simai.data/grid/block/header/display.search.icon/`

Ключевые параметры:

```php
// display.search.icon — ключевые параметры
return [
    $nameTemplate . "__ICON_MODIFIER" => [
        "TYPE"    => "STRING",
        "DEFAULT" => "fal fa-search mr-2 c-primary",
    ],
    $nameTemplate . "__LINK_MODIFIER" => [
        "TYPE"    => "STRING",
        "DEFAULT" => "c-text-primary sf-link",
    ],
];
```

Как читать: блок — это «иконка поиска/ссылка», а параметры — чисто про CSS-классы (модификаторы). Это хороший пример для новичка: быстро видно, что “настройки блока” часто сводятся к модификаторам и классам.

---

## Footer: `button`

Папка блока: `{site_dir}/simai.data/grid/block/footer/button/`

Ключевые параметры:

```php
// button — ключевые параметры
return [
    $nameTemplate . "_MODIFIER" => [
        "TYPE"    => "STRING",
        "DEFAULT" => "",
    ],
    $nameTemplate . "__NAME" => [
        "TYPE"    => "STRING",
        "DEFAULT" => "",
    ],
    $nameTemplate . "__LINK" => [
        "TYPE"    => "STRING",
        "DEFAULT" => "",
    ],
];
```

Что важно заметить: у этого блока встречается ключ **`_MODIFIER`** (с одним подчёркиванием), а остальные параметры — через `__`. Это не ломает работу, но в документации стоит отдельно отметить как «особенность конкретного блока», чтобы у разработчика не было ожидания, что *везде* строго `__`.

## Sidebar: `menu.sidebar`

Папка блока: `{site_dir}/simai.data/grid/block/sidebar/menu.sidebar/`

Ключевые параметры:

```php
// menu.sidebar — ключевые параметры
$params = [
    $nameTemplate . "__ACTIVE_ITEM_TEXT_COLOR" => [
        "TYPE"    => "COLORPICKER",
        "DEFAULT" => "",
    ],
    $nameTemplate . "__ACTIVE_ITEM_BACKGROUND_COLOR" => [
        "TYPE"    => "COLORPICKER",
        "DEFAULT" => "",
    ],
];

return $params;
```

Как читать: блок меню может иметь «визуальные» параметры, которые управляются не строкой классов, а специализированным типом (`COLORPICKER`). Это хороший пример того, что параметры блока — это не только “строки”, но и типизированные контроли.

## Home: `news.card`

Папка блока: `{site_dir}/simai.data/grid/block/home/news.card/`

Ключевые параметры (минимальный набор, который показывает разные типы):

```php
// news.card — ключевые параметры (фрагменты)
$nameTemplate . "__SECTION_CODE" => [
    "TYPE"        => "STRING",
    "DEFAULT"     => "",
    "EXPERT_MODE" => "Y",
],

$nameTemplate . "__ELEMENT_QUANTITY" => [
    "TYPE"    => "STRING",
    "DEFAULT" => "8",
],

$nameTemplate . "__COL_COUNT_XL" => [
    "TYPE"        => "LIST",
    "VALUES"      => $arColumn,
    "DEFAULT"     => "4",
    "EXPERT_MODE" => "Y",
],

$nameTemplate . "__USE_FILTER" => [
    "TYPE"        => "CHECKBOX",
    "DEFAULT"     => "Y",
    "EXPERT_MODE" => "Y",
    "REFRESH"     => "Y",
],
```

Что этот пример даёт для документации:

* `LIST` показывает, что у параметра бывает список допустимых значений (`VALUES`).  
* `CHECKBOX` показывает, что блок может включать/выключать функциональность (фильтрацию) и требовать `REFRESH => Y` для перерисовки формы настройки.  
* `EXPERT_MODE => Y` удобно использовать как маркер “расширенных” параметров в UI.

## Main: `banner.single`

Папка блока: `{site_dir}/simai.data/grid/block/main/banner.single/`

Ключевые параметры (и главное — демонстрация «множественности»):

```php
// banner.single — базовый параметр секции/источника
$nameTemplate . "__SECTION_CODE" => [
    "TYPE"        => "STRING",
    "DEFAULT"     => "section-top",
    "EXPERT_MODE" => "Y",
],
```

Множественные параметры реализованы через **счётчик \+ набор параметров по индексу**:

```php
// banner.single — множественные фильтры через COUNT + CODE_i/VALUE_i
$params[$nameTemplate . "_FILTER_COUNT"] = [
    "TYPE"    => "LIST",
    "VALUES"  => [1 => 1, 2 => 2, 3 => 3, 4 => 4],
    "DEFAULT" => "1",
    "REFRESH" => "Y",
];

for ($i = 0; $i < $arCurrentValues[$tmpCode . "_FILTER_COUNT"]; $i++) {
    $params[$nameTemplate . "_CODE_" . $i] = [
        "TYPE"        => "STRING",
        "DEFAULT"     => "PROPERTY_MAIN",
        "EXPERT_MODE" => "Y",
    ];
    $params[$nameTemplate . "_VALUE_" . $i] = [
        "TYPE"        => "STRING",
        "DEFAULT"     => "false",
        "EXPERT_MODE" => "Y",
    ];
}
```

Это и есть практический эквивалент “multiple”, даже если явного `MULTIPLE => Y` нет: пользователь в настройках увеличивает `*_FILTER_COUNT`, и UI показывает дополнительные пары `CODE_i/VALUE_i`.

# При отсутствии registry использовать `content.json` как источник параметров

На практике «пустые» или почти пустые `.parameters.php` встречаются: блок может существовать и корректно рендериться, но не иметь параметров (или параметры временно закомментированы). Тогда рабочая стратегия для документации такая:

* если `.parameters.php` **есть и возвращает массив** — описывать параметры по нему (это самый точный источник);  
* если `.parameters.php` **пустой/закомментирован** — в документации фиксировать “параметров нет (или не используются)”, а назначение блока описывать по поведению `template.php` и метаданным из `.description.php`;  
* если блока нет параметров, но он управляется внешними настройками (например, через area-параметры во view) — описывать именно эти area-параметры.

# Цитаты брать через `content.json` (или прямые JSON-фрагменты) для точности; указывать путь/код блока

Чтобы в документации не возникали “примерные” описания (которые потом расходятся с реальностью), хороший регламент для примеров такой:

* указывать **код блока** и **папку** в `{site_dir}/simai.data/grid/block/<section>/<code>/`;  
* параметры приводить в формате “ключ → TYPE/DEFAULT (+ при наличии: VALUES/REFRESH/EXPERT\_MODE)”;  
* если есть динамические группы параметров (`*_FILTER_COUNT`, `*_CODE_i`, `*_VALUE_i`) — обязательно показывать этот паттерн, потому что он объясняет, **как именно масштабируются настройки**.

При этом в тексте документации лучше показывать не «сырой JSON», а уже приведённый к читабельному виду фрагмент (как в примерах выше).

# Если `content.json` / `grid.md` недоступны, использовать актуальные источники истины

Если реестр/учебные материалы недоступны или “не под рукой”, то для восстановления истины по блоку достаточно фактических артефактов проекта:

1. `{site_dir}/simai.data/grid/block/<...>/<code>/.parameters.php` — какие параметры вообще существуют и каких типов они бывают.  
2. `{site_dir}/simai.data/grid/block/<...>/<code>/template.php` — что блок реально рендерит и от чего зависит.  
3. `{site_dir}/simai.data/grid/view/<...>/template.php` — как блок подключён в конкретном представлении (и какие area-параметры ему прокидываются).
