Ниже — маленький “скелет” того, как проект обычно опирается на API ядра SF4 (без привязки к внутренностям поставки):

```php
<?php

use SIMAI\Main\Configuration\Property;
use SIMAI\Main\Page\Asset;
use SIMAI\Main\IO\IncludeArea;

// 1) Получить итоговое свойство страницы (собранное на уровне site/section/page/user)
$layout = Property::getValue(SF_SITE_DIR, 'layout_type');

// 2) Подключить системный ассет из реестра SF4
Asset::getInstance()->load('jquery');

// 3) Подключить шаблонную область из {site_dir}/simai.data/template/area/...
IncludeArea::includeTemplateArea('sidebar/right');
```
