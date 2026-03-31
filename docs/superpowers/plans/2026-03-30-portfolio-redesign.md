# Portfolio Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rewrite index.html and style.css to implement a Dark Editorial aesthetic with bento grid layout, repositioning Tiago's portfolio as a confident full stack & mobile developer.

**Architecture:** Full rewrite of index.html and style.css — no incremental refactor. menu.js is reused unchanged. All images reused. sucesso.html updated for palette consistency.

**Tech Stack:** HTML5, CSS3 (custom properties, CSS Grid, Flexbox), vanilla JS (IntersectionObserver), Space Grotesk via Google Fonts, Bootstrap Icons via CDN.

---

## File Map

| File | Action | Responsibility |
|---|---|---|
| `index.html` | Rewrite | Full page structure — all 7 sections |
| `style.css` | Rewrite | All styles — palette vars, typography, layout, components, responsive |
| `menu.js` | No change | Mobile nav toggle — logic unchanged |
| `sucesso.html` | Update | Match new palette (dark bg, orange accent) |
| `.gitignore` | Update | Add `.superpowers/` entry |

---

## Task 1: Setup — gitignore + base CSS variables

**Files:**
- Modify: `.gitignore`
- Rewrite: `style.css`

- [ ] **Step 1: Add .superpowers/ to .gitignore**

Open `.gitignore` (create if absent). Add:

```
.superpowers/
```

- [ ] **Step 2: Rewrite style.css with CSS variables and base reset**

Replace the entire contents of `style.css` with:

```css
/* =============================================
   DESIGN TOKENS
   ============================================= */
:root {
  --bg:       #0d0d0d;
  --bg-2:     #111111;
  --bg-cell:  #161616;
  --border:   #1d1d1d;
  --accent:   #e85d04;
  --text:     #ffffff;
  --muted:    #555555;
}

/* =============================================
   RESET & BASE
   ============================================= */
*, *::before, *::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  background-color: var(--bg);
  color: var(--text);
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 400;
  line-height: 1.6;
}

body::-webkit-scrollbar {
  display: none;
}

a {
  text-decoration: none;
  color: inherit;
}

ul {
  list-style: none;
}

img {
  display: block;
  max-width: 100%;
}

/* =============================================
   LAYOUT UTILITIES
   ============================================= */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 5%;
}

/* =============================================
   SCROLL ANIMATION
   ============================================= */
.fade-up {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

.fade-up.visible {
  opacity: 1;
  transform: translateY(0);
}

/* =============================================
   SECTION TITLES
   ============================================= */
.section-title {
  font-size: clamp(28px, 4vw, 42px);
  font-weight: 900;
  letter-spacing: -1px;
  text-transform: uppercase;
  color: var(--text);
  margin-bottom: 48px;
}

.section-title span {
  color: var(--accent);
}

/* =============================================
   CHIPS (tech tags)
   ============================================= */
.chip {
  display: inline-block;
  border: 1px solid var(--border);
  color: var(--muted);
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1px;
  padding: 3px 10px;
  border-radius: 2px;
  text-transform: uppercase;
}

.chip.hi {
  border-color: var(--accent);
  color: var(--accent);
}
```

- [ ] **Step 3: Commit**

```bash
git add .gitignore style.css
git commit -m "feat: base CSS variables, reset, and utility classes"
```

---

## Task 2: HTML skeleton + Google Fonts

**Files:**
- Rewrite: `index.html`

- [ ] **Step 1: Write the full HTML skeleton**

Replace the entire contents of `index.html` with:

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- Google Fonts: Space Grotesk -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;700;900&display=swap" rel="stylesheet" />

  <!-- Bootstrap Icons -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css" />

  <!-- Favicons -->
  <link rel="apple-touch-icon" sizes="180x180" href="./images/apple-touch-icon.png" />
  <link rel="icon" type="image/png" sizes="32x32" href="./images/favicon-32x32.png" />
  <link rel="icon" type="image/png" sizes="16x16" href="./images/favicon-16x16.png" />

  <link rel="stylesheet" href="style.css" />
  <script src="menu.js" defer></script>

  <title>Tiago Vieira — Full Stack & Mobile Developer</title>
