# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A Jekyll-based photography portfolio and blog website, deployed to GitHub Pages at denzilly.github.io. Based on the "Photography" template by Ram Patra using HTML5UP's Multiverse design.

## Build Commands

```bash
# Install dependencies
npm install
bundle install

# Build CSS and JS (compile SASS, minify JS)
npx gulp build

# Watch SASS changes during development
npx gulp sass:watch

# Process images (resize to full + thumbnail versions, requires ImageMagick)
npx gulp resize

# Full build (CSS, JS, and images)
npx gulp default

# Serve locally
bundle exec jekyll serve
```

## Architecture

**Static Site Generator**: Jekyll 3.10 with github-pages gem

**Asset Pipeline**: Gulp 4
- SASS compiled from `assets/sass/` → `assets/css/*.min.css`
- JS minified in-place to `assets/js/*.min.js`
- Images resized: drop files in `images/` root, gulp creates `images/fulls/` (1024px) and `images/thumbs/` (512px)

**Layout Structure**:
- `_layouts/default.html` - Base HTML wrapper
- `_layouts/post.html` - Blog post template
- `_includes/header.html` - Head meta, CSS, analytics
- `_includes/footer.html` - Script includes

**Content**:
- `index.html` - Photo gallery (home page), iterates over `images/fulls/`
- `blog.html` - Blog post listing
- `_posts/` - Blog posts in `YYYY-MM-DD-title.md` format

**Styling**: SASS modules in `assets/sass/` with variables in `libs/_vars.scss`. Custom styles go in `custom.scss`.

**Configuration**: `_config.yml` controls site title, social links, EXIF display tags, and image paths.

## EXIF Display

Photos display camera metadata (Model, FNumber, ExposureTime, ISO) via EXIF.js when viewed in lightbox. Configure displayed tags in `_config.yml` under the `exif` key.
