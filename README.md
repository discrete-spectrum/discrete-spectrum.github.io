# Discrete Spectrum

Static website for Discrete Spectrum Records. Built with [Hugo](https://gohugo.io), hosted on GitHub Pages at [discretespectrum.com](https://discretespectrum.com).

---

## Dev

### Prerequisites

Hugo 0.163.2+ (extended). Install or upgrade via Homebrew:

```bash
brew install hugo
```

### Run the dev server

```bash
hugo server
```

Site is live at http://localhost:1313/ with hot-reload — save any file and the browser updates instantly.

### Build for production

```bash
hugo --gc --minify
```

Output goes to `public/`. In practice you rarely need to run this manually — the GitHub Actions workflow builds and deploys automatically on every push to `main`.

---

## Adding content

All content lives in `content/`. Each file is Markdown with a front-matter block at the top.

### Add an artist

```bash
hugo new artists/band-name.md
```

Then open `content/artists/band-name.md` and fill in the front-matter fields. Link fields (`bandcamp`, `website`, `spotify`, `instagram`) only render on the page when they have a value — leave blank to hide.

### Add a release

```bash
hugo new releases/ds-012.md
```

Then fill in `content/releases/ds-012.md`. Cover art goes in `static/images/covers/` and is referenced as `coverart: /images/covers/ds-012.jpg`.

### Add a news post

```bash
hugo new news/2026-06-18-post-title.md
```

Posts are reverse-chronological. The date in the filename is just for sorting; the canonical date is the `date:` field in front-matter.

---

## Mobile preview

### Chrome DevTools (quickest)

1. Open http://localhost:1313/ in Chrome
2. Open DevTools: `Cmd+Option+I`
3. Toggle the device toolbar: `Cmd+Shift+M`
4. Pick a device preset (iPhone, Pixel, etc.) or drag the viewport edge to a custom width

### Real device on the same WiFi

Start the server bound to your local network instead of just localhost:

```bash
hugo server --bind 0.0.0.0 --baseURL http://$(ipconfig getifaddr en0)/
```

Then open `http://<your-mac-ip>:1313/` on your phone. The terminal output will print the exact URL when the server starts.

To find your Mac's local IP manually:

```bash
ipconfig getifaddr en0
```

Or: **System Settings → Wi-Fi → click your network name → IP address**.
