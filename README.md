# CoderDojo Brighton Website

![Hugo](https://img.shields.io/badge/Hugo-0.136.4-ff4088?logo=hugo)
![Theme](https://img.shields.io/badge/theme-CoderDojoBrighton2013-2f855a)
![GitHub Pages](https://img.shields.io/badge/deploy-GitHub%20Pages-222222?logo=github)

A Hugo-powered website for CoderDojo Brighton.

This repository contains the site content, Hugo configuration, GitHub Pages deployment workflow, and the extracted custom theme used to preserve the existing site design.

## What This Project Does

This project builds and deploys the CoderDojo Brighton website as a static Hugo site.

It includes:
- Content pages written in Markdown, with optional inline HTML where needed
- A custom Hugo theme in `themes/CoderDojoBrighton2013`
- A GitHub Actions workflow for automatic GitHub Pages deployment
- A page-bundle-based content structure for images and PDFs

## Why It Is Useful

This repo makes the site easier to maintain than the old WordPress-style export.

Benefits:
- Fast local development with Hugo
- Simple content editing in Markdown
- Predictable page URLs such as `/python/` and `/resources/`
- Version-controlled menus, theme changes, and content updates
- Better organization for page-specific files like images and PDFs
- GitHub Pages deployment on push to `main`

## Project Structure

```text
.
|-- .github/workflows/hugo.yml
|-- content/
|-- hugo.toml
|-- themes/CoderDojoBrighton2013/
|-- public/
|-- README.md
`-- README-HUGO.md
```

Important locations:
- `content/`: page content
- `content/_index.md`: home page content
- `content/<slug>/index.md`: a normal page bundle
- `themes/CoderDojoBrighton2013/layouts/`: templates and partials
- `themes/CoderDojoBrighton2013/static/`: theme-owned static assets
- `hugo.toml`: site config, menus, and sidebar session data
- `.github/workflows/hugo.yml`: GitHub Pages build and deploy workflow
- `public/`: generated output from Hugo

## Getting Started

### Prerequisites

- [Hugo extended](https://gohugo.io/installation/) `v0.136.4` or newer
- Git

### Run Locally

Run commands from the repository root.

```powershell
hugo server --disableFastRender
```

Open the local URL shown by Hugo, usually:

```text
http://localhost:1313/
```

Important:
- Run Hugo from the repo root, the folder containing `hugo.toml`
- Do not run it from `D:\` or another parent directory

### Build the Site

```powershell
hugo
```

The generated site is written to `public/`.

## Editing Existing Pages

Most site pages are leaf bundles:

```text
content/
`-- python/
    |-- index.md
    |-- 1.png
    |-- Guide_-Drawing-a-snowman-1.pdf
    `-- power.png
```

To edit a page:
1. Open its `index.md`
2. Update the Markdown content
3. Keep any page-specific files in the same folder as `index.md`
4. Preview locally with `hugo server --disableFastRender`

Examples:
- Home page: `content/_index.md`
- Python page: `content/python/index.md`
- Resources landing page: `content/resources/index.md`
- Nested page: `content/resources/music-with-sonic-pi/index.md`

## Creating a New Page

Create a new page as a leaf bundle so page-specific assets can live beside the page.

Example:

```text
content/my-new-page/
`-- index.md
```

Minimal example:

```md
---
title: "My New Page"
slug: "my-new-page"
---

## Page heading

Add your content here.
```

This will create the URL:

```text
/my-new-page/
```

For a nested page, create a nested folder:

```text
content/resources/my-topic/index.md
```

This will create:

```text
/resources/my-topic/
```

## Images, PDFs, and Other Files

### Best Practice in This Repo

Use page bundles for files that belong to one page.

Put images and PDFs next to the page's `index.md`:

```text
content/python/
|-- index.md
|-- power.png
`-- worksheet.pdf
```

Then reference them with bundle-relative paths.

### Referencing Images in Markdown

If the image is in the same page bundle:

```md
![Power sprite](power.png)
```

Linked thumbnail example:

```md
[![Sonic Pi](sonic-pi-code-border-300x300.png)](sonic-pi-code-border.png)
```

### Referencing PDFs in Markdown

If the PDF is in the same page bundle:

```md
[Download the worksheet](worksheet.pdf)
```

### When to Use Theme Static Assets

Use `themes/CoderDojoBrighton2013/static/` for assets that are shared by the site design rather than one page.

Examples:
- Header background images
- Theme CSS, JS, and icons
- Shared decorative assets used by templates

Example theme asset URL:

```text
/themes/twentythirteen/images/site-header.jpg
```

### What Not to Do

Avoid adding new files to an `uploads` folder.

For this Hugo site:
- Page-specific files belong in the relevant `content/<page>/` bundle
- Theme-owned shared assets belong in `themes/CoderDojoBrighton2013/static/`

## Menus and Navigation

The main navigation is configured in `hugo.toml` under `[menu]`.

To:
- rename menu items
- reorder items
- add dropdown children
- point items at new pages

edit the `[[menu.main]]` entries in `hugo.toml`.

## Reusable Content and Includes

This site uses Hugo shortcodes for reusable embedded content.

Current example:
- `themes/CoderDojoBrighton2013/layouts/shortcodes/mailchimp_mentor_signup.html`

Used in content like this:

```md
{{< mailchimp_mentor_signup >}}
```

Use a shortcode when:
- the same embedded markup is reused in more than one place
- a block contains complex HTML, scripts, or third-party embed code

## Styling and Theme Changes

The active theme is defined in `hugo.toml`:

```toml
theme = "CoderDojoBrighton2013"
```

Most visual changes belong in:
- `themes/CoderDojoBrighton2013/layouts/`
- `themes/CoderDojoBrighton2013/static/themes/twentythirteen/`

Be careful not to edit generated files inside `public/`.

## Deployment

GitHub Pages deployment is configured in `.github/workflows/hugo.yml`.

On push to `main`, the workflow:
1. Installs Hugo extended
2. Builds the site
3. Uploads `public/`
4. Deploys to GitHub Pages

Repository setting required:
- In GitHub repository settings, set Pages source to `GitHub Actions`

## Help and Documentation

Useful repo files:
- [README-HUGO.md](README-HUGO.md)
- [hugo.toml](hugo.toml)
- [.github/workflows/hugo.yml](.github/workflows/hugo.yml)
- [themes/CoderDojoBrighton2013/theme.toml](themes/CoderDojoBrighton2013/theme.toml)

External documentation:
- [Hugo documentation](https://gohugo.io/documentation/)
- [Hugo content management](https://gohugo.io/content-management/)
- [Hugo menu configuration](https://gohugo.io/content-management/menus/)
- [GitHub Pages documentation](https://docs.github.com/pages)

## Maintainers and Contributions

Maintained by CoderDojo Brighton.

Contributions are welcome through normal GitHub collaboration:
- create a branch
- make and test changes locally
- open a pull request

Recommended contribution workflow:
1. Run `hugo server --disableFastRender`
2. Preview your change locally
3. Run `hugo`
4. Commit the content, config, or theme updates
5. Open a pull request for review

## Quick Reference

```powershell
# Start local dev server
hugo server --disableFastRender

# Build production output
hugo
```

```text
Edit a page:             content/<slug>/index.md
Add page image:          content/<slug>/image.png
Add page PDF:            content/<slug>/file.pdf
Theme shared asset:      themes/CoderDojoBrighton2013/static/...
Do not edit generated:   public/
Menus and sessions:      hugo.toml
```
