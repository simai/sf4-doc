# Пример 1\. Подключение компонента мастера на странице

```php
<?php
$APPLICATION->IncludeComponent(
    'simai:sf.wizard',
    '.default',
    [
        'WIZARD_DIR' => '/simai/wizard/my_wizard',          // относительно корня сайта
        'WIZARD_CONFIG_FILE' => '/simai/wizard/my_wizard/.wizard.config.php',
        'CACHE_TYPE' => 'N',
        'AJAX_TIME_INTERVAL' => 5,                          // интервал между “порциями” выполнения
    ]
);
```

# Пример 2\. Описание действия в конфиге мастера (общая форма)

```php
[
    'name' => 'Запросить параметры у пользователя',
    'code' => 'data.add.property',
    'data_output_code' => 'setup',
    'prev_disable' => 'Y',
    'parameter' => [
        'file' => 'data/config/.property.config.php',
    ],
]
```

# Пример 3\. Где обычно лежат пакеты данных мастера

```
WIZARD_DIR/
  .wizard.config.php
  data/
    config/
      .option.config.php
      .usergroup.config.php
      .iblocktype.config.php
    iblock/
      ... архивы инфоблоков ...
    component/
      simai.component.zip
    module/
      ... модули ...
    public/
      public.zip
      SITE_ID/
        site.SITE_ID.public.zip
    template/
      template.zip
    php_interface/
      dbconn.add
      init.add
```
