# Docara Documentation Site - AI Agent Instructions

This is a **Docara** documentation site built on **Jigsaw** (Laravel-based static site generator). Docara extends Jigsaw with multilingual documentation support, custom markdown tags, automated builds, and a UI component framework.

## Architecture & Key Concepts

**Build System**: Hybrid PHP + Node.js
- **Backend**: Jigsaw static site generator (PHP 8.2+)
- **Frontend**: Laravel Mix + custom `laravel-mix-docara` plugin
- **Assets**: SCSS (with custom SF design tokens) + vanilla JS (Fuse.js search, Turbo Drive)

**Content Structure**:
- `source/docs/{locale}/` - markdown documentation organized by section
- Each section has `.settings.php` (menu config, title, order) and `.lang.php` (translations)
- `source/_core/` - immutable core from `simai/docara` package (layouts, assets, components)
- `source/Helpers/CustomTags/` - custom CommonMark tags extending `Simai\Docara\CustomTags\BaseTag`

**Localization Flow**:
- Single-locale site: default and only locale is Russian (`DOCS_DIR` → `docs/ru`)
- `translate.config.php` has `languages` set to `[]` (translation disabled); add targets to re-enable
- Translations would output to `source/docs/{locale}/` if targets are added

## Critical Workflows

### Development
```bash
# First-time setup (copies configs, installs deps)
php vendor/bin/docara init --update

# Watch mode (rebuilds on file changes)
yarn run watch
# Builds to build_local/, serves via BrowserSync on localhost:3000

# Production build
yarn prod
php vendor/bin/docara build production
```

### Translation Workflow
- Currently disabled (no target locales). To enable, set `languages` in `translate.config.php` and run:
```bash
php vendor/bin/docara translate
php vendor/bin/docara translate --test
```

### Collection System
- Collections auto-generated from `source/_core/collections.php`
- Scans `DOCS_DIR` for `.settings.php` with `menu['index']` arrays
- Creates routes like `/{locale}/{section}/{page}` or `/{locale}/{section}/` for index pages
- Page metadata in frontmatter: `extends`, `section`, `title`, `description`

## Project-Specific Conventions

### Custom Markdown Tags
Register in `config.php` `tags` array (class name without namespace):
```php
'tags' => ['ExampleTag', 'Folders', 'ListWrap'],
```

Common tags:
- `!folders … !endfolders` - file tree with toggleable folders, syntax: `-` (folder), `--` (file), `(focus)` to highlight
- `!badge [Text] {type=success size=1}` - styled badge component
- `!links … !endlinks` - wraps link list with `.links` class

Tags extend `Simai\Docara\CustomTags\BaseTag`:
- `type()`: tag name in markdown
- `baseAttrs()`: default HTML attributes
- `renderer()`: custom render logic (returns callable or null for default)
- `allowNestingSame()`: allow recursive nesting

### Configuration Patterns
**Layout System** (`config.php` `$layoutConfiguration`):
- Toggle header/footer/sidebars via `enabled` flags
- `asideLeft.blocks.menu` - auto-generated from `.settings.php`
- `asideRight.blocks.navigation` - on-page heading nav (TOC)
- Override per-section in `.settings.php` `layoutOverrides`

**Menu Structure**:
```php
// .settings.php
return [
    'title' => 'Section Title',
    'order' => 1,
    'showInMenu' => true,
    'menu' => [
        'subsection-slug' => 'Display Name',
    ],
];
```

**Blade Layouts**:
- `_core._layouts.master` - base template (header/main/footer)
- `_core._layouts.documentation` - docs pages (breadcrumbs, nav)
- Extends chain: page → documentation → master

### Asset Build
- Mix config in `webpack.mix.js` (root) extends `source/_core/webpack.mix.js`
- Output: `source/assets/build/` (versioned with `mix()` helper)
- Core assets: `source/_core/_assets/{css,js,img,fonts}`
- Custom overrides: `source/img/` → copied to build

### Search Implementation
- Client-side Fuse.js search with `search-index_{locale}.json` (auto-generated)
- Config: `keys: ['title', 'content', 'headings.text']`, `threshold: 0.0`
- Search UI in `_core._components.header.search` + `_core._assets/js/helpers/Search.js`

## Integration Points

**External Dependencies**:
- `simai/ui` CDN (`cdn.jsdelivr.net`) - SF design system components/CSS
- Azure Cognitive Translator API (for `docara translate`)
- Turbo Drive (`@hotwired/turbo`) for SPA-like navigation

**Key Files to Check First**:
- [`config.php`](config.php) - Jigsaw config, site vars, layout toggles, custom tags, locales (ru-only)
- [`source/_core/collections.php`](source/_core/collections.php) - collection generation logic
- [`source/docs/ru/.settings.php`](source/docs/ru/.settings.php) - root menu structure (Russian)
- [`webpack.mix.js`](webpack.mix.js) - asset build pipeline
- [`.env`](.env) - Azure API keys (unused while translation off), `DOCS_DIR` locale path

**Common Pitfalls**:
- Don't edit `source/_core/` directly (overwritten by `docara init --update`)
- Custom tags must be registered in `config.php` AND have class in `source/Helpers/CustomTags/`
- Collections won't generate without `.settings.php` in section root
- Blade components use `@includeWhen(layout_enabled($page, 'header'), ...)` pattern
- Translation requires `.env` with valid Azure credentials

## Testing & Debugging
- Check build errors: `php vendor/bin/docara build local` (outputs to `build_local/`)
- Validate translation config: `php vendor/bin/docara translate --test`
- BrowserSync auto-refresh watches `build_local/**/*` (not source files directly)
- Use `@dd($page)` in Blade for debugging page context
