# A) Мини-цепочка установки решения (практический каркас)

```php
return [
    [
        'name'         => 'Соглашение',
        'code'         => 'agreement',
        'autocomplete' => 'N',
        'parameter'    => [
            'path' => Wizard::getLocal(__DIR__) . '/data/agreement.html',
        ],
    ],

    [
        'name'            => 'Выбор сайта',
        'code'            => 'site.choice.install',
        'data_output_code'=> 'site_config',
        'autocomplete'    => 'N',
        // параметры выбора сайта зависят от вашей реализации UI шага
    ],

    [
        'name'            => 'Копирование файлов решения',
        'code'            => 'file.copy',
        'data_input_code' => 'site_config',
        'autocomplete'    => 'Y',
        'parameter'       => [
            // операции copy
        ],
    ],

    [
        'name'            => 'Импорт инфоблоков (сведения)',
        'code'            => 'iblock.import.archive.sveden',
        'data_input_code' => 'site_config',
        'autocomplete'    => 'Y',
        'parameter'       => [
            // structure.zip + content.zip
        ],
    ],

    [
        'name'            => 'Обновление настроек сайта',
        'code'            => 'site.update.sveden',
        'data_input_code' => 'site_config',
        'autocomplete'    => 'Y',
        'parameter'       => [
            // обычно: template, name, и прочие значения под решение
        ],
    ],

    [
        'name'         => 'Правила ЧПУ',
        'code'         => 'prepare.urlrewrite',
        'autocomplete' => 'Y',
    ],
    [
        'name'         => 'Добавление ЧПУ',
        'code'         => 'urlrewrite.add',
        'autocomplete' => 'Y',
        'parameter'    => [
            'source' => Wizard::getLocal(__DIR__) . '/data/urlrewrite/urlrewrite.rules.php',
        ],
    ],
];
```

# B) Мини-цепочка “подготовки пакета обновления” (если вы используете export)

Если у вас есть задача собирать обновления/пакеты, то обычно это:

* `iblock.export.archive` (упаковка инфоблоков),  
* `site.export.data`, `option.export.data`, `usergroup.export.data`, `shortlink.export.data` (служебные данные).

Но для `iblock.export.archive` и части экспортов лучше отдельно зафиксировать контракт параметров (путь куда сохранять, как выбирать инфоблоки). Это как раз тот блок, где я предлагаю “контрактом” закрыть неопределённости одним документом и дальше переиспользовать.
