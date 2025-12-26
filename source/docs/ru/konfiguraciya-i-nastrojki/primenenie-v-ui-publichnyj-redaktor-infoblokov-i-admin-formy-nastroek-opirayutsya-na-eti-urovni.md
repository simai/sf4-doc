В пользовательском интерфейсе это обычно проявляется так:

* **Админ-формы настроек** (уровни site/section/page/demo) берут:

  * schema из `{site_dir}/simai.data/config/*.config.php`  
  * значения из `{site_dir}/simai.data/.site.property.php` и `/.property.php`  
  * и строят поля через универсальные свойства (единый механизм типов/шаблонов)

* **Публичные редакторы** (в зависимости от сценария решения) используют те же источники, но в другом UI: принцип остаётся тем же — schema задаёт “что редактируем”, property-файлы задают “что сохранено”, а `simai.property` обеспечивает “как отрисовать и принять ввод”.

# Пример: точечная запись значения на разных уровнях через `Configuration`

```php
<?php

declare(strict_types=1);

use SIMAI\Main\Configuration\Page;
use SIMAI\Main\Configuration\Section;
use SIMAI\Main\Configuration\Site;
use SIMAI\Main\Configuration\Property;

// 1) Сайт: значение пишется в {site_dir}/simai.data/.site.property.php
Site::setValue(SF_SITE_DIR, 'organization_name', 'SIMAI');

// 2) Раздел: значение пишется в <директория>/.property.php в секцию "section"
Section::setValue('/catalog/', 'title', 'Каталог');

// 3) Страница: значение пишется в <директория>/.property.php в секцию "page" по имени файла
Page::setValue('/catalog/index.php', 'show_title', 'Y');

// 4) Пользователь: значение пишется в сессию (storageId "user")
Property::setValue('user', 'demo_mode', 'Y');
```

Если нужно “снять” пользовательское переопределение, используется `Property::delValue('user', 'demo_mode')` или очистка стораджа `Property::clear('user')`.
