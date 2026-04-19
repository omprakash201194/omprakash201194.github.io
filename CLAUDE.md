# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Static personal portfolio site for Omprakash Gautam, deployed via GitHub Pages at `omprakash201194.github.io`. No build step, no package manager, no tests — plain HTML/CSS/JS served directly. The `CNAME` file exists but is currently empty (custom domain was removed, see commit `8dbe93b`).

## Local preview

Any static file server works. From the repo root:

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

Changes pushed to `master` go live on GitHub Pages automatically.

## Architecture

- **`index.html`** — single-page portfolio (home, about, skills, experience, education, testimonials, projects, contact). All section content is hardcoded here.
- **`projects/*.html`** — one standalone HTML page per vanilla-JS mini-project (custom video player, DOM array methods, exchange rate calculator, form validation, movie seat selector). Each links its own dedicated CSS and JS in `css/` and `js/` by matching filename.
- **`css/style.css`** — main compiled stylesheet for `index.html`. Source is in `scss/style.scss` + partials (`_variables`, `_typography`, `_buttons`, `_common`, `_mixins`) and `scss/templates/`. If editing styles for the portfolio itself, edit the SCSS and recompile; the other `css/*.css` files (one per project) are hand-written and not generated from SCSS.
- **`js/script.js` / `js/scripts.js`** — portfolio page behavior (nav, slick slider, shuffle grid). Per-project JS files are independent and only loaded by their matching project page.
- **`plugins/`** — vendored third-party libs (Bootstrap 4, jQuery, slick slider, shuffle, themify-icons). Do not modify; upgrade by replacing the directory.

## Conventions

- When adding a new mini-project, follow the existing triplet pattern: `projects/<name>.html` + `css/<name>.css` + `js/<name>.js`, and add a card linking to it in the Projects section of `index.html`.
- Keep asset paths relative (no leading `/`) so the site works both at the repo root and under a subpath.
- Don't introduce a build tool or framework unless explicitly asked — the site's value prop is that it's trivially hostable on GitHub Pages.
