`.framework.config.php` — это базовый конфиг уровня **ядра SF4**, который хранится в каталоге фреймворка и читается классом `SIMAI\Main\Configuration\Framework`.

Фактический путь к файлу задаётся константой:

* `SF_DIR = "/simai"`  
* `SF_PATH = $_SERVER["DOCUMENT_ROOT"] . SF_DIR`  
* `Framework::CONFIGURATION_FRAMEWORK_FILE_PATH = SF_PATH . "/config/.framework.config.php"`

То есть в рабочем проекте чтение/запись идёт именно в:

* `/simai/config/.framework.config.php`

# Структура файла

Файл возвращает ассоциативный массив, где **каждый параметр** хранится как:

* `value` — значение параметра (скаляр / массив / bool)  
* `readonly` — признак “только чтение” (запрещает изменение через обычные методы записи)

Концептуально структура выглядит так:

```php
<?php

return [
    'some_key' => [
        'value' => '...',
        'readonly' => false,
    ],
];
```

# Ключи базовой поставки

В базовой поставке в `.framework.config.php` есть две смысловые группы параметров.

## SMTP-параметры

Эти ключи предназначены для настройки отправки почты (значения по умолчанию именно такие, как в базовой поставке):

* `smtp_status` → `N` (readonly: `false`)  
* `smtp_encoding` → `utf-8` (readonly: `false`)  
* `smtp_debug` → массив вида `['01' => 'Y']` (readonly: `false`)  
* `smtp_secure` → `ssl` (readonly: `false`)  
* `smtp_port` → `465` (readonly: `false`)  
* `smtp_host` → `smtp.yandex.ru` (readonly: `false`)  
* `smtp_login` → пустая строка (readonly: `false`)  
* `smtp_pass` → пустая строка (readonly: `false`)

## Ссылки на “проектные” конфиги/данные

Это ключи, которые содержат пути/флаги, и в базовой поставке помечены как `readonly = true`:

* `site_nav_config` → `'/ru/simai.data/config/.nav.config.php'` (readonly: `true`)  
* `site_update` → `false` (readonly: `true`)  
* `site_property` → `'/ru/simai.data/config/.site.property.php'` (readonly: `true`)

Важно: значения здесь — именно **строки путей**, которые затем используются другими частями системы как “указатели” на проектные конфиги и property-хранилища.

# Как работает `readonly` и почему это важно

Класс `SIMAI\Main\Configuration\Framework` обеспечивает несколько способов записи, и они по-разному относятся к `readonly`:

* `add($name, $value)` — **не перезапишет** параметр, если он уже существует и `readonly = true`  
* `delete($name)` — **не удалит** параметр, если он `readonly = true`  
* `addReadonly($name, $value)` — принудительно установит значение и выставит `readonly = true`  
* `saveConfiguration()` — сохраняет текущее состояние в файл

Из этого следует практическое правило:

* если параметр помечен как `readonly`, обычный `setValue()` (внутри вызывает `add()`) **не изменит** его, и это ожидаемое поведение, а не ошибка.

# API `Configuration\Framework`: чтение и запись

У класса есть удобные статические методы-обёртки:

* `Framework::getValue($name)` → возвращает `value` или `null`  
* `Framework::setValue($name, $value)` → вызывает `add()` и затем `saveConfiguration()`

## Пример: чтение и запись через `Framework::getValue/setValue`

```php
<?php

declare(strict_types=1);

use SIMAI\Main\Configuration\Framework;

// Чтение
$smtpHost = Framework::getValue('smtp_host');
$smtpPort = Framework::getValue('smtp_port');

// Запись (сохранится только если ключ не readonly)
Framework::setValue('smtp_host', 'smtp.example.com');
Framework::setValue('smtp_port', '587');
Framework::setValue('smtp_secure', 'tls');
```

## Пример: попытка изменить readonly-ключ (не сработает)

```php
<?php

declare(strict_types=1);

use SIMAI\Main\Configuration\Framework;

// В базовой поставке site_nav_config readonly=true,
// поэтому setValue() его не перезапишет.
Framework::setValue('site_nav_config', '/ru/simai.data/config/.nav.config.custom.php');

// Проверка: вернётся старое значение из конфига
$navConfig = Framework::getValue('site_nav_config');
```

## Пример: принудительно задать readonly-значение (через instance API)

Если вам действительно нужно создать/зафиксировать ключ как `readonly`, это делается через `addReadonly()` у экземпляра:

```php
<?php

declare(strict_types=1);

use SIMAI\Main\Configuration\Framework;

$cfg = Framework::getInstance();
$cfg->addReadonly('site_update', true);
$cfg->saveConfiguration();
```

# Особенности сохранения файла

Сохранение выполняется через:

* `var_export($data, true)`  
* `file_put_contents($path, "<?php\nreturn " . $data . ";\n")`

Перед записью предпринимается попытка сделать файл доступным для записи (`chmod 0644`), если `is_writable($path)` возвращает `false`. Поэтому в реальных окружениях важно, чтобы:

* файл `/simai/config/.framework.config.php` существовал и был доступен на запись пользователю веб\-сервера (или чтобы права/владелец позволяли изменить режим).