</head>
<body>

  <!-- HEADER -->
  <header id="inicio">
    <div class="container">
      <div class="header-inner">
        <a href="#inicio" class="logo">TV</a>
        <nav class="menu-desktop">
          <ul>
            <li><a href="#sobre">Sobre</a></li>
            <li><a href="#sobre">Stack</a></li>
            <li><a href="#projetos">Projetos</a></li>
            <li><a href="#experiencia">Experiência</a></li>
          </ul>
        </nav>
        <a href="#formulario" class="btn-contato-header">CONTATO</a>
        <div class="btn-abrir-menu" id="btn-menu">
          <i class="bi bi-list"></i>
        </div>
      </div>
    </div>
    <!-- Mobile menu -->
    <div class="menu-mobile" id="menu-mobile">
      <div class="btn-fechar"><i class="bi bi-x-lg"></i></div>
      <nav>
        <ul>
          <li><a href="#inicio">Início</a></li>
          <li><a href="#sobre">Sobre</a></li>
          <li><a href="#projetos">Projetos</a></li>
          <li><a href="#experiencia">Experiência</a></li>
          <li><a href="#formulario">Contato</a></li>
        </ul>
      </nav>
    </div>
    <div class="overlay-menu" id="overlay-menu"></div>
  </header>

  <main>

    <!-- HERO -->
    <section class="hero">
      <div class="container">
        <div class="hero-content">
          <p class="hero-eyebrow">Full Stack · Mobile Developer</p>
          <h1 class="hero-headline">
            TRANSFORMANDO<br>
            <span>CÓDIGO</span><br>
            EM PRODUTO
          </h1>
          <p class="hero-sub">React · React Native · Node.js · TypeScript</p>
          <a href="#projetos" class="btn-hero">VER MEU TRABALHO ↓</a>
        </div>
      </div>
    </section>

    <!-- BENTO GRID (Sobre + Stack) -->
    <section class="bento" id="sobre">
      <div class="container">
        <div class="bento-grid">

          <!-- Stack cell — full width -->
          <div class="bento-cell bento-stack fade-up">
            <p class="bento-label">STACK</p>
            <div class="chips-row">
              <span class="chip hi">React</span>
              <span class="chip hi">React Native</span>
              <span class="chip hi">TypeScript</span>
              <span class="chip hi">Node.js</span>
              <span class="chip">Express</span>
              <span class="chip">PostgreSQL</span>
              <span class="chip">REST APIs</span>
            </div>
          </div>

          <!-- Sobre cell -->
          <div class="bento-cell bento-sobre fade-up">
            <p class="bento-label">SOBRE</p>
            <div class="sobre-inner">
              <img src="images/Tiago.jpg" alt="Tiago Vieira" class="sobre-photo" />
              <div class="sobre-text">
                <strong>Tiago Vieira</strong>
                <p>Dev Full Stack &amp; Mobile com +4 anos em React e React Native. Construo do banco ao app.</p>
                <div class="social-icons">
                  <a href="https://www.linkedin.com/in/tiagovieirapires/" target="_blank"><i class="bi bi-linkedin"></i></a>
                  <a href="https://github.com/TiagoVP86" target="_blank"><i class="bi bi-github"></i></a>
                  <a href="https://www.instagram.com/tiagovieira86/" target="_blank"><i class="bi bi-instagram"></i></a>
                </div>
              </div>
            </div>
          </div>

          <!-- Projeto destaque cell -->
          <div class="bento-cell bento-destaque fade-up">
            <p class="bento-label">PROJETO DESTAQUE</p>
            <a href="https://github.com/TiagoVP86/pizzaria" target="_blank" class="destaque-link">
              <img src="images/front.png" alt="Pizzaria App" class="destaque-img" />
              <span class="destaque-name">Pizzaria Full Stack ↗</span>
            </a>
          </div>

          <!-- Count cells -->
          <div class="bento-cell bento-count fade-up">
            <p class="bento-label">PROJETOS</p>
            <a href="#projetos" class="count-link">
              <span class="count-number">6</span>
              <span class="count-arrow">→</span>
            </a>
          </div>

          <div class="bento-cell bento-count fade-up">
            <p class="bento-label">ANOS DE EXPERIÊNCIA</p>
            <div class="count-link">
              <span class="count-number">+4</span>
            </div>
          </div>

        </div>
      </div>
    </section>

    <!-- PROJETOS -->
    <section class="projetos" id="projetos">
      <div class="container">
        <h2 class="section-title">MEU <span>TRABALHO.</span></h2>
        <div class="projetos-grid">

          <div class="projeto-card fade-up">
            <a href="https://fokus-brown-five.vercel.app/" target="_blank">
              <img src="images/fokus.png" alt="Fokus" class="projeto-img" />
            </a>
            <div class="projeto-body">
              <h3 class="projeto-nome">Fokus</h3>
              <p class="projeto-desc">Timer Pomodoro com foco e produtividade</p>
              <div class="projeto-chips">
                <span class="chip">JavaScript</span>
                <span class="chip">CSS</span>
              </div>
              <div class="projeto-links">
                <a href="https://fokus-brown-five.vercel.app/" target="_blank">Live ↗</a>
                <a href="https://github.com/TiagoVP86" target="_blank">GitHub</a>
              </div>
            </div>
          </div>

          <div class="projeto-card fade-up">
            <a href="https://meteora-gray-three.vercel.app/" target="_blank">
              <img src="images/meteora.png" alt="Meteora" class="projeto-img" />
            </a>
            <div class="projeto-body">
              <h3 class="projeto-nome">Meteora</h3>
              <p class="projeto-desc">E-commerce de moda com layout responsivo</p>
              <div class="projeto-chips">
                <span class="chip">Bootstrap</span>
                <span class="chip">HTML</span>
              </div>
              <div class="projeto-links">
                <a href="https://meteora-gray-three.vercel.app/" target="_blank">Live ↗</a>
                <a href="https://github.com/TiagoVP86" target="_blank">GitHub</a>
              </div>
            </div>
          </div>

          <div class="projeto-card fade-up">
            <a href="https://serenatto-indol-rho.vercel.app/" target="_blank">
              <img src="images/serenatto.png" alt="Serenatto" class="projeto-img" />
            </a>
            <div class="projeto-body">
              <h3 class="projeto-nome">Serenatto</h3>
              <p class="projeto-desc">Landing page para cafeteria artesanal</p>
              <div class="projeto-chips">
                <span class="chip">Bootstrap</span>
                <span class="chip">HTML</span>
              </div>
              <div class="projeto-links">
                <a href="https://serenatto-indol-rho.vercel.app/" target="_blank">Live ↗</a>
                <a href="https://github.com/TiagoVP86" target="_blank">GitHub</a>
              </div>
            </div>
          </div>

          <div class="projeto-card fade-up">
            <a href="https://github.com/TiagoVP86/pizzaria/tree/main/frontend" target="_blank">
              <img src="images/front.png" alt="Pizzaria Frontend" class="projeto-img" />
            </a>
            <div class="projeto-body">
              <h3 class="projeto-nome">Pizzaria — Frontend</h3>
              <p class="projeto-desc">Dashboard web para gestão de pedidos</p>
              <div class="projeto-chips">
                <span class="chip hi">React</span>
                <span class="chip hi">TypeScript</span>
              </div>
              <div class="projeto-links">
                <a href="https://github.com/TiagoVP86/pizzaria/tree/main/frontend" target="_blank">GitHub ↗</a>
              </div>
            </div>
          </div>

          <div class="projeto-card fade-up">
            <a href="https://github.com/TiagoVP86/pizzaria/tree/main/mobile" target="_blank">
              <img src="images/mobile.png" alt="Pizzaria Mobile" class="projeto-img" />
            </a>
            <div class="projeto-body">
              <h3 class="projeto-nome">Pizzaria — Mobile</h3>
              <p class="projeto-desc">App para garçons registrarem pedidos em tempo real</p>
              <div class="projeto-chips">
                <span class="chip hi">React Native</span>
                <span class="chip hi">TypeScript</span>
              </div>
              <div class="projeto-links">
                <a href="https://github.com/TiagoVP86/pizzaria/tree/main/mobile" target="_blank">GitHub ↗</a>
              </div>
            </div>
          </div>

          <div class="projeto-card fade-up">
            <a href="https://github.com/TiagoVP86/pizzaria/tree/main/backend" target="_blank">
              <img src="images/back.png" alt="Pizzaria Backend" class="projeto-img" />
            </a>
            <div class="projeto-body">
              <h3 class="projeto-nome">Pizzaria — Backend</h3>
              <p class="projeto-desc">API REST para pedidos, mesas e produtos</p>
              <div class="projeto-chips">
                <span class="chip hi">Node.js</span>
                <span class="chip">Express</span>
                <span class="chip">PostgreSQL</span>
              </div>
              <div class="projeto-links">
                <a href="https://github.com/TiagoVP86/pizzaria/tree/main/backend" target="_blank">GitHub ↗</a>
              </div>
            </div>
          </div>

        </div>
      </div>
    </section>

    <!-- EXPERIÊNCIA -->
    <section class="experiencia" id="experiencia">
      <div class="container">
        <h2 class="section-title"><span>EXPERIÊNCIA.</span></h2>
        <div class="timeline">

          <div class="timeline-item fade-up">
            <div class="timeline-dot"></div>
            <div class="timeline-content">
              <h3 class="tl-company">Empresa A <span class="tl-placeholder">[substituir]</span></h3>
              <p class="tl-period">2022 – presente · Dev Full Stack</p>
              <div class="tl-chips">
                <span class="chip hi">React</span>
                <span class="chip hi">Node.js</span>
                <span class="chip">PostgreSQL</span>
              </div>
            </div>
          </div>

          <div class="timeline-item fade-up">
            <div class="timeline-dot"></div>
            <div class="timeline-content">
              <h3 class="tl-company">Empresa B <span class="tl-placeholder">[substituir]</span></h3>
              <p class="tl-period">2020 – 2022 · Dev Mobile</p>
              <div class="tl-chips">
                <span class="chip hi">React Native</span>
                <span class="chip">TypeScript</span>
              </div>
            </div>
          </div>

        </div>
      </div>
    </section>

    <!-- CONTATO -->
    <section class="formulario" id="formulario">
      <div class="container">
        <h2 class="section-title">FALE <span>COMIGO.</span></h2>
        <form method="POST" action="https://formsubmit.co/devtiagovieira@gmail.com">
          <input type="hidden" name="_next" value="https://tiagovp86.github.io/portfolio/sucesso" />
          <input type="hidden" name="_captcha" value="false" />
          <input type="text" name="nome" placeholder="Seu nome completo" required />
          <input type="email" name="email" placeholder="Seu e-mail" required />
          <input type="tel" name="telefone" placeholder="Seu celular" />
          <textarea name="mensagem" placeholder="Sua mensagem" required></textarea>
          <button type="submit">ENVIAR</button>
        </form>
      </div>
    </section>

  </main>

  <!-- FOOTER -->
  <footer>
    <div class="container">
      <div class="footer-top">
        <a href="#inicio" class="logo">TV</a>
        <div class="social-icons">
          <a href="https://www.linkedin.com/in/tiagovieirapires/" target="_blank"><i class="bi bi-linkedin"></i></a>
          <a href="https://github.com/TiagoVP86" target="_blank"><i class="bi bi-github"></i></a>
          <a href="https://www.instagram.com/tiagovieira86/" target="_blank"><i class="bi bi-instagram"></i></a>
        </div>
      </div>
      <div class="footer-bottom">
        <a href="mailto:devtiagovieira@gmail.com">devtiagovieira@gmail.com</a>
      </div>
    </div>
  </footer>

  <!-- Scroll animation -->
  <script>
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible');
        }
      });
    }, { threshold: 0.1 });

    document.querySelectorAll('.fade-up').forEach(el => observer.observe(el));
  </script>

