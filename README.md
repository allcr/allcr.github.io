# allcr.github.io

Pelican-powered site, built and deployed by GitHub Actions on every push to `main`.

## One-time repo setup

1. On GitHub, create a new repo named exactly `allcr.github.io` (empty, no README/gitignore/license).
2. From this folder:

   ```fish
   cd allcr.github.io
   git init
   git add .
   git commit -m "Initial Pelican site"
   git branch -M main
   git remote add origin git@github.com:allcr/allcr.github.io.git
   git push -u origin main
   ```

3. In the repo on GitHub: **Settings -> Pages -> Build and deployment -> Source**, select
   **GitHub Actions**. That's it — the workflow in `.github/workflows/pelican.yml` handles the
   build and deploy on every push. First run takes a minute or two; the site will be live at
   `https://allcr.github.io`.

## Local development

```fish
uv venv
uv pip install -r requirements.txt
pelican -r -l
```

`-r` rebuilds on file changes, `-l` serves at http://localhost:8000. Ctrl-C to stop.

To just build once without serving:

```fish
pelican content -o output -s pelicanconf.py
```

## Adding content

- New posts go in `content/articles/` as `.md` files with `Title`, `Date`, `Category` metadata
  at the top (see `content/articles/welcome.md` for the format).
- Standalone pages (About, etc.) go in `content/pages/`.
- Images go in `content/images/` and are referenced as `{static}/images/whatever.png`.

## Config files

- `pelicanconf.py` — used for local dev (`pelican -r -l`), relative URLs, no feeds.
- `publishconf.py` — used by CI (`publishconf.py` imports `pelicanconf.py` and overrides
  `SITEURL` to the real domain, turns on absolute URLs and Atom feeds).

## Theme

Currently using Pelican's bundled `notmyidea` theme, set in `pelicanconf.py`. Browse more at
https://pelicanthemes.com if you want something else — drop the theme folder into a `themes/`
directory and point `THEME` at it.
