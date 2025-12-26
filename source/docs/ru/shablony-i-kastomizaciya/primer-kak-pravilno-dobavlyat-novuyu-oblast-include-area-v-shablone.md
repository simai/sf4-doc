В SF4 “области” подключаются из проектного `template.php` вызовом:

```php
<?IncludeArea::includeTemplateArea("sidebar/left");?>
```

Код области в вызове (`"sidebar/left"`) напрямую задаёт путь к файлу шаблона области в `simai.data`:

* общий вид: `{site_dir}/simai.data/template/area/<area_code>/template.php`  
* пример, который вы привели: `/ru/simai.data/template/area/sidebar/right/template.php`

То есть, чтобы добавить новую область:

1. В `{site_dir}/simai.data/template/area/` создаёте папку области (можно вложенную, со слешами в коде: `sidebar/right`, `service/top`, `main/top` и т.п.).  
2. Внутри создаёте `template.php` — это и есть реализация области.  
3. В `{site_dir}/simai.data/template/template.php` добавляете вызов `IncludeArea::includeTemplateArea("<area_code>");` в нужное место layout’а.