</body>
</html>
```

- [ ] **Step 2: Open index.html in browser and verify structure loads**

Open `index.html` with Live Server (port 5501) or directly in browser. Expected: page renders with Space Grotesk font, dark background, all sections present, no console errors.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: HTML skeleton with all 7 sections"
```

---

## Task 3: Header styles

**Files:**
- Modify: `style.css` — append header section

- [ ] **Step 1: Append header styles to style.css**

Add to the end of `style.css`:

```css
/* =============================================
   HEADER
   ============================================= */
header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
  padding: 20px 0;
  background: transparent;
  transition: background 0.3s ease;
}

header.scrolled {
  background: var(--bg);
  border-bottom: 1px solid var(--border);
}

.header-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.logo {
  font-size: 22px;
  font-weight: 900;
  letter-spacing: -1px;
  color: var(--text);
}

.menu-desktop ul {
  display: flex;
  gap: 36px;
}

.menu-desktop a {
  color: var(--muted);
  font-size: 13px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  transition: color 0.2s;
}

.menu-desktop a:hover {
  color: var(--text);
}

.btn-contato-header {
  background: var(--accent);
  color: #000;
  font-size: 11px;
  font-weight: 900;
  letter-spacing: 2px;
  padding: 8px 18px;
  border-radius: 2px;
  transition: opacity 0.2s;
}

.btn-contato-header:hover {
  opacity: 0.85;
}

.btn-abrir-menu {
  display: none;
  cursor: pointer;
}

.btn-abrir-menu i {
  color: var(--accent);
  font-size: 32px;
}

/* Mobile menu */
.menu-mobile {
  background: var(--bg);
  height: 100vh;
  position: fixed;
  top: 0;
  right: 0;
  z-index: 99999;
  width: 0;
  overflow: hidden;
  transition: width 0.4s ease;
  border-left: 1px solid var(--border);
}

.menu-mobile.abrir-menu {
  width: 70%;
}

.menu-mobile.abrir-menu ~ .overlay-menu {
  display: block;
}

.menu-mobile nav ul {
  text-align: right;
  padding-top: 20px;
}

.menu-mobile nav ul li a {
  color: var(--text);
  font-size: 18px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  padding: 16px 8%;
  display: block;
  transition: color 0.2s;
}

.menu-mobile nav ul li a:hover {
  color: var(--accent);
}

.menu-mobile .btn-fechar {
  padding: 20px 8%;
  text-align: right;
}

.menu-mobile .btn-fechar i {
  color: var(--accent);
  font-size: 28px;
  cursor: pointer;
}

.overlay-menu {
  background: rgba(0,0,0,0.85);
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 88888;
  display: none;
}
```

