# Schema-конфиги (описание полей) — в `{site_dir}/simai.data/config/` (`.site.config.php`, `.structure.config.php`, `.demo.config.php`; локальный `.structure.config.php` в разделе может переопределять базовый)
# Values (значения):
* **Сайт:** `{site_dir}/simai.data/.site.property.php`  
* **Раздел/страница:** `/.property.php` в директории раздела (`section` и ветка `page` внутри)  
* **Пользователь:** сессионное хранилище через `Property` (storageId `user`)  
# **Роль SIMAI Property:** типы полей, валидаторы, шаблоны ввода/отображения для UI форм

Формат `/.property.php` (упрощённо) выглядит так:

```php
<?php

declare(strict_types=1);

return [
    'section' => [
        'title' => 'Каталог',
        'show_sidebar' => 'Y',
    ],
    'page' => [
        'index.php' => [
            'show_title' => 'Y',
        ],
        'detail.php' => [
            'show_title' => 'N',
        ],
    ],
];
```

А формат `{site_dir}/simai.data/.site.property.php` — плоский:

```php
<?php

declare(strict_types=1);

return [
    'organization_name' => 'Компания',
    'organization_phone' => '+7 (999) 123-45-67',
];
```

Запись этих файлов выполняется через `var_export()` и сохранение `<?php return ...;` (то есть это “настоящий PHP-конфиг”, а не JSON).
