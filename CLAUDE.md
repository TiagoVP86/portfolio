# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static HTML/CSS/JavaScript personal portfolio for Tiago Vieira, a full-stack developer. No build tools, package managers, or frameworks are used — everything runs directly in the browser with CDN-hosted dependencies (Bootstrap Icons, Google Fonts).

## Local Development

Open `index.html` directly in a browser, or use VS Code Live Server (configured on port 5501 in `.vscode/settings.json`).

There are no install, build, lint, or test commands.

## Architecture

- `index.html` — Single main page containing all sections: header/nav, hero, specialties, about, portfolio, and contact form
- `sucesso.html` — Success page shown after contact form submission
- `style.css` — All styles in one file; uses flexbox and media queries for responsiveness
- `menu.js` — Mobile nav toggle (opens/closes the hamburger menu)
- `images/` — All static assets (project screenshots, profile photos, favicon variants)

## Key Integration Points

- **Contact form:** POSTs to `https://formsubmit.co/devtiagovieira@gmail.com`; success redirect points to `https://tiagovp86.github.io/portfolio/sucesso`
- **Hosting:** GitHub Pages at `tiagovp86.github.io/portfolio`
- **External CDNs:** Bootstrap Icons and Google Fonts loaded via `<link>` tags in `index.html`
