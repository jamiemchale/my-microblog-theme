# Repository Guidelines

This is a Hugo blog template for a Micro.blog theme. For all suggestions and edits consider the work in context of Micro.blog and the micro.blog service.

Micro.blog uses Hugo 0.91 - so make sure all templates, themes and settings are compatible with this version.

## Project Structure & Module Organization

- `layouts/`: Hugo templates (`_default/`, `partials/`, `post/`, `section/`). Start from `_default/baseof.html` and override blocks in `single.html` and `list.html`.
- `assets/css/`: Source styles (`main.css`) and `tailwind.config.js`. Edit here; output is generated.
- `static/css/`: Built CSS (`main.css`) served by Hugo. Do not edit by hand.
- `archetypes/`: Default front matter templates.
- `theme.toml`: Theme metadata (name, author, description).
- `package.json`, `.prettierrc`: Tooling config (Tailwind CLI, Prettier + Go template parser).

## Build, Test, and Development Commands

- Install tooling: `npm ci` (uses `package-lock.json`).
- Build CSS (once): `npx @tailwindcss/cli -i assets/css/main.css -o static/css/main.css --minify`.
- Watch CSS during dev: `npx @tailwindcss/cli -i assets/css/main.css -o static/css/main.css --watch`.
- Preview in a site: from your Hugo site (that references this theme), run `hugo server -t my-microblog-theme`. Use your site’s `config` to select the theme.

## Coding Style & Naming Conventions

- Indentation: 2 spaces; no tabs.
- Templates: Hugo Go templates. Prefer lowercase, hyphenated filenames (e.g., `pagination.html`). Keep reusable bits in `layouts/partials/`.
- CSS: Favor Tailwind utilities; add small component classes in `assets/css/main.css`. Configure design tokens in `tailwind.config.js`.
- Formatting: Prettier with `prettier-plugin-go-template`. Run `npx prettier --write "layouts/**/*.html" "assets/**/*.css" "*.md"`.

## Testing Guidelines

- No unit tests; validate visually: home (`layouts/index.html`), lists, singles, replies, and partials (header/footer) at mobile and desktop widths.
- Run `hugo --gc --minify` in a parent site to catch template errors. Check browser console and broken links.

## Commit & Pull Request Guidelines

- Commits: Imperative mood with conventional prefixes: `feat:`, `fix:`, `style:`, `refactor:`, `docs:`, `chore:` (e.g., `fix: correct replies pagination include`).
- Branching: Small, focused branches; one concern per PR.
- PRs: Include a short description, linked issue (if any), before/after screenshots for UI changes, and note whether CSS was rebuilt. Avoid committing generated `static/css/main.css` unless the change requires it.

## Security & Configuration Tips

- Avoid inline scripts; use Hugo’s safe functions (`safeURL`, `relURL`).
- Keep secrets/config out of the theme; the parent site should provide content and settings.
