# `/bitrix/templates/simai.framework` — универсальный шаблон (layout, header/footer, includes, панели)

Системный шаблон SF4 в Bitrix выполняет роль “точки входа” фреймворка на публичной части: именно он активируется для сайта и обеспечивает базовую связку “Bitrix → SF4”. При этом логика шаблона устроена так, чтобы **не заставлять проект править системные файлы**: системные `header.php`/`footer.php` передают управление в проектный слой `{site_dir}/simai.data`.

В базовой поставке это видно буквально: `header.php` проверяет, что модуль `simai.framework` подключён, и затем подключает `{site_dir}/simai.data/template/template.php` (если файл существует). `footer.php` делает то же самое — за счёт внутренней логики проектный `template.php` различает “входим в header” и “входим в footer”.

Пример (упрощённо, как есть по смыслу):

```php
<?php
if (!\Bitrix\Main\Loader::includeSharewareModule('simai.framework'))
{
    // сообщение об ошибке и остановка
}

if (file_exists(SF_DATA_PATH . "/template/template.php"))
{
    include SF_DATA_PATH . "/template/template.php";
}
```

Главная идея: системный шаблон остаётся стабильным и обновляемым, а весь “реальный сайт” собирается через проектный слой.

# Адаптация под проект: всё, что изменяется, копируется/расширяется в `{site_dir}/simai.data/template`

Проектная адаптация в SF4 строится вокруг **единой точки расширения**: `{site_dir}/simai.data/template/template.php`. Этот файл фактически становится “главным layout-файлом проекта”: он формирует HTML-каркас страницы и подключает остальные части проекта.

Типовой состав проектного шаблона (как минимум по умолчанию) выглядит так:

* `{site_dir}/simai.data/template/template.php` — общий layout и подключение областей  
* `{site_dir}/simai.data/template/property.php` — подключение/подготовка свойств и настроек  
* `{site_dir}/simai.data/template/panel.php` — подключение панели/режимов (что показывать, когда включён режим редактирования)  
* `{site_dir}/simai.data/template/style.php`, `js.php`, `meta.php` — базовые стили/скрипты/мета-теги

Дальше `template.php` не “рисует всё сам”, а подключает **области** через механизм include-area SF4. В базовой схеме используются области вроде `header`, `footer`, `main/top`, `main/bottom`, `sidebar/left`, `sidebar/right`, служебные (`service/top`, `service/bottom`), скриптовые (`script/top`, `script/bottom`) и т.п.

Каждая область реализуется отдельным файлом в `{site_dir}/simai.data/template/area/...`, и внутри области обычно выбирается активное представление (view) по настройке `grid_view_*`. Пример логики области `header`:

```php
<?php
use SIMAI\Main\Configuration\Property;

$tmpView = Property::getValue(SF_SITE_DIR, 'grid_view_header');
$fileTemplate = SF_DATA_PATH . "/grid/view/header/" . $tmpView . "/template.php";

if (file_exists($fileTemplate))
{
    include $fileTemplate;
}
```

Так достигается важный эффект: проект меняет структуру и внешний вид не через правку системного шаблона, а через **переключение представлений областей** и **переопределение блоков/шаблонов** в `simai.data`.

# Ассеты шаблона: системные стили/скрипты и проектные переопределения

Подключение ассетов в SF4 централизовано: проектный шаблон подключает `style.php`/`js.php`, а внутри них SF4-загрузчик подключает пакеты по именам. В базовой сборке `style.php` подгружает набор пакетов через `SIMAI\Main\Page\Asset` (примерно так):

```php
<?php
use SIMAI\Main\Page\Asset;

Asset::getInstance()->load("lazysizes");
Asset::getInstance()->load("jquery");
Asset::getInstance()->load("popper");
Asset::getInstance()->load("simai.framework");
Asset::getInstance()->load("simai.bx-panel");
Asset::getInstance()->load("font-awesome");
Asset::getInstance()->load("fancybox");
Asset::getInstance()->load("swiper");
Asset::getInstance()->load("simai.special");
```

Сами пакеты описываются конфигурацией ассетов как набор “файлы \+ тип (style/script) \+ версия/каталог”. Важно, что в вашем проектном подходе действует правило:

* конфигурация ассетов сайта **замещает**, а не дополняет системную.

Практический смысл этого правила: даже если в ядре SF4 при обновлении изменится состав системных пакетов, проект остаётся стабильным, потому что использует **свою** фиксированную конфигурацию пакетов. Цена этого подхода тоже понятна: проектная конфигурация должна содержать полный набор того, что реально нужно сайту, иначе “лишнего” ничего не подтянется.

Проектные CSS/JS при этом живут в `{site_dir}/simai.data/template` (и/или подключаются через пакеты), то есть снова соблюдается ключевой принцип: “ядро обновляемое — проект отдельно”.

# Опорная карта путей для работы с шаблоном

Чтобы быстро ориентироваться при разработке и диагностике, достаточно держать в голове несколько точек:

* `/bitrix/templates/simai.framework/header.php`, `/bitrix/templates/simai.framework/footer.php` — системные входные файлы Bitrix-шаблона, которые делегируют сборку в проект  
* `{site_dir}/simai.data/template/template.php` — главный layout проекта (точка расширения)  
* `{site_dir}/simai.data/template/style.php`, `js.php`, `meta.php` — базовое подключение ресурсов и мета-информации  
* `{site_dir}/simai.data/template/area/...` — шаблоны областей страницы; внутри них выбираются и подключаются view из `grid/view`  
* `{site_dir}/simai.data/grid/view/...` — представления областей (то, что пользователь выбирает в настройках)  
* `{site_dir}/simai.data/grid/block/...` — блоки, которые фактически рендерят area-шаблоны и выводят контент
