# DS BÜREAU — Hero Section (Concept 2)

A responsive hero section for the DS BÜREAU landing page, featuring an interactive ASCII-rendered 3D cube as the hero visual.

🔗 **Live preview:** [hellbent86.github.io/ds-hero-section](https://hellbent86.github.io/ds-hero-section)

---

## Overview

Designed from a Figma concept (Concept 2) and implemented as a single self-contained HTML file. Combines a dark editorial layout with a real-time interactive 3D element rendered entirely in ASCII characters. No build step required — opens directly in any modern browser.

---

## File Structure

```
ds-hero-section/
├── index.html   # Complete hero section — markup, styles, scripts
└── README.md    # This file
```

---

## Components

### Navigation
- Transparent flat nav, max-width 1440px, 120px horizontal padding
- **Logo:** Inline SVG — the DS BÜREAU mark in `#6673FF`
- **Links:** Services, Projects, Principles, Awards — uppercase, IBM Plex Sans
- **CTA:** "Say Hello!" — semi-transparent blue fill, `#6673FF` border, 8px radius
- **Mobile (<=900px):** Links collapse to a fullscreen drawer overlay via hamburger toggle

### Hero Layout
- CSS Grid: `3fr 2fr` (60% text / 40% cube) on desktop
- Single column on tablet/mobile (<=900px), cube stacks **below** the text
- `min-height: calc(100vh - 100px)` — fills the viewport on desktop
- Max-width 1440px, centered

### Background Glow
- Radial gradient orb: `rgba(65,78,217,0.28)` to transparent
- 600×600px, anchored to the left edge, vertically centered
- Decorative only — `pointer-events: none`

### Hero Copy

| Element | Details |
|---|---|
| **Badge pill** | "WHO WE ARE" — 12px uppercase IBM Plex Sans, `rgba(77,91,255,0.6)` border, pulsing blue dot |
| **Headline** | "Our team delivers impactful solutions" — Alexandria Medium, `clamp(36px, 3.75vw, 54px)` |
| **Body copy** | Alexandria Light 300, `clamp(14px, 1.1vw, 16px)`, `#d9d9d9` |
| **Primary CTA** | "START A PROJECT" — blue fill + `#6673FF` border, 8px radius, 44px height |
| **Secondary CTA** | "LEARN MORE" — transparent, grey border, arrow shifts on hover |

### Headline Glitch Animation

Two-phase effect triggered on load and repeating every 8 seconds:

1. **Scramble phase** (~1s) — all characters rapidly cycle through `DS$#@&%!?|/[]{}01<>` in `#5b69ff`
2. **Resolve phase** — characters snap back left-to-right with 60ms stagger, flickering `#98a4ff` before settling
3. A `skewX` CSS animation fires simultaneously for a corrupted-signal feel

### ASCII 3D Cube

A Three.js scene rendered to a hidden offscreen canvas, sampled pixel-by-pixel and redrawn as ASCII characters on a visible 2D canvas.

**3D scene:**
- `BoxGeometry(2,2,2)` — dark Phong-shaded cube body (`#111111`)
- 6 faces with extruded SVG logos (`ExtrudeGeometry`, depth 0.12, bevelled edges)
- Face pattern: **D** on front/back/bottom — **S** on left/right/top
- `PerspectiveCamera(52°)` at `(2.53, 2.07, 2.53)` looking at origin
- 3 lights: key (white 1.5), fill (blue-white 0.5), ambient (white 0.7)
- Auto-rotation: `0.008 rad/frame` on Y axis
- Drag to rotate (mouse + touch), resize-aware

**ASCII rendering:**
- Grid resolution: `floor(width / 110)` font-size, 0.6:1 character aspect ratio
- 46-character brightness ramp: sparse punctuation → strokes → fills → **S** → **D**
- Dark symbols: `rgba(91, 105, 255, a)` — `#5B69FF`
- Bright symbols: `rgba(152, 164, 255, a)` — `#98A4FF`
- Alpha scales with pixel brightness for natural shading falloff

**SVG assets (inlined):**
- `d-side.svg` — concentric D letterform, 211×211
- `s-side.svg` — concentric S letterform, 208×211

---

## Fonts

| Font | Weights | Used for |
|---|---|---|
| Alexandria | 300, 400, 500 | Headline, body copy |
| IBM Plex Sans | 300, 400, 500 | Nav, buttons, badge |

---

## Dependencies

| Library | Version | Purpose |
|---|---|---|
| Three.js | r128 | 3D scene rendering |
| Three.js SVGLoader | r128 | Parsing SVG paths into extruded 3D geometry |

---

## Breakpoints

| Breakpoint | Behaviour |
|---|---|
| > 1024px | Full layout, 120px horizontal padding |
| <= 1024px | Reduced padding (48px) |
| <= 900px | Single column, cube below text, hamburger nav |
| <= 540px | Smaller button font sizes (13px) |

---

## Colour Palette

| Token | Value | Use |
|---|---|---|
| `--bg` | `#050508` | Page background |
| `--accent` | `#414ed9` | Accent base |
| `--accent-border` | `#6673ff` | Button and logo colour |
| `--accent-bg` | `rgba(65,78,217,0.4)` | Button fill |
| `--text-1` | `#e5e5e5` | Primary text |
| `--text-2` | `#999` | Nav link colour |
| `--border` | `#666` | Secondary button border |
| `--pill-border` | `rgba(77,91,255,0.6)` | Badge border |
| ASCII dark | `#5B69FF` | Shadow/mid ASCII symbols |
| ASCII light | `#98A4FF` | Highlight ASCII symbols |

---

## GitHub Pages Setup

1. Go to **Settings > Pages** in this repo
2. Set source to **Deploy from a branch**
3. Select branch `main`, folder `/ (root)`
4. Save — the page will be live at `https://hellbent86.github.io/ds-hero-section`
