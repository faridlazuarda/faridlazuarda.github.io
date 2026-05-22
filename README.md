# faridlazuarda.github.io

Source code for [faridlazuarda.github.io](https://faridlazuarda.github.io), Farid Adilazuarda's academic homepage.

The site is built with [Jekyll](https://jekyllrb.com/) and a modified [al-folio](https://github.com/alshedivat/al-folio) theme. The repository keeps the theme structure, but the live site is intentionally small: homepage, resume, publications, teaching, news, and static assets.

## Site Content

The main editable content lives in:

- `_pages/about.md` - homepage biography and research summary
- `_pages/cv.md` - resume page
- `_pages/publications.md` - publications page wrapper
- `_bibliography/papers.bib` - publication entries
- `_news/` - homepage news items
- `_config.yml` - site metadata, navigation, plugins, and feature flags
- `assets/img/prof_pic.jpg` - profile photo

Inherited al-folio demo posts and demo media are kept in the repository for reference, but they are excluded from the generated site through `_config.yml`.

## Local Setup

Install Ruby and Node dependencies:

```bash
bundle install
npm install
```

Serve the site locally:

```bash
bundle exec jekyll serve
```

Build the site the same way the deployment workflow does:

```bash
bundle exec jekyll build --lsi
npx -y purgecss -c purgecss.config.js
```

The generated site is written to `_site/`.

## Checks

Run the formatting check:

```bash
npx prettier . --check
```

Run the Jekyll build:

```bash
bundle exec jekyll build --lsi
```

Run CSS purging after the build:

```bash
npx -y purgecss -c purgecss.config.js
```

Run a secrets scan if `gitleaks` is installed:

```bash
gitleaks detect --no-git
```

## Deployment

Deployment is handled by GitHub Actions in `.github/workflows/deploy.yml`.

On pushes to `master`, the workflow:

1. Installs Ruby dependencies.
2. Builds the Jekyll site with `bundle exec jekyll build --lsi`.
3. Runs PurgeCSS.
4. Deploys `_site/` to GitHub Pages.

The broken-link and Prettier workflows run on pull requests and pushes. They intentionally ignore upstream template docs, generated files, and demo assets that are not part of the live site.

## Maintenance Notes

- Keep public content changes in `_pages/`, `_news/`, `_bibliography/`, and `assets/img/`.
- Keep theme/config changes scoped and verify with the commands above.
- Do not re-enable inherited blog/demo machinery unless the site is going to publish blog posts.
- If a new page uses code blocks, notebooks, project cards, image zoom, or other optional al-folio features, check `_config.yml` and `_includes/scripts/` so the needed assets are enabled deliberately.

## Attribution

This site is based on the al-folio Jekyll theme and keeps the upstream license in `LICENSE`.
