# PTE Academic Study Tools

Interactive tools for PTE Academic exam preparation. Built with vanilla HTML, CSS, and JavaScript — no frameworks, no login required.

---

## Files

| File | Description |
|------|-------------|
| `index.html` | Landing page with navigation to all tools |
| `pronunciacion_master.html` | Read Aloud pronunciation trainer |
| `perfect_tenses_master.html` | Perfect tenses grammar trainer |
| `styles.css` | **Shared stylesheet — single source of truth for all styles** |

---

## 🎨 Design System (`styles.css`)

All tools **must** link to `styles.css` and follow this design system. Never write standalone styles that duplicate what's already in `styles.css`.

### Linking the stylesheet
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
<link rel="stylesheet" href="styles.css">
```

### Color Palette

```css
/* Backgrounds (dark, layered) */
--bg:  #08081a   /* page background */
--bg2: #0f0f24   /* sidebar, cards */
--bg3: #13132e   /* nested surfaces */

/* Surfaces (overlay on dark bg) */
--s1: rgba(255,255,255,0.04)   /* card base */
--s2: rgba(255,255,255,0.07)   /* card hover */
--s3: rgba(255,255,255,0.11)   /* active/pressed */

/* Borders */
--b1: rgba(255,255,255,0.08)   /* default border */
--b2: rgba(255,255,255,0.16)   /* hover border */

/* Text */
--t1: #e2e8f0   /* primary text */
--t2: #94a3b8   /* secondary text */
--t3: #64748b   /* muted/labels */

/* Semantic */
--ok:   #10b981   /* correct / success */
--err:  #f43f5e   /* error / wrong */
--warn: #f59e0b   /* warning / hint */

/* Accent colors (use for tool identity) */
--purple: #7c3aed   /* grammar tools */
--blue:   #2563eb   /* reading/speaking */
--cyan:   #0891b2   /* pronunciation */
--pink:   #db2777   /* endings */
--green:  #059669   /* linking words */
--amber:  #d97706   /* stress/rhythm */
--indigo: #4f46e5   /* PTE practice */
```

### Typography
- **Font family:** `Inter` (UI) + `JetBrains Mono` (phonetics, code)
- Titles: `font-weight: 900`, gradient text via `-webkit-background-clip: text`
- Body: `font-weight: 400–500`
- Labels: `font-size: 10–11px`, `text-transform: uppercase`, `letter-spacing: .1em`

---

## 🏗️ Layout Structure

Every tool **must** follow this layout:

```html
<body>
  <button class="mob-btn" id="menuBtn" onclick="toggleSidebar()">☰</button>

  <aside class="sidebar" id="sidebar">
    <div class="sb-logo">
      <a href="index.html"><h1>Tool Name</h1></a>
      <p>Short description</p>
    </div>
    <a href="index.html" class="sb-home">← All Tools</a>
    <nav class="sb-nav">
      <div class="nav-lbl">Section Label</div>
      <a class="nav-item active" href="#section" style="--ac:#7c3aed">
        <span class="nav-icon">🔤</span>
        <span class="nav-title">Section Name</span>
        <span class="nav-ck" id="ck-section"></span>
      </a>
    </nav>
    <div class="sb-prog">
      <div class="sb-prog-row"><span>Progress</span><span id="pct">0%</span></div>
      <div class="pbar"><div class="pbar-fill" id="pbar" style="width:0%"></div></div>
    </div>
  </aside>

  <main class="main">
    <section class="hero">
      <div class="hero-badge">🎯 PTE Academic — Category</div>
      <h1>Tool Title<br><span>Subtitle</span></h1>
      <p>Description...</p>
      <div class="hero-stats">
        <div class="hstat">
          <span class="hstat-icon">📚</span>
          <div><div class="hstat-val">7</div><div class="hstat-lbl">Label</div></div>
        </div>
      </div>
    </section>
    <section class="sec" id="section-id">
      <!-- content -->
    </section>
  </main>
