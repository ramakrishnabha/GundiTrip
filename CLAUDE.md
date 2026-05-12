# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this project is

A single-file static travel itinerary page for an 18-day trip to London, Oxford, and the Cotswolds (26 May – 7 June 2026). Hosted on GitHub Pages at `https://ramakrishnabha.github.io/GundiTrip/`.

The entire site is one file: `index.html` — all CSS, JavaScript, and HTML in one place. There is no build step, no package manager, no dependencies to install.

## Deploying

Every change is deployed by committing and pushing to `main`:

```bash
git add index.html
git commit -m "description"
git push origin main
```

GitHub Pages auto-deploys within ~1 minute. Hard-refresh (Cmd+Shift+R) to bust the browser cache after deploying.

## Architecture of index.html

The file is structured in order: `<style>` → HTML body.

**CSS custom properties** (`:root`) define the colour palette: `--pink`, `--purple`, `--teal`, `--yellow`, `--blue`, `--green`, `--gold`, `--bg`, `--card`, `--border`.

**Phase wrappers** group days by trip section and control the top-border gradient colour of day cards via CSS class:
- `.phase-settle` — arrival days (teal/blue)
- `.phase-oxford` — Oxford & Cotswolds (purple/pink)
- `.phase-london` — London iconic day (yellow/pink)
- `.phase-day-out` — museum/royal days (blue/teal)
- `.phase-fun` — fun days (green/teal)
- `.phase-farewell` — last day (pink/purple)

**Activity highlighting** — add class `hp` or `shop` to `.activity` to get the gold Harry Potter glow + "⚡ HP" badge, or the pink shopping glow + "🛍️ Shop" badge respectively.

**Oxford tabbed section** — three tabs (`ox0`, `ox1`, `ox2`) switched via `switchOxTab(index)`. Active tab has class `active` on both `.ox-tab` and `.ox-day`.

**Trip photos** — inline `.trip-photos` grid (two columns, stacks to one on mobile) placed inside `.act-body` after `.act-note`. Single photo: one `.trip-photo` div. Two photos: two `.trip-photo` divs side by side. Images are sourced from Unsplash (`images.unsplash.com`) or Wikimedia Commons (`upload.wikimedia.org`). Always verify image URLs return HTTP 200 before adding.

**Edit mode** — pencil button toggles `contentEditable` on all `.act-name`, `.act-note`, `.day-title`, and `.tip-box` elements. Changes are persisted to `localStorage` under key `gunditrip_edits` and restored on page load.

**Weather strips** — `.weather-strip` inside each day card, sourced from Open-Meteo historical archive (2025 actuals for the same calendar dates). The disclaimer reads "last year's actuals".
