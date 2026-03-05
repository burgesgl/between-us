# CLAUDE.md — Between Us

## Project Overview

**Between Us** is a couples' conversation card game — a single-page web application that helps partners connect through curated discussion prompts. It features "Joe," a cat mascot with witty commentary, 20+ topic categories, preset game modes, mini-games (Tic Tac Toe, Connect 4), and a starry night visual theme.

## Architecture

The entire application lives in a single self-contained file:

```
index.html    # ~650 lines — HTML structure, CSS, and JavaScript all inline
```

There is no build system, no package manager, no external dependencies (aside from Google Fonts loaded via CDN). The file is ready to open directly in a browser.

### Structure within `index.html`

1. **`<style>` block** — All CSS, including CSS custom properties (theming), responsive layout, animations, and component styles
2. **`<body>` HTML** — Three screens (`intro`, `selector`, `gameScreen`) plus overlay/drawer UI
3. **`<script>` block** — All application logic: data (categories, presets, Joe quotes), game state, DOM manipulation, mini-games, canvas rendering

## Code Conventions

- **No frameworks** — Vanilla HTML/CSS/JS only
- **Minified inline styles** — CSS is compact, one rule per line, using CSS custom properties for the color system
- **camelCase** for JS variables and functions (`selectedCats`, `drawCard`, `showScreen`)
- **Kebab-case** for CSS classes and data attributes (`.preset-card`, `.sel-card`, `data-cat`)
- **Inline event handlers** — Mix of `onclick` attributes in HTML and `addEventListener` in JS
- **No modules or imports** — Everything is in the global scope within one `<script>` tag
- **Functional style** — Named functions at the top level, no classes
- **`var`/`let`/`const`** — Uses `const` and `let` in newer code, some `var` in older patterns

## Theming & Design System

Colors are defined as CSS custom properties on `:root`:
- Brown palette: `--brown-deep` through `--brown-cream` (primary UI tones)
- Accent colors: `--teal`, `--sage`, `--dusty-rose`, `--amber`, `--rust`, `--plum`, etc.
- Semantic tokens: `--bg`, `--parchment`, `--text-body`, `--text-muted`
- Typography: Playfair Display (headings), Lora (italic/body), Nunito (UI/sans-serif)

## Key Application Concepts

- **Screens**: Three main views toggled via `.screen.active` — intro, category selector, game
- **Categories**: ~20 topics (connection, communication, dreams, etc.) each with icon, name, color, and question array
- **Presets**: Curated combinations of categories for quick game setup (e.g., "First Date Night", "Deep Dive")
- **Quick Draws**: Shorter game configurations
- **Joe**: Cat mascot with sweet, surly, and philosophical response modes; category-specific commentary
- **Drawer**: Side panel with tabs for History, Saved cards, Tally, and mini-Games
- **Mini-games**: Tic Tac Toe and Connect 4 with score tracking, used as break activities

## Development Workflow

### Running locally
```bash
# Open directly in a browser — no server required
open index.html
# Or use any static file server
python3 -m http.server 8000
```

### Making changes
Since everything is in one file, edits are straightforward but require care:
- CSS changes: edit within the `<style>` block
- Content changes (questions, categories, Joe quotes): edit the data structures in `<script>`
- UI/layout changes: edit the HTML body and corresponding CSS
- Logic changes: edit functions in the `<script>` block

### No build, lint, or test commands
There is no `package.json`, no linter, no test framework, and no build step. Validate changes by opening the file in a browser and testing manually.

## Important Notes for AI Assistants

- **Single file architecture**: Do not split this into multiple files unless explicitly asked. The single-file design is intentional for simplicity and portability.
- **Preserve the minified CSS style**: CSS is written compactly (one declaration block per line). Match this style when adding new CSS.
- **Joe's personality matters**: When adding or modifying Joe's quotes, maintain his character — witty, slightly sarcastic, cat-themed, and endearing.
- **Mobile-first**: The app targets mobile viewports. Test responsive behavior and use `clamp()`, `dvh`, and flexible units as the existing code does.
- **No external dependencies**: Do not introduce npm packages, frameworks, or build tools unless specifically requested.
- **Accessibility**: The app uses semantic elements, keyboard navigation (Space/Arrow keys on game screen), and readable contrast. Preserve these when making changes.
