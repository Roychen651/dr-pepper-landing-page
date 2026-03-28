# Dr Pepper — Immersive Landing Page

> **Educational & Portfolio Project** — Not affiliated with Keurig Dr Pepper Inc.

A premium, Awwwards-level product landing page built as a front-end portfolio piece. Combines scroll-driven canvas animation, 3 flavor variants, and a native-feel mobile experience.

---

## Live Demo

**[roychen651.github.io/dr-pepper-landing-page](https://roychen651.github.io/dr-pepper-landing-page)**
*(or your Vercel URL once deployed)*

---

## Features

### Scroll-Driven Canvas Animation
- **625 WebP frames** across 3 flavor variants (Regular 220 · Cherry 203 · Blackberry 202)
- Frame sequences rendered on HTML5 Canvas with `requestAnimationFrame`
- Cover-fit draw math keeps the can centered and full-bleed at any viewport size
- HiDPI / Retina support — canvas renders at `devicePixelRatio × 2.5` on mobile for crisp pixels

### 3 Flavor Variants
| Variant | Frames | Accent Color |
|---------|--------|-------------|
| Regular | 220 | `#711F25` deep burgundy |
| Cherry | 203 | `#CC0000` vivid red |
| Blackberry | 202 | `#4a1d82` dark violet |

Color theme, typography accent, and section copy all update live when switching flavors.

### Mobile-First UX (iOS/Android native feel)
- `100dvh` sizing — no layout jump when browser chrome shows/hides
- Native scroll on mobile (Lenis disabled) — zero friction against iOS momentum
- **Swipe left/right** anywhere on the hero to switch flavors
- First-visit **onboarding sheet** slides up from the bottom showing all 3 flavors
- Persistent **flavor peek strips** on left/right viewport edges — always hints there's more to swipe to
- Bottom thumb-zone flavor bar — critical interactions reachable with one thumb
- Early loader exit at 30% on mobile (remaining frames load in background)

### Desktop Experience
- **Lenis 1.1.14** smooth scroll with custom friction tuning
- GSAP 3.12.2 + ScrollTrigger for section reveals, counter animations, parallax
- Magnetic button effect — buttons subtly attract the cursor
- Custom CSS cursor — 8px dot + 40px lerp ring with `mix-blend-mode: difference`
- 3D tilt on cards — `perspective(900px)` rotateX/Y on mousemove
- Particle constellation background — 52 nodes, connecting lines, mouse repulsion

### Visual Design
- **Syne** display typeface (headings) + **Inter** body — loaded via Google Fonts
- Shimmer gradient on headings — white → accent → white animated loop
- Film grain overlay — SVG `feTurbulence` at 3.2% opacity
- Scroll progress bar (custom scrollbar track)
- Glassmorphism cards — `backdrop-filter: blur` + layered box-shadow

### Sound
- Can-opening sound plays on first real user gesture (click, tap, key)
- Uses `<audio>` element with capture-phase event listeners
- Respects browser autoplay policy — retries on next gesture if blocked

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Markup | Vanilla HTML5 (single file) |
| Styles | Vanilla CSS — custom properties, `clamp()`, `dvh`, media queries |
| Animation | GSAP 3.12.2 + ScrollTrigger, Lenis 1.1.14, Web Animations API |
| Canvas | HTML5 Canvas 2D — custom cover-fit, DPR scaling |
| Fonts | Google Fonts — Syne + Inter |
| Build | None — zero build step, zero dependencies to install |

---

## Project Structure

```
dr_pepper_landing_page/
├── index.html                        ← entire application (~2 400 lines)
├── regular_dr_pepper_frames/         ← 220 WebP frames (Regular variant)
│   ├── frame_000_delay-0.04s.webp
│   └── …
├── dr_pepper_cherry_frames/          ← 203 WebP frames (Cherry variant)
├── blackberry_dr_pepper_frames/      ← 202 WebP frames (Blackberry variant)
├── dr_pepper_start.png               ← poster / loader image (Regular)
├── cherry_start.png                  ← poster / loader image (Cherry)
├── black_berry_start.png             ← poster / loader image (Blackberry)
└── freesound_community-opening-soda-can-85366.mp3  ← can-open SFX
```

---

## Running Locally

No build step required — just serve the folder over HTTP (Canvas + Audio need a server origin):

```bash
# Python 3
python3 -m http.server 8080

# Node (npx)
npx serve .

# VS Code
# Install "Live Server" extension → right-click index.html → Open with Live Server
```

Then open `http://localhost:8080` in your browser.

---

## Deployment

### Vercel (recommended)
1. Push this repo to GitHub (already done)
2. Go to [vercel.com](https://vercel.com) → **Add New Project**
3. Import `dr-pepper-landing-page` from GitHub
4. Framework: **Other** (no framework)
5. Root directory: `/` (default)
6. Click **Deploy** — done in ~30 seconds

### GitHub Pages
```bash
# In repo Settings → Pages → Source: Deploy from branch → main → / (root)
```

---

## Performance Notes

- WebP frames are pre-decoded by the browser via `new Image()` preloading
- On mobile, frames 1–66 (30%) load before the loader hides — enough for the first scroll segment
- Remaining frames (67–220) continue loading in the background
- Canvas DPR capped at `2.5×` — balances sharpness vs. memory on high-DPR devices
- RAF loop always runs (never idles) — guarantees zero-latency canvas updates
- Particle canvas is disabled on mobile to preserve battery and prevent heat

---

## Disclaimer

> This website was created **solely for educational and portfolio purposes**. It is not affiliated with, endorsed by, or connected to Keurig Dr Pepper Inc. in any way. All Dr Pepper branding, trademarks, and product names are the property of their respective owners. No commercial use is intended. Content is presented under fair use for educational demonstration.

---

## Author

**Roy Chen** — [github.com/Roychen651](https://github.com/Roychen651)
