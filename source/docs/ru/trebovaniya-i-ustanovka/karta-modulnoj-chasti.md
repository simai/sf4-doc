# Ядро `/simai` (в составе модуля)

`/simai` — это системная часть SIMAI Framework 4, которая **устанавливается модулем `simai.framework`** в корень сайта и используется как “платформенное ядро”: здесь лежат базовые конфиги, системные ассеты и инфраструктура мастеров/редакторов. В проектной разработке это важно воспринимать как “прошивку платформы”: **в проектах не правится**, чтобы обновления SF4 не превращались в ручное слияние изменений.

Как это выглядит в установке на практике:

* при установке модуля содержимое **`/bitrix/modules/simai.framework/install/simai`** копируется в **`/simai`**;  
* при удалении модуля системная папка **`/simai`** удаляется целиком.

Внутри `/simai` есть несколько “опорных зон”, которые встречаются в типовых сценариях:

* **`/simai/config`** — базовые конфиги платформы (включая системные варианты `.asset.config.php`, `.font.config.php`, `.framework.config.php`);  
* **`/simai/asset`** — системные библиотеки и ресурсы SF4 (используются и публичной частью, и панелью/редакторами);  
* **`/simai/wizard/action`** — библиотека “действий” мастера (шаги установки/импорта/настройки).

Граница ответственности простая: всё, что относится к конкретному сайту/решению, должно жить в `{site_dir}/simai.data`, а `/simai` остаётся чистым “ядром платформы”.

# Компоненты `/bitrix/components/simai`

Компоненты SF4 ставятся в `/bitrix/components/simai` при установке модуля и подключаются стандартным образом Bitrix:

* имя компонента в вызове строится как `simai:<код_папки>`,  
* где `<код_папки>` — имя директории компонента внутри `/bitrix/components/simai`.

Например, папка `sf.grid` подключается как:

```php
<?php
$APPLICATION->IncludeComponent("simai:sf.grid", ".default", ["VIEW" => "home_main"]);
```

В поставке модуля присутствует набор компонентов, который закрывает как “строительную” часть (грид/блоки/представления), так и прикладные задачи (инфоблоки, меню, формы, утилиты). В установленной структуре компоненты сгруппированы довольно логично — по назначению:

**Грид и блоки (сборка страницы и редакторы блоков)**

* `sf.grid`  
* `sf.block`  
* `sf.block.view`  
* `sf.block.edit`  
* `sf.block.property`  
* `sf.block.row.property`  
* `sf.block.col.property`

**Инфоблоки (типовые варианты вывода)**

* `sf.iblock.list`  
* `sf.iblock.detail`  
* `sf.iblock.section`  
* `sf.iblock.table`  
* `sf.iblock.filter`  
* `sf.iblock.calendar`

**HL и специализированные выводы**

* `sf.highloadblock.grid`

**Мастер (установка/сценарии)**

* `sf.wizard`  
* `sf.wizard.stage`

**Меню и навигация**

* `sf.menu`  
* `sf.menu.sections`  
* `menu.list`  
* `sf.breadcrumb`  
* `pagenavigation`

**Feedback / сообщения**

* `sf.feedback`  
* `sf.feedback.appeal`  
* `sf.feedback.vote`  
* `feedback.error`  
* `sf.message`

**Утилитарные / контентные**

* `sf.template.include`  
* `sf.cookie.notification`  
* `sf.share`  
* `sf.rss.show`  
* `sf.pdf.viewer`  
* `sf.weather`  
* `sf.swiper.nav`  
* `sf.up`  
* `sf.banner.main`  
* `sf.promo`  
* `sf.section.main.map`  
* `sf.user.list`  
* `sf.photo.add`  
* `sf.video.add`  
* `property.news.calendar`  
* `info.help`  
* `main.ui.grid`  
* `main.ui.filter`  
* `sf.property.edit`

Практический смысл для разработчика решения: “каркас” страницы обычно собирает `sf.grid`, а дальше нужные куски контента выводятся блоками и/или компонентами внутри блоков.

Отдельно полезно отметить `simai:sf.wizard`: он используется как “движок” установщика решения. В вашем примере установочный `install/index.php` загружает пакеты ассетов через `SIMAI\Main\Page\Asset` и затем запускает мастер через `simai:sf.wizard`, передавая ему путь к конфигу мастера (`.wizard.config.php`) и параметры AJAX-исполнения.

# Действия мастера `/simai/wizard/action`

`/simai/wizard/action` — библиотека шагов мастера: каждый шаг реализован отдельной папкой-действием. У каждого действия обычно есть минимум:

* `.description.php` — метаданные (NAME/DESCRIPTION/SORT/VERSION) для отображения в интерфейсе мастера;  
* `action.php` — код выполнения шага;  
* `lang/...` — локализация сообщений.