- [ ] **Step 2: Add scrolled class script — append to the inline script in index.html**

Find the `<script>` block at the bottom of `index.html` and add inside it, after the observer code:

```js
// Header scroll effect
window.addEventListener('scroll', () => {
  const header = document.querySelector('header');
  header.classList.toggle('scrolled', window.scrollY > 40);
});
```

- [ ] **Step 3: Verify in browser**

Expected: header is transparent at top, gains dark background on scroll. Nav links visible in desktop. Hamburger hidden on desktop.

- [ ] **Step 4: Commit**

```bash
git add style.css index.html
git commit -m "feat: header styles with scroll effect and mobile menu"
```

---

## Task 4: Hero section styles

**Files:**
- Modify: `style.css` — append hero section

- [ ] **Step 1: Append hero styles to style.css**

```css
/* =============================================
   HERO
   ============================================= */
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--bg);
  padding: 120px 0 80px;
}

.hero-content {
  text-align: center;
  max-width: 800px;
  margin: 0 auto;
}

.hero-eyebrow {
  color: var(--muted);
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 4px;
  text-transform: uppercase;
  margin-bottom: 24px;
}

.hero-headline {
  font-size: clamp(52px, 9vw, 96px);
  font-weight: 900;
  letter-spacing: -3px;
  line-height: 0.9;
  text-transform: uppercase;
  color: var(--text);
  margin-bottom: 28px;
}

.hero-headline span {
  color: var(--accent);
}

.hero-sub {
  color: var(--muted);
  font-size: 14px;
  letter-spacing: 2px;
  margin-bottom: 40px;
}

.btn-hero {
  display: inline-block;
  border: 1px solid var(--accent);
  color: var(--accent);
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 3px;
  text-transform: uppercase;
  padding: 14px 32px;
  border-radius: 2px;
  transition: background 0.2s, color 0.2s;
}

.btn-hero:hover {
  background: var(--accent);
  color: #000;
}
```

