# SIMAI Framework 4

Эта документация предназначена для двух аудиторий:

1) **Разработчики решений на SF4 (Track A)** — сборка страниц через `{site_dir}/simai.data`, грид/блоки/view, готовые Bitrix-компоненты SIMAI, настройки и мастера.
2) **Разработчики ядра SF4 (Track B)** — устройство модулей, классы, внутренние подсистемы, совместимость и обновления.

## Быстрый вход
- Начните с Track A: `tracks/solutions/intro.md` → `tracks/solutions/getting-started.md`
- Для структуры путей: `tracks/solutions/file-model.md`, `reference/sources-of-truth.md`
- Для терминов и путей: `reference/terminology.md`, `reference/project-structure.md`
- Для практики: `tracks/solutions/examples.md`, `tracks/solutions/faq.md`

## Принципы
- Ядро `/simai` и системный шаблон `/bitrix/templates/simai.framework` **не правятся** в проектах. Расширение делается через `{site_dir}/simai.data` и/или отдельные модули.
- Источники истины для каждого раздела зафиксированы в `reference/sources-of-truth.md`.
- Документация без frontmatter (чистый Markdown). Дата сборки архива: 2025-12-16.
