# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A static single-page resource hub for Microsoft 365 Copilot, hosted on GitHub Pages at `https://microsoft.github.io/m365-copilot-resources/`. Part of a collection of sister sites:
- https://aka.ms/agent365/resources (github: microsoft/agent365-resources)
- https://aka.ms/copilotstudio/resources (github: microsoft/copilot-studio-resources)

No build step, no dependencies, no package manager. Open `index.html` directly in a browser to develop.

## Architecture

The site is three files:

- **`index.html`** — all content and markup. Each topic is a `.section-card` div with a unique `id` used for both hash navigation and the sticky nav links.
- **`assets/css/styles.css`** — all styling via CSS custom properties defined in `:root`. Brand colors, hero gradient, and icon badge colors are the only things that differ from the sister sites.
- **`assets/js/main.js`** — three behaviors: accordion toggle (`.section-header` click toggles `.open` on `.section-card`), hash-based deep linking (`location.hash` → open + scroll), and real-time search (filters `li` elements inside `.link-list` and `.session-grid`; hides empty cards).

### Content structure in `index.html`

Each section follows this pattern:
```html
<div class="section-card" id="SECTION-ID">
  <button class="section-header" aria-expanded="false">
    <span class="section-icon ICON-CLASS">EMOJI</span>
    <span class="section-title">Title</span>
    <svg class="chevron">...</svg>
  </button>
  <div class="section-body">
    <h3 class="sub-heading">Sub-heading</h3>
    <ul class="link-list"><li>...</li></ul>
    <!-- or for conference sessions: -->
    <ul class="session-grid"><li><a href="..."><span class="session-badge">BRK###</span> Title</a></li></ul>
  </div>
</div>
```

The sticky nav `<nav class="nav-strip">` must have a matching `<a href="#SECTION-ID">` for every `.section-card`.

**Search behavior note:** Search only matches text inside `li` elements — section titles are not searchable by design.

## Images

- `images/og-image.png` — 1200×630 social preview card, generated with Python/Pillow (script in conversation history). Regenerate if the title or URL changes.
- `images/copilot.png` — source for `favicon.ico`; the Microsoft 365 Copilot logo.
- `favicon.ico` — multi-resolution (16–256px), generated from `images/copilot.png` using Pillow.

## Deployment

GitHub Pages serves from the `main` branch root. No configuration file needed — enable in repo Settings → Pages → Source: main / (root).

## Brand colors

The hero gradient (`#061a3a → #0078d4 → #00b4d8 → #4361ee → #9333ea → #3b0764`) uses the cool half of the M365 Copilot logo palette (midnight navy → Microsoft blue → Copilot cyan → blue-violet → vivid purple → deep indigo). This is intentionally distinct from the Copilot Studio sister site, which uses a full warm-to-cool rainbow (pink → orange → teal → blue → purple).