</body>
```

```js
function toggleSidebar() {
  document.getElementById('sidebar').classList.toggle('open');
}
```

---

## 📦 Component Reference

### Cards
```html
<div class="card">Generic card</div>
<div class="ra-card">Content card with hover</div>
<div class="q-card">Question card (animated entry)</div>
```

### Tip / Alert boxes
```html
<div class="tip rule">
  <span class="tip-icon">📌</span>
  <div class="tip-body"><div class="tip-lbl">Rule</div><strong>Key point</strong> — explanation</div>
</div>
<!-- Variants: tip.rule (purple) | tip.es (red) | tip.info (amber) | tip.ok (green) -->
```

### Buttons
```html
<button class="quiz-btn primary">Start Quiz</button>   <!-- purple gradient -->
<button class="quiz-btn success">Complete</button>     <!-- green gradient -->
<button class="btn-sp">🔊 Listen</button>              <!-- small audio button -->
<button class="icon-btn">✕</button>                   <!-- icon only -->
```

### Badges
```html
<span class="badge-pill" style="background:rgba(124,58,237,.14);color:#a78bfa;">Label</span>
<span class="diff easy">Easy</span>
<span class="diff med">Medium</span>
<span class="diff hard">Hard</span>
```

### Quiz / Multiple Choice
```html
<div class="q-opts">
  <button class="q-opt" onclick="check(0)">
    <span class="opt-ltr">A</span> Option text
  </button>
</div>
<!-- After answer: add class "ok" (correct) or "no" (wrong) -->
```

### Feedback Panel
```html
<div class="fb-panel show">
  <div class="fb-panel-hdr ok">✅ Correct! +10 XP</div>
  <div class="fb-panel-body">
    <div class="fb-answer-box">✏️ Correct answer: ...</div>
    <div class="fb-rule">📖 <strong>Rule:</strong> ...</div>
    <div class="fb-expl">💡 <strong>Explanation:</strong> ...</div>
    <div class="fb-examples"><p>• Example</p></div>
  </div>
</div>
<!-- Header variants: ok | no | hint -->
```

### Form Inputs
```html
<input class="tool-input" type="text" placeholder="Type here...">
<textarea class="tool-textarea" rows="3"></textarea>
<!-- After validation: add class "ok" or "no" -->
```

### Source / Error boxes
```html
<div class="src-box">Source sentence for transform exercise</div>
<div class="err-box">Sentence with an error to correct</div>
```

### Modal
```html
<div class="overlay" id="overlay">
  <div class="modal">
    <div class="modal-hdr">
      <div class="modal-ttl">Title</div>
      <button class="icon-btn" onclick="closeModal()">✕</button>
    </div>
    <div class="modal-body">Content</div>
  </div>
</div>
```
```js
document.getElementById('overlay').classList.toggle('open');
```

### Toast
```html
<div class="toast" id="toast"><span>🎉</span><span id="toast-txt">Message</span></div>
```
```js
function showToast(msg) {
  document.getElementById('toast-txt').textContent = msg;
  const t = document.getElementById('toast');
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 3000);
}
```

---

## 🛠️ Creating a New Tool — Checklist

1. Copy `perfect_tenses_master.html` as a starting template
2. Link `styles.css` and Google Fonts (same `<link>` tags)
3. Set a unique accent color: `style="--ac:#your-color"` on nav items
4. Add a card in `index.html` pointing to the new file
5. Keep tool-specific styles in a `<style>` block in the tool's own `<head>`
6. Never override the CSS variables — extend, don't replace

- [ ] Links `styles.css` and Google Fonts
- [ ] Has `.sb-logo` with link to `index.html`
- [ ] Has `.sb-home` back link
- [ ] Has `.hero` section with stats
- [ ] `toggleSidebar()` function implemented
- [ ] Uses `--ac` for nav item accent color
- [ ] Card added to `index.html`

---

## GitHub Pages

🌐 **Live site:** [https://gapolaniadev.github.io/english_class/](https://gapolaniadev.github.io/english_class/)

Repository: `https://github.com/GapolaniaDev/english_class`

`index.html` at the root is the entry point. Every new tool pushed to `main` is automatically deployed.
