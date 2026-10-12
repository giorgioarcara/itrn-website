# itrn.org — Italian Reproducibility Network website

Source of [www.itrn.org](https://www.itrn.org), built with [Quarto](https://quarto.org) and published on GitHub Pages.

## Structure

```
_quarto.yml                  site configuration: navbar, footer, theme
styles/itrn.scss             ITRN theme (brand colours, fonts, cards, grids)
styles/itrn-dark.scss        dark-mode overrides
index.qmd                    home page
join-itrn.qmd, contacts.qmd
news/                        news listing (+ RSS feed at /news/index.xml)
  posts/YYYY-MM-DD-slug/index.qmd
community/                   steering, nodes, mailing list, newsletter
itrn-scientific-events/      "Initiatives": annual meeting, seminars, ReproCoffee, awards, teaching
resources/                   expert list, presentations, governance documents
images/                      logo, favicon, portraits, partner logos
CNAME                        custom domain for GitHub Pages
.github/workflows/publish.yml  renders and publishes on every push to main
```

File paths mirror the old Google Sites URLs (e.g. `/community/steering`,
`/itrn-scientific-events/onlineseminars`), so existing links keep working.
`/home` redirects to the home page.

## Editing

1. Install Quarto (≥ 1.6): <https://quarto.org/docs/get-started/>
2. Live preview while editing:

   ```sh
   quarto preview
   ```

3. Edit the `.qmd` files (plain Markdown). Commit and push to `main`: the site is rebuilt and published automatically.

### Add a news item

Create `news/posts/2026-11-15-my-title/index.qmd`:

```yaml
---
title: "My title"
description: "One-sentence summary shown in listings and on the home page."
date: 2026-11-15
categories: [Events]
image: flyer.jpg        # optional, put the image in the same folder
---

Text of the announcement…
```

It appears automatically on the News page, on the home page (latest 3) and in the RSS feed.

### Other common edits

- **Navigation menu, footer, social links:** `_quarto.yml`
- **Colours and fonts:** `styles/itrn.scss`
- **Steering Committee:** `community/steering.qmd` (portraits in `images/steering/`)
- **Online seminars:** add a row to the right table in `itrn-scientific-events/onlineseminars.qmd`

## Publishing on GitHub Pages (one-time setup)

1. Create the repository and push (example with the GitHub CLI):

   ```sh
   gh repo create <OWNER>/itrn-website --public --source=. --remote=origin --push
   ```

2. Create the `gh-pages` branch once, from your computer:

   ```sh
   quarto publish gh-pages
   ```

3. On GitHub, open **Settings → Pages**: set *Source* to "Deploy from a branch", branch `gh-pages`, folder `/ (root)`.
4. In **Settings → Actions → General → Workflow permissions**, select "Read and write permissions".
5. **Custom domain:** in **Settings → Pages → Custom domain**, enter `www.itrn.org`. Then, at the DNS provider of itrn.org:
   - `www` → `CNAME` record pointing to `<OWNER>.github.io`
   - apex `itrn.org` → `A` records `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`

   When the DNS check passes, tick **Enforce HTTPS**. Until the DNS is switched, the Google Sites version stays online.
6. Optionally, uncomment `repo-url` / `repo-actions` in `_quarto.yml` to show "Edit this page" and "Report an issue" links.

From then on, every push to `main` runs `.github/workflows/publish.yml`, which renders the site and updates `gh-pages`.

## Open items from the migration

- `itrn-scientific-events/teaching.qmd`: add the link to the *Manifesto of the ITRN Teaching group* (embedded Drive file on the old site; its URL is not exposed in the page source).
- `itrn-scientific-events/reproducibility-awards-list.qmd`: the last 2023 honourable mention (Priolo et al.) is truncated on the old site too; complete the sentence.
- Add the ITRN Instagram profile to `_quarto.yml` (only a single post link was found on the old site).

See [IMPROVEMENTS.md](IMPROVEMENTS.md) for proposed structural improvements.
