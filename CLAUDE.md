# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the **frontend** of Hobbylos Search — a podcast search engine for the German podcast "Hobbylos" (Rezo & Julien Bam). Static HTML/CSS/JS site hosted at `search.hobbylos.online`, calling `https://api.hobbylos.online/` for search queries.

The parent directory (`../`) contains the full project CLAUDE.md with backend details. The backend lives in `../docker-search/`.

## Architecture

**No build system, no bundler, no framework.** Pure static files served directly. All JavaScript is inline in the HTML files.

### Key Pages

- `index.html` — Main search page. Contains all search logic: form handling, API calls via `fetch()`, DOM-based result rendering, pagination (previous/next), sort dropdown (relevance / newest / oldest), URL state management via `pushState`
- `zertifikat.html` — Spotify OAuth-protected page (certificate/Zertifikat feature) with login/logout flow using bearer tokens
- `habit-private-aiusdhs9328husa9d8z.html` / `habit-public-oa7sndzma8dn0a7.html` — "Habit" matching feature pages (private requires Spotify auth, public is read-only)
- `higher-lower.html` — Higher-Lower game using podcast search counts
- `rangliste.html` — Leaderboard/ranking page
- `datenschutz-impressum-usw.html` / `datenschutz-impressum.html` — Privacy/legal pages

### Frontend-Backend Contract

The frontend calls the API at `https://api.hobbylos.online/` with these query params:
- `word` (required) — search term
- `offset`, `limit` — pagination
- `sort_by_time` — `forward` (newest) or `reverse` (oldest), omit for relevance

API response fields use short keys: `search[]` array with `L` (relevance/date), `f` (Spotify episode ID), `n` (episode name), `s` (timestamp in seconds), `text` (context snippet). Pagination via `next`/`previous` URLs, `v`/`b` for offset/limit, `count_all` for result count message.

Spotify links are constructed as: `https://open.spotify.com/episode/{f}?go=1&t={s}&utm_source=search.hobbylos.online`

### Styling

- `css/init.css` — Reset/normalize styles
- `css/main.css` — All layout and component styles. Uses `vw` units extensively for responsive sizing. Three breakpoints: 991px, 767px. Background uses blurred podcast cover image with webp/jpg fallbacks via `image-set()`.
- Font: Bebas Neue (loaded externally), fallback sans-serif
- Dark theme (background `#292626`, white text)

### Security

- XSS protection: All dynamic content uses `textContent` / `createElement`, never `innerHTML` for user data. `escapeHtml()` utility exists but DOM methods are preferred.
- Cloudflare Turnstile loaded on index page (captcha protection)

## Development

No build step. Edit HTML/CSS/JS files directly and open in browser or deploy to hosting.

**Local testing:** Open `index.html` in a browser. API calls go to `https://api.hobbylos.online/` (production), so search functionality requires the backend to be running.

**Deployment:** Static files are hosted on Infomaniak. Upload changed files to the web hosting.

## Projektregeln

- Nach jeder Änderung am Code oder an Dateien sollen die Änderungen in der CLAUDE.md im Parent-Verzeichnis (`../CLAUDE.md`) dokumentiert werden
