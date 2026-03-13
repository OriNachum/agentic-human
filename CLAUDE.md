# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Jekyll blog at **agentic-human.org** — Ori Nachum's blog on autonomous intelligence, agentic development, and developer experience. Hosted on GitHub Pages.

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
- Custom dark theme in `assets/css/style.css` (no CSS framework — hand-rolled with Inter/Fira Code fonts, #6c63ff accent)
- Permalink pattern: `/:year/:month/:day/:title/`
- Content licensed CC BY 4.0

## Post Front Matter

```yaml
---
layout: post
title: "Post Title"
date: YYYY-MM-DD
original_url: "https://..."  # optional, for republished content
---
```