Мастер решения задаёт цепочку шагов в `.wizard.config.php`: там перечисляются действия в нужном порядке, с условиями и параметрами. В вашей конфигурации действия описываются как элементы массива `action`, где важные поля обычно такие:

* `code` — код действия (имя папки в `/simai/wizard/action`);  
* `data_input_code` / `data_output_code` — входные/выходные данные шага (обмен между шагами);  
* `condition` — условия выполнения (например, по значениям выбранных параметров);  
* `parameter` — “прокидывание” параметров (например, выбранный сайт, пути, файлы конфигов).

Примерно так мастер связывает “интерфейсный выбор” пользователя и фактическое исполнение шагов.

В поставке платформы есть действия, которые покрывают типовой жизненный цикл установки/миграций:

**Файлы и каталоги**

* `file.copy`, `file.create`, `file.delete`, `file.rename`, `file.add`  
* `file.unzip`, `file.zip`  
* `dir.make`, `dir.choice`  
* а также служебные вроде `file.encode.win1251`

**Инфоблоки и конфиги**

* `iblock.import.archive`, `iblock.export.archive`  
* `iblock.translate`  
* `iblocktype.import.data` / `iblocktype.export.data`  
* `iblocksection.import.data`  
* `iblockconfig.import.data`

**Сайт и настройки**

* `site.choice`, `site.create`, `site.update`  
* `site.import.data`, `site.export.data`  
* `option.import.data`, `option.export.data`  
* `usergroup.import.data`, `usergroup.export.data`

**Переводы/служебные**

* `translate.check`, `site.translate`  
* `urlrewrite.add`, `prepare.urlrewrite`  
* `redirect`, `replace.code`, `restore.names`, `cut.names`  
* `shortlink.import.data`, `shortlink.export.data`  
* `install.check`, `language.choice`, `info`, `agreement`

Отдельная деталь, полезная для backend-описания: действия мастера работают со “состоянием мастера” и сохраняют результаты шагов в хранилище через конфигурационные классы SF4. Например, в действиях встречается сохранение массива результата мастера через `SIMAI\Main\Configuration\Property::setArray(...)` — это и есть механизм “пронести данные через цепочку шагов”.

# Классы/утилиты модуля: Configuration/Setting/Iblock/Page/Utility/IO/Block/Search и др.

В `simai.framework` есть прикладной PHP-слой (API), который используют и компоненты, и мастер, и админ-инструменты. По структуре модуля хорошо выделяются несколько пакетов в `lib/`, которые задают “скелет” backend-части SF4:

* `SIMAI\Main\Block\...` — логика, связанная с блоками/разделами/структурами представлений;  
* `SIMAI\Main\Configuration\...` — работа с конфигурациями и уровнями настроек (site/section/page), а также хранение/перенос данных конфигураций;  
* `SIMAI\Main\Page\...` — то, что относится к сборке страницы и ресурсам;  
* `SIMAI\Main\IO\...` — ввод/вывод и низкоуровневые операции с настройками;  
* `SIMAI\Main\Search\...` — поиск/индексация (в контексте платформенных задач);  
* `SIMAI\Main\Utility\...` — вспомогательные утилиты;  
* плюс `SIMAI\Install\...` (импорт/экспорт установочных данных) и `SIMAI\Wizard` (утилиты мастера).

Три класса, которые уже хорошо видны в реальных сценариях установки и настройки (и их обычно стоит упоминать в документации backend-уровня):

1. **`SIMAI\Main\Page\Asset`** — централизованный загрузчик ассетов/пакетов. Используется прямо в установщике решения:

```php
use SIMAI\Main\Page\Asset;

Asset::getInstance()->load("jquery");
Asset::getInstance()->load("simai.framework");
Asset::getInstance()->load("swiper");
```

   Это важная часть архитектуры: SF4 подключает ассеты через единый механизм, а проектная конфигурация может задавать свой состав пакетов.

2. **`SIMAI\Wizard`** — утилиты мастера (в т.ч. корректные пути и вспомогательные операции). В установщике типовой паттерн — получить “локальный путь” мастера:

```php
use SIMAI\Wizard;

$dirWizard = Wizard::getLocal(__DIR__);
```

3. **`SIMAI\Main\Block\Section`** — утилиты, которые помогают работать со структурами блоков/представлений, включая получение списков с превью. Например, список представлений для настройки `grid_view_*` формируется через:

```php
'values' => \SIMAI\Main\Block\Section::getImageList(SF_DATA_DIR . "/grid/view/header"),
```

   Это как раз объясняет, почему в интерфейсе настроек можно показывать варианты “плиткой с картинкой” — список берётся из структуры каталогов view и их превью.
