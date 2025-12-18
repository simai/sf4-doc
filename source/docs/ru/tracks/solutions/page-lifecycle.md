# Жизненный цикл страницы (SF4)

## Назначение
Описание последовательности построения страницы SF4: выбор шаблона, загрузка ассетов, чтение конфигов, сборка грида и кэширование.

## Где применяется
Системный шаблон `/bitrix/templates/simai.framework`, слой сайта `{site_dir}/simai.data` (config/template/grid), компонент `simai:sf.grid`.

## Где находится
- Иерархия настроек и ментальная модель: `source/file-functional.md`.
- Узлы шаблона и данных сайта: `source/sf4-structure.enriched.json`.
- Реестры грида/view/block: `source/sf_grid.json`, `source/view.json`, `source/block.json`.

## Требования
- Активный шаблон `/bitrix/templates/simai.framework`.
- Наличие конфигов `{site_dir}/simai.data/config/.asset.config.php` и `.font.config.php`.
- Модули `simai.framework` и `simai.property*` доступны.

## Как это работает
1. Bitrix выбирает активный шаблон (`/bitrix/templates/simai.framework`), который подключает ассеты ядра `/simai` и overrides из `{site_dir}/simai.data/template`.
2. Читаются конфиги уровней: сайт → раздел → страница → пользователь (описано в `file-functional.md`).
3. Компонент `simai:sf.grid` (реестр в `structure.json`) собирает страницу: выбирает view из `{site_dir}/simai.data/grid/view`, подключает блоки из `{site_dir}/simai.data/grid/block`.
4. Результат кэшируется в соответствии с настройками компонентов/Bitrix.

## Настройка и параметры
| Узел/файл | Назначение | Источник |
| --- | --- | --- |
| `/bitrix/templates/simai.framework` | Системный шаблон, подключает ассеты | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/config/.asset.config.php` | Ассеты сайта | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/config/.font.config.php` | Шрифты сайта | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/grid/view` | Пресеты view для грида | `source/sf4-structure.enriched.json` |
| `{site_dir}/simai.data/grid/block` | Шаблоны блоков | `source/sf4-structure.enriched.json` |

## Примеры из репозитория
Источник: `source/file-functional.md`
```md
2. **Иерархия уровней настроек**: сайт → раздел → страница → пользователь. 
3. **Шина данных (массив)**: единый массив, через который “едут” входные данные и настройки к блокам/шаблонам. 
4. **Гриды + блоки + view**: системные компоненты на базе SF4, которые связывают “что показывать” (block) и “как раскладывать” (view, left/right и т.п.).  
5. **Шаблон сайта** (Bitrix template): системный шаблон `/bitrix/templates/` → `simai.framework` (шаблон SF4) — финальная сборка страницы. 
```

## Типичные ошибки и диагностика
- Не выбран системный шаблон → включить `/bitrix/templates/simai.framework`.
- Отсутствует view или блок в `simai.data/grid` → создать/скопировать нужные шаблоны.
- Конфиги ассетов/шрифтов отсутствуют → проверить наличие файлов в `{site_dir}/simai.data/config`.
- Кэш не сброшен после правок → очистить кэш Bitrix/компонентов.

## Что должен уметь читатель после
- Понимать порядок чтения конфигов и сборки страницы.
- Проверять наличие view/block и конфигов ассетов/шрифтов.
- Диагностировать проблемы, связанные с шаблоном и кэшем.

## Источники истины
- `source/file-functional.md`
- `source/sf4-structure.enriched.json`
- `source/structure.json`
