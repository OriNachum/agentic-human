# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Jekyll blog at **agentic-human.org** — Ori Nachum's blog on agentic development, developer experience, and the evolving relationship between humans and AI systems. Hosted on GitHub Pages via GitHub Actions.

## Commands

```bash
bundle install                # Install Ruby dependencies
bundle exec jekyll serve      # Local dev server at localhost:4000
bundle exec jekyll build      # Build static site to _site/
```

## Architecture

- Standard Jekyll structure: `_layouts/`, `_posts/`, `assets/`, `_config.yml`
- Layout chain: `post.html` → `default.html`
- Posts use `YYYY-MM-DD-title-slug.md` naming with YAML front matter
- Dual-theme CSS in `assets/css/style.css` — warm cream light theme (default) and dark mode, toggled via `data-theme="dark"` on `<html>`, persisted in localStorage
- CSS custom properties (`--bg`, `--surface`, `--border`, `--text`, `--text-muted`, `--heading`, `--accent`, `--accent-hover`) drive both themes
- Fonts: Inter (body), Fira Code (mono). Accent color: `#D97706` (warm amber)
- Permalink pattern: `/:year/:month/:day/:title/`
- Content licensed CC BY 4.0

## Plugins

- `jekyll-feed` — generates `/feed.xml` (RSS/Atom)
- `jekyll-sitemap` — generates `/sitemap.xml`
- `jekyll-seo-tag` — injects `<meta>` and Open Graph tags via `{% seo %}`

## Post Front Matter

```yaml
---
layout: post
title: "Post Title"
date: YYYY-MM-DD
tags: [tag1, tag2]            # displayed on post and index pages
toc: true                     # optional, enables table of contents
original_url: "https://..."   # optional, for republished content
---
```

## Key Files

- `llm.txt` — agent-accessible site description (llmstxt.org spec)
- `robots.txt` — crawl directives + sitemap pointer
- `404.html` — custom 404 page
- `tags.html` — tag listing page (pure Liquid)
- `.github/workflows/pages.yml` — GitHub Actions deployment workflow

## Comments (giscus)

Posts include a giscus comment widget. Requires:
1. GitHub Discussions enabled on the repo
2. giscus GitHub App installed
3. `data-repo-id` and `data-category-id` filled in `_layouts/post.html`