- [ ] **Step 2: Verify in browser**

Expected: full-viewport dark hero with giant uppercase headline, "CÓDIGO" in orange, outline CTA button, eyebrow text above, stack text below.

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "feat: hero section styles"
```

---

## Task 5: Bento Grid styles

**Files:**
- Modify: `style.css` — append bento section

- [ ] **Step 1: Append bento styles to style.css**

```css
/* =============================================
   BENTO GRID
   ============================================= */
.bento {
  background: var(--bg-2);
  padding: 100px 0;
}

.bento-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: auto;
  gap: 12px;
}

.bento-cell {
  background: var(--bg-cell);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 28px;
  transition: border-color 0.2s;
}

.bento-cell:hover {
  border-color: #333;
}

.bento-label {
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 3px;
  color: var(--muted);
  text-transform: uppercase;
  margin-bottom: 16px;
}

/* Stack cell — spans 2 columns */
.bento-stack {
  grid-column: span 2;
}

.chips-row {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

/* Sobre cell */
.sobre-inner {
  display: flex;
  gap: 16px;
  align-items: flex-start;
}

.sobre-photo {
  width: 72px;
  height: 90px;
  object-fit: cover;
  border-radius: 3px;
  flex-shrink: 0;
  border: 1px solid var(--border);
}

.sobre-text strong {
  display: block;
  font-size: 15px;
  font-weight: 700;
  color: var(--text);
  margin-bottom: 6px;
}

.sobre-text p {
  font-size: 13px;
  color: var(--muted);
  line-height: 1.5;
  margin-bottom: 14px;
}

/* Social icons — used in bento sobre and footer */
.social-icons {
  display: flex;
  gap: 10px;
}

.social-icons a {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 32px;
  height: 32px;
  background: var(--accent);
  color: #000;
  border-radius: 50%;
  font-size: 14px;
  transition: opacity 0.2s;
}

.social-icons a:hover {
  opacity: 0.8;
}

/* Destaque cell */
.destaque-link {
  display: block;
}

.destaque-img {
  width: 100%;
  height: 140px;
  object-fit: cover;
  border-radius: 3px;
  border: 1px solid var(--border);
  margin-bottom: 10px;
  transition: opacity 0.2s;
}

.destaque-link:hover .destaque-img {
  opacity: 0.8;
}

.destaque-name {
  font-size: 13px;
  font-weight: 700;
  color: var(--accent);
}

/* Count cells */
.count-link {
  display: flex;
  align-items: baseline;
  gap: 8px;
}

.count-number {
  font-size: clamp(48px, 6vw, 72px);
  font-weight: 900;
  letter-spacing: -3px;
  color: var(--text);
  line-height: 1;
}

.count-arrow {
  font-size: 28px;
  color: var(--accent);
}

a.count-link:hover .count-number {
  color: var(--accent);
}
```

- [ ] **Step 2: Verify in browser**

Expected: dark bento grid with 2 columns. Top row: stack chips spanning full width. Below: sobre (photo + bio + social icons) and destaque side by side. Below that: two count cells with large numbers.

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "feat: bento grid styles"
```

---

## Task 6: Projetos section styles

**Files:**
- Modify: `style.css` — append projetos section

- [ ] **Step 1: Append projetos styles to style.css**

```css
/* =============================================
   PROJETOS
   ============================================= */
.projetos {
  background: var(--bg);
  padding: 100px 0;
}

.projetos-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}

.projeto-card {
  background: var(--bg-cell);
  border: 1px solid var(--border);
  border-radius: 4px;
  overflow: hidden;
  transition: transform 0.2s, border-color 0.2s;
}

.projeto-card:hover {
  transform: translateY(-3px);
  border-color: var(--accent);
}

.projeto-img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  display: block;
  border-bottom: 1px solid var(--border);
}

.projeto-body {
  padding: 20px;
}

.projeto-nome {
  font-size: 16px;
  font-weight: 700;
  color: var(--text);
  margin-bottom: 6px;
}

.projeto-desc {
  font-size: 13px;
  color: var(--muted);
  margin-bottom: 12px;
  line-height: 1.4;
}

.projeto-chips {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-bottom: 14px;
}

.projeto-links {
  display: flex;
  gap: 16px;
}

.projeto-links a {
  font-size: 12px;
  font-weight: 700;
  color: var(--accent);
  letter-spacing: 1px;
  text-transform: uppercase;
  transition: opacity 0.2s;
}

.projeto-links a:hover {
  opacity: 0.7;
}
```

- [ ] **Step 2: Verify in browser**

Expected: 3-column grid of project cards. Each card has screenshot, name, 1-line desc, chip tags, and orange links. Hover lifts card and turns border orange.

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "feat: projetos grid styles"
```

---

## Task 7: Experiência timeline styles

**Files:**
- Modify: `style.css` — append experiencia section

- [ ] **Step 1: Append experiencia styles to style.css**

```css
/* =============================================
   EXPERIÊNCIA
   ============================================= */
.experiencia {
  background: var(--bg-2);
  padding: 100px 0;
}

.timeline {
  position: relative;
  padding-left: 32px;
  max-width: 640px;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 6px;
  top: 8px;
  bottom: 8px;
  width: 2px;
  background: var(--accent);
  opacity: 0.3;
}

.timeline-item {
  position: relative;
  margin-bottom: 48px;
}

.timeline-item:last-child {
  margin-bottom: 0;
}

.timeline-dot {
  position: absolute;
  left: -29px;
  top: 6px;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: var(--accent);
}

.tl-company {
  font-size: 18px;
  font-weight: 700;
  color: var(--text);
  margin-bottom: 4px;
}

.tl-placeholder {
  font-size: 12px;
  color: var(--muted);
  font-weight: 400;
}

.tl-period {
  font-size: 13px;
  color: var(--accent);
  letter-spacing: 1px;
  margin-bottom: 12px;
}

.tl-chips {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}
```

- [ ] **Step 2: Verify in browser**

Expected: vertical orange timeline line on the left, two items with company name, orange period, and tech chips.

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "feat: experiencia timeline styles"
```

---

## Task 8: Contato + Footer styles

**Files:**
- Modify: `style.css` — append contact and footer sections

- [ ] **Step 1: Append contact styles to style.css**

```css
/* =============================================
   CONTATO
   ============================================= */
.formulario {
  background: var(--bg);
  padding: 100px 0;
}

.formulario form {
  max-width: 480px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.formulario input,
.formulario textarea {
  width: 100%;
  background: var(--bg-2);
  border: 1px solid var(--border);
  border-radius: 2px;
  outline: none;
  padding: 16px;
  color: var(--text);
  font-family: 'Space Grotesk', sans-serif;
  font-size: 14px;
  transition: border-color 0.2s;
}

.formulario input:focus,
.formulario textarea:focus {
  border-color: var(--accent);
}

.formulario textarea {
  resize: none;
  height: 180px;
}

.formulario button[type="submit"] {
  width: 100%;
  background: var(--accent);
  color: #000;
  border: none;
  border-radius: 2px;
  padding: 16px;
  font-family: 'Space Grotesk', sans-serif;
  font-size: 13px;
  font-weight: 900;
  letter-spacing: 3px;
  text-transform: uppercase;
  cursor: pointer;
  transition: opacity 0.2s;
  margin-top: 8px;
}

.formulario button[type="submit"]:hover {
  opacity: 0.85;
}

/* =============================================
   FOOTER
   ============================================= */
footer {
  background: var(--bg-2);
  padding: 32px 0;
  border-top: 1px solid var(--accent);
}

.footer-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 20px;
  margin-bottom: 20px;
  border-bottom: 1px solid var(--border);
}

.footer-bottom {
  text-align: center;
}

.footer-bottom a {
  color: var(--muted);
  font-size: 13px;
  transition: color 0.2s;
}

.footer-bottom a:hover {
  color: var(--text);
}
```

- [ ] **Step 2: Verify in browser**

Expected: dark form with orange focus borders, full-width orange submit button. Footer with TV logo left, social icons right, email centered below divider.

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "feat: contato form and footer styles"
```

---

## Task 9: Responsive styles

**Files:**
- Modify: `style.css` — append media queries

- [ ] **Step 1: Append media queries to style.css**

```css
/* =============================================
   RESPONSIVENESS
   ============================================= */

/* Tablet: 768px–1020px */
@media screen and (max-width: 1020px) {
  .menu-desktop,
  .btn-contato-header {
    display: none;
  }

  .btn-abrir-menu {
    display: block;
  }

  .projetos-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Mobile: < 768px */
@media screen and (max-width: 768px) {
  .hero-headline {
    letter-spacing: -2px;
  }

  .bento-grid {
    grid-template-columns: 1fr;
  }

  .bento-stack {
    grid-column: span 1;
  }

  .projetos-grid {
    grid-template-columns: 1fr;
  }

  .section-title {
    font-size: 28px;
  }

  .timeline {
    max-width: 100%;
  }

  .footer-top {
    flex-direction: column;
    gap: 20px;
    text-align: center;
  }
}
```

- [ ] **Step 2: Verify responsiveness**

Resize browser to 768px and then to 375px. Expected:
- 768px: single column bento, single column projects, hamburger menu visible
- 375px: hero headline still legible, all sections stack correctly, no horizontal scroll

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "feat: responsive styles for tablet and mobile"
```

---

## Task 10: Update sucesso.html

**Files:**
- Modify: `sucesso.html`

- [ ] **Step 1: Read current sucesso.html**

Read the file to understand its current structure before replacing.

- [ ] **Step 2: Rewrite sucesso.html to match new palette**

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;700;900&display=swap" rel="stylesheet" />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css" />
  <link rel="stylesheet" href="style.css" />
  <title>Mensagem enviada — Tiago Vieira</title>
  <style>
    .sucesso-page {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
      padding: 40px;
    }
    .sucesso-icon {
      font-size: 56px;
      color: var(--accent);
      margin-bottom: 24px;
    }
    .sucesso-title {
      font-size: 32px;
      font-weight: 900;
      letter-spacing: -1px;
      text-transform: uppercase;
      margin-bottom: 12px;
    }
    .sucesso-sub {
      color: var(--muted);
      font-size: 15px;
      margin-bottom: 36px;
    }
    .sucesso-btn {
      display: inline-block;
      background: var(--accent);
      color: #000;
      font-size: 12px;
      font-weight: 900;
      letter-spacing: 3px;
      text-transform: uppercase;
      padding: 14px 28px;
      border-radius: 2px;
      transition: opacity 0.2s;
    }
    .sucesso-btn:hover { opacity: 0.85; }
  </style>
</head>
<body>
  <div class="sucesso-page">
    <div class="sucesso-icon"><i class="bi bi-check-circle"></i></div>
    <h1 class="sucesso-title">Mensagem <span style="color:var(--accent)">enviada!</span></h1>
    <p class="sucesso-sub">Obrigado pelo contato. Responderei em breve.</p>
    <a href="https://tiagovp86.github.io/portfolio/" class="sucesso-btn">← VOLTAR AO PORTFÓLIO</a>
  </div>
</body>
</html>
```

- [ ] **Step 3: Commit**

```bash
git add sucesso.html
git commit -m "feat: update sucesso.html to match new palette"
```

---

## Task 11: Final review and cleanup

**Files:**
- Review: `index.html`, `style.css`

- [ ] **Step 1: Open at desktop width (1280px)**

Verify all 7 sections render correctly: header (sticky on scroll), hero (full viewport), bento grid (2 cols), projetos (3 cols), experiência (timeline), contato (form), footer.

- [ ] **Step 2: Open at mobile width (375px)**

Verify: hamburger menu works (opens/closes), all sections single column, no horizontal scroll, form usable.

- [ ] **Step 3: Update timeline with real data**

In `index.html`, find `.tl-placeholder` spans and replace company names and dates with real data. Remove `.tl-placeholder` spans once filled in.

- [ ] **Step 4: Final commit**

```bash
git add index.html style.css sucesso.html
git commit -m "feat: complete portfolio redesign — Dark Editorial"
```
