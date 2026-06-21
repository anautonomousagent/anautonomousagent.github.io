# CLAUDE.md

This file provides context for AI coding assistants working in this repository.

## Project Overview

**An Autonomous Agent** (`anautonomousagent.github.io`) is a personal blog and content archive with the tagline "exploring the noosphere". It was originally a self-hosted WordPress site (WordPress 5.2.3) that was exported to a fully static HTML site and is now served via GitHub Pages (CDN). There is no server-side rendering, no build step, and no package manager — all content is pre-built static HTML.

## Repository Structure

```
/                   Root — contains index.html (homepage) and top-level pages
├── 2012–2019/      Posts organized by year/month/slug/index.html
├── thoughts/       Category archive page
├── books/          Category archive page
├── videos/         Category archive page
├── miscellaneous/  Category archive page
├── to-read/        Category archive page
├── category/       Per-category archive pages (one subdirectory per tag slug)
├── tag/            Per-tag archive pages (one subdirectory per tag slug)
├── author/         Author archive page
├── page/           Paginated homepage archives (page/2/, page/3/, …)
├── feed/           RSS feed
├── comments/       Comments feed
├── wp-content/     Static copies of WordPress theme assets and uploaded media
│   ├── themes/lovecraft/   CSS, JS, and fonts for the Lovecraft theme
│   ├── plugins/            Static assets from WordPress plugins
│   └── uploads/            Uploaded images organized by year/month
├── wp-includes/    Static copies of WordPress core CSS/JS (block library, etc.)
├── wp-json/        Static copy of the WordPress REST API JSON responses
├── sitemap.xml     XML sitemap
├── sitemap.html    HTML sitemap
└── clean-up-commands   Shell one-liners used to post-process the exported HTML
```

There are approximately 1,550 HTML files in the repository.

## Technology Stack

- **Hosting**: GitHub Pages (static CDN, no server-side logic)
- **Original CMS**: WordPress 5.2.3
- **Static export tool**: WP Static Site Generator by Leon Stafford
- **Theme**: Lovecraft (custom WordPress theme)
- **Fonts**: Google Fonts — Lato (400/700/900) and Playfair Display (400/700/italic)
- **Icons**: Genericons icon font
- **JavaScript**: jQuery 1.12.4 (loaded from CDN `code.jquery.com`)
- **Comments**: Disqus (via the `disqus-conditional-load` plugin)

## How the Static Export Works

1. WordPress is installed locally on a GNU/Linux machine.
2. Comments are turned off in WordPress before export.
3. The "WP Static Site Generator By Leon Stafford" plugin crawls the site and outputs all pages as static HTML files.
4. Post-processing shell commands in `clean-up-commands` are run to:
   - Strip WordPress version query strings (e.g. `?ver=5.2.3`) from asset URLs.
   - Rewrite absolute URLs from the original domain to the GitHub Pages domain.
   - Fix Disqus embed script URLs.
5. The resulting files are committed to this repository and served by GitHub Pages.

## Making Changes

Because the site is entirely static HTML:

- **Content changes** require editing the relevant `index.html` file(s) directly.
- **Style changes** require editing files under `wp-content/themes/lovecraft/`.
- **Adding new posts** means creating a new directory under the appropriate `YYYY/MM/slug/` path with an `index.html`, then updating the homepage pagination and any relevant category/tag/archive pages.
- **There is no build system** — changes take effect as soon as the file is saved and pushed.
- **No linter, test suite, or CI pipeline** is currently configured for this repository.

## Content Themes

The blog covers topics including philosophy, science, technology, consciousness, and media. Content types include:

- **Thoughts**: written essays and reflections
- **Books**: book recommendations and notes
- **Videos**: curated documentary and lecture links
- **Miscellaneous**: links and short items that don't fit other categories
- **To-read**: reading list entries
