# Hugo Setup Notes

This folder has been scaffolded as a Hugo site while keeping your existing exported assets.

## What was added

- `hugo.toml` for Hugo config
- `content/` with key pages extracted from your current HTML (`entry-content` blocks)
- `layouts/_default/` templates for home/single/list pages
- `layouts/partials/sidebar.html` for the right sidebar widgets

## Asset strategy

The WordPress-exported assets were flattened into Hugo's standard `static/` structure to remove `wp-*` paths:

- `static/themes` -> `/themes`
- `static/plugins` -> `/plugins`
- `static/uploads` -> `/uploads`
- `static/js` -> `/js`

Template and content references were updated to these paths.

## Local development

Run from this folder:

```powershell
hugo server -D
```

Open the local URL shown by Hugo (usually `http://localhost:1313/`).

## Build

```powershell
hugo
```

Output is generated in `public/`.

## Editing content

- Home page: `content/_index.md`
- Main pages: files under `content/<slug>/index.md`

You can use Markdown and raw HTML in the same file.

## Session list in sidebar

Upcoming session dates are currently manual and live in `hugo.toml` under:

- `params.upcomingSessions`

Update those entries as needed.

## GitHub Pages deployment options

- Easiest: deploy `public/` as static output.
- Better long-term: use a GitHub Actions workflow to run Hugo on push and publish automatically.

## GitHub Actions deployment

A workflow has been added at `.github/workflows/hugo.yml`.

It will:

- run on pushes to `main`
- build the site with Hugo
- deploy `public/` to GitHub Pages

GitHub repository settings needed once:

- in **Settings > Pages**, set **Source** to **GitHub Actions**

## Navigation and content cleanup

- Main nav now supports dropdowns for **Resources** and **FAQs**.
- Internal content links copied from WordPress-style paths were normalized to Hugo-friendly paths (for example, `/resources/` instead of `../resources/index.html`).
- The mentor signup embed was moved into a Hugo shortcode:
	- `layouts/shortcodes/mailchimp_mentor_signup.html`
	- page uses `{{< mailchimp_mentor_signup >}}`
