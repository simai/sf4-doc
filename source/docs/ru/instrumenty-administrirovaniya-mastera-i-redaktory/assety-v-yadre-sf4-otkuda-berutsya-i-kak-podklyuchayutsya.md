В SIMAI Framework 4 (SF4) есть отдельный “реестр ассетов” на стороне ядра: он хранится в системном конфиге `/simai/config/.asset.config.php`, а сами файлы ассетов ожидаются в системном каталоге ассетов `/simai/asset`. Подключение выполняется через класс `SIMAI\Main\Page\Asset`, который уже внутри добавляет CSS/JS/строки в стандартный менеджер ассетов 1С-Битрикс (`\Bitrix\Main\Page\Asset::getInstance()`).

Ключевая логика подключения устроена так:

* ассет подключается по **имени** (`load($name, $version = 'default')`);

* конфиг описывает:

  * базовую папку группы (поле `dir`),  
  * версии/варианты (внутри `asset[$version]`),  
  * набор файлов (внутри `file[]`) и их тип (`style`, `script` или `string`);

* при подключении `style/script` SF4 проверяет опцию Bitrix `main/use_minified_assets`: если она включена и рядом есть `.min.css` / `.min.js`, будет подключён минифицированный файл, иначе — обычный.

Важно для вашей практики: **проектный конфиг `{site_dir}/simai.data/config/.asset.config.php` у вас не используется вообще**, поэтому “правильный” проектный способ добавлять CSS/JS — через слой шаблона в `{site_dir}/simai.data/template/`. Это также видно по тому, как устроен ваш проектный `template.php`: перед выводом head он делает `include "style.php"; include "js.php";`, а уже затем вызывает `$APPLICATION->ShowHead();`. То есть именно `style.php/js.php` — ваша штатная точка, куда можно положить проектные `addCss/addJs` и/или `Asset::load(...)`, не затрагивая системные файлы.

Ниже — минимальный пример подключения реестровых ассетов через API SF4 (это именно “ядровой” способ, когда ассет описан в `/simai/config/.asset.config.php`):

```php
<?php

use SIMAI\Main\Page\Asset;

Asset::getInstance()->load('jquery');
Asset::getInstance()->load('simai-framework');
Asset::getInstance()->load('font-awesome');
```

И “схема” того, какую структуру ожидает реестр (упрощённо, как контракт для `Asset::load`):

```php
<?php

return [
    'simai-framework' => [
        'dir' => '/simai-framework',
        'asset' => [
            'default' => [
                'dir' => '/default',
                'file' => [
                    ['type' => 'style',  'path' => '/css/app.css'],
                    ['type' => 'script', 'path' => '/js/app.js'],
                    ['type' => 'string', 'path' => '<meta name="foo" content="bar">'],
                ],
            ],
        ],
    ],
];
```

Отдельно в ядре есть реестр шрифтов через `SIMAI\Main\Page\Font`: он читает `/simai/config/.font.config.php` и добавляет `<link ...>` как “строку” (`addString`), а также умеет выдавать `font-family` по коду шрифта. Это полезно, когда типографика сайта завязана на свойства (например, `body_font`) и должна настраиваться централизованно.
