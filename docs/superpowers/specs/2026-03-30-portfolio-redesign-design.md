# Portfolio Redesign — Design Spec
**Date:** 2026-03-30
**Author:** Tiago Vieira
**Status:** Approved for implementation

---

## Overview

Complete redesign of Tiago Vieira's personal portfolio. The goal is to reposition from a junior-leaning frontend showcase to a confident full stack & mobile developer portfolio. The aesthetic is **Dark Editorial** — black background, orange accent, heavy uppercase typography, bento grid layout.

No frameworks, no build tools. Pure HTML/CSS/JS, CDN-hosted fonts. Single `index.html` + `style.css` + `menu.js`.

---

## Visual Identity

### Palette
| Token | Value | Usage |
|---|---|---|
| `--bg` | `#0d0d0d` | Main background |
| `--bg-2` | `#111111` | Alternating section background |
| `--bg-cell` | `#161616` | Bento cells, project cards |
| `--border` | `#1d1d1d` | Subtle borders |
| `--accent` | `#e85d04` | Orange — only color, used sparingly |
| `--text` | `#ffffff` | Primary text |
| `--muted` | `#555555` | Secondary/supporting text |

### Typography
- **Font:** Space Grotesk (Google Fonts) — replaces Poppins
- **Weights used:** 400, 700, 900
- **Style:** Uppercase for headings, tight letter-spacing (-1px to -2px), strong hierarchy
- **Body text:** Regular weight, `--muted` color, kept short

### Motion
- Subtle fade-in on scroll: CSS `@keyframes fadeInUp` triggered via `IntersectionObserver` in a small inline `<script>` block in `index.html`
- Card hover: `transform: translateY(-3px)` + subtle border-color transition to `--accent`
- No bouncing, no floating animations (removes current hero image float)

---

## Implementation Strategy

**Approach:** Full rewrite of `index.html` and `style.css`. The redesign is radical enough that refactoring the existing code would be more complex than starting clean. `menu.js` is reused as-is (mobile nav toggle logic is unchanged).

**Files changed:**
- `index.html` — full rewrite
- `style.css` — full rewrite
- `menu.js` — no changes
- `sucesso.html` — minor style update to match new palette

**Files unchanged:**
- All images in `images/` — reused as-is
- Favicon files — unchanged
- `.vscode/settings.json` — unchanged

---

## Page Structure

### 1. Header / Nav
- Fixed or sticky, transparent background that gains `background: var(--bg)` on scroll
- Left: Logo "TV" in heavy weight, links to `#inicio`
- Center: Nav links — Sobre · Stack · Projetos · Experiência
- Right: "CONTATO" button, orange solid, small, sharp corners (`border-radius: 2px`)
- Mobile: hide desktop nav + button, show hamburger icon; reuse existing `menu.js` toggle logic

### 2. Hero — Centered Manifesto
- Full viewport height (`min-height: 100vh`), content centered vertically
- Eyebrow: `FULL STACK · MOBILE DEVELOPER` — small caps, `--muted`, wide letter-spacing
- Headline: 3-line uppercase, largest font on the page (clamp 48px–96px):
  ```
  TRANSFORMANDO
  CÓDIGO
  EM PRODUTO
  ```
  "CÓDIGO" in `--accent` orange
- Subtext: `React · React Native · Node.js · TypeScript` in `--muted`, small
- CTA: outline button `VER MEU TRABALHO ↓`, border `--accent`, text `--accent`, no fill — links to `#projetos`
- No photo in the hero

### 3. Bento Grid Section
A CSS Grid layout with 2 columns and asymmetric cells. Section id: `#sobre`.

**Cells (desktop layout):**
| Cell | Span | Content |
|---|---|---|
| Stack | full width (2 cols) | Label "STACK" + chips for each tech |
| Sobre | 1 col | Small photo (80×100px) + 2-sentence bio + social icon buttons |
| Projeto destaque | 1 col | Screenshot of top project + name + link |
| Projetos count | 1 col | Large number "6" + label "Projetos" + arrow link |
| Experiência count | 1 col | Large number "+4" + label "Anos de experiência" |

**Tech chips in Stack cell:** React, React Native, TypeScript, Node.js, Express, PostgreSQL, REST APIs
Chips style: border `1px solid --border`, text `--muted`; highlighted chips (core skills) use `border-color: --accent`, `color: --accent`

### 4. Projetos
Section id: `#projetos`. Title: `MEU TRABALHO.` with "TRABALHO" in `--accent`.

**Grid:** 3 columns desktop, 2 columns tablet, 1 column mobile
**Card structure:**
- Screenshot image (full width, fixed height ~200px, `object-fit: cover`)
- Card body: project name, 1-line description, stack chips, links (Live ↗ · GitHub ↗)
- Hover state: `translateY(-3px)`, border turns `--accent`

**Projects to include (from current portfolio):**
1. Fokus — Pomodoro timer em JavaScript puro
2. Meteora — E-commerce em Bootstrap
3. Serenatto — Landing page em Bootstrap
4. Pizzaria Frontend — React
5. Pizzaria Mobile — React Native
6. Pizzaria Backend — Node.js / API

### 5. Experiência
Section id: `#experiencia`. Title: `EXPERIÊNCIA.`

**Timeline:** vertical line in `--accent` on the left, items stacked
**Each item:**
- Orange dot on the timeline line
- Company name (bold, white)
- Period + role (small, `--muted`, orange for dates)
- Technologies used (chips, same style as stack chips)

> **Note:** Placeholder company names used in implementation. Tiago fills in real data after.

### 6. Contato
Section id: `#formulario`. Title: `FALE COMIGO.`

- Same `formsubmit.co` action and hidden fields (email, `_next`, `_captcha`) — no backend changes
- Fields: Nome, Email, Telefone, Mensagem
- Field style: `background: var(--bg-2)`, border `1px solid var(--border)`, no border-radius or `border-radius: 2px`
- Submit button: orange solid, uppercase, full width of form

### 7. Footer
- Logo "TV" left
- Social icon buttons (LinkedIn, GitHub, Instagram) right — circular, orange background
- Second line: email link, centered
- Top border: `1px solid var(--accent)`

---

## Responsiveness

| Breakpoint | Behavior |
|---|---|
| `> 1020px` | Full desktop layout, 3-col project grid, 2-col bento |
| `768px–1020px` | 2-col project grid, 2-col bento collapses to stacked |
| `< 768px` | 1-col everything, hamburger menu, bento cells full width |

---

## Constraints
- No JavaScript beyond `menu.js` (mobile nav) and optional `IntersectionObserver` for scroll animations
- No external CSS frameworks
- Contact form backend unchanged (formsubmit.co)
- All existing images reused — no new assets required
- `.gitignore` should include `.superpowers/`
