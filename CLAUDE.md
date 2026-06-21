# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
hugo server                          # dev server at http://localhost:1313 with hot-reload
hugo --gc --minify                   # production build to public/
hugo new artists/band-name.md        # scaffold a new artist page
hugo new releases/ds-035-title.md    # scaffold a new release page
hugo new videos/video-title.md       # scaffold a new video page
hugo new news/2026-06-21-title.md    # scaffold a news post
```

Hugo 0.163.2+ (extended) is required. Deployment is automatic: pushing to `main` triggers GitHub Actions, which builds and deploys to GitHub Pages at discretespectrum.com. The `public/` directory is gitignored — never commit it.

## Architecture

This is a Hugo static site with a single custom theme at `themes/ds-editorial/`. There are no npm dependencies, no JavaScript bundles, and no build pipeline beyond Hugo itself.

### Content sections

All content lives in `content/` across four sections: `artists`, `releases`, `videos`, and `news`. Each section has an archetype in `archetypes/` that scaffolds the correct front-matter when using `hugo new`.

### Cross-linking convention

The templates wire content together using **exact title matching** on front-matter fields — there is no ID-based system. Specifically:

- A release's `artist:` field must exactly match an artist page's `title:` to generate a linked artist name and to list the release on the artist page.
- A video's `artist:` field must exactly match an artist `title:` to link back to the artist page and appear in the artist's video list.
- A video's `release:` field must exactly match a release `title:` to link to the release page and appear in the release's video list.

If these strings don't match exactly (case-sensitive), the link silently degrades to plain text with no cross-reference.

### Front-matter fields by section

**Artists** (`content/artists/`): `status` (`"active"` or `"legacy"`), `weight` (integer; lower = higher on roster), `website`, `bandcamp`, `spotify`, `instagram`, `photo` or `photos` (array).

**Releases** (`content/releases/`): `artist`, `catalog` (e.g. `DS-035`), `format`, `released`, `coverart` (path under `/images/`), `bandcamp`, `spotify`, `bandcamp_embed` (raw iframe HTML).

**Videos** (`content/videos/`): `artist`, `release`, `youtube` (video ID only, not the full URL).

**News** (`content/news/`): no special fields; date in the filename is for sorting, the canonical date is the `date:` front-matter field.

### Theme layout

`themes/ds-editorial/layouts/baseof.html` is the base shell. It reads `coverart`, `photo`, `photos`, and `youtube` params to populate OG/Twitter card meta and JSON-LD structured data automatically — no manual meta tags needed in content files.

`themes/ds-editorial/layouts/_default/single.html` handles all four section types with `{{ if eq .Section "..." }}` blocks. `list.html` does the same for section index pages. `layouts/index.html` is the homepage only.

The homepage shows the 6 most recent releases and videos (ordered by Hugo's default sort, which is `date` descending), then active artists sorted by `weight`.

Artists are split into "Current" (status `active`) and "Legacy" (status `legacy`) on the roster page, each sorted by `weight`.
