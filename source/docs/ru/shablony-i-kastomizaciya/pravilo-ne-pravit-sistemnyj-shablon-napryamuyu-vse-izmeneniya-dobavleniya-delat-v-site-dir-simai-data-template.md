Базовое правило безопасной кастомизации SF4:

* системный шаблон `simai.framework` **не редактируем**;  
* вся проектная логика и внешний вид — в `{site_dir}/simai.data/template/…`.

Типовой набор проектных файлов (минимум, который часто встречается в проектах SF4):

* `{site_dir}/simai.data/template/template.php` — основной layout и подключение областей  
* `{site_dir}/simai.data/template/property.php` — подготовка/подключение свойств и настроек  
* `{site_dir}/simai.data/template/panel.php` — панели/режимы (в т.ч. режимы редактирования)  
* `{site_dir}/simai.data/template/style.php`, `js.php`, `meta.php` — подключение ресурсов и мета-информации
