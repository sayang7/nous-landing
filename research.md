# Nous Landing Page — Research Notes

## Phase 1: Dark Landing Page Design Analysis

### What Makes Award-Winning Dark Pages Work

**Typography Scale**
- Oversized display type (100px–200px) creates instant hierarchy
- Tight tracking on display fonts (letter-spacing: -0.02em to -0.05em) reads as intentional
- High contrast between display weight and body weight — never use medium for both
- Cinzel/serif for classical gravitas, geometric mono for tech authority
- Line-height of 1.0–1.1 on hero headings; 1.6–1.7 on body

**Spacing Rhythm**
- 8-point grid base; sections breathe at 120px–160px padding
- Section transitions use negative margins or overlapping elements to avoid "stacked card" feel
- Max-width containers (~1280px) with asymmetric padding create editorial feel
- Generous whitespace inside cards; never let text touch the border

**Color Technique**
- Primary: near-black canvas (#04030a range) — not pure black, which reads flat on OLED
- Accent colors used sparingly (max 10% of any viewport)
- Subtle noise/grain texture on background surfaces adds tactility
- Glows achieved with multi-stop box-shadow, not solid borders
- Chromatic aberration: R channel offset +2px, B channel offset -2px in opposite direction

**Motion**
- Scroll-triggered reveals: translateY(40px) → translateY(0) + opacity 0→1, ~600ms ease-out
- Parallax at 0.4x ratio on hero backgrounds
- Hover states: 200ms ease — faster in than out
- Micro-animations on stat numbers (count-up on scroll entry)

---

## Phase 2: Vaporwave / Synthwave CSS Techniques

### Perspective Grid (80s Style)
```css
.grid {
  transform: perspective(400px) rotateX(60deg);
  background-image:
    linear-gradient(rgba(180,120,255,0.4) 1px, transparent 1px),
    linear-gradient(90deg, rgba(180,120,255,0.4) 1px, transparent 1px);
  background-size: 60px 60px;
  animation: gridMove 3s linear infinite;
}
@keyframes gridMove {
  from { background-position: 0 0; }
  to   { background-position: 0 60px; }
}
```

### CRT Scanlines
```css
.scanlines::after {
  content: '';
  position: absolute; inset: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent, transparent 2px,
    rgba(0,0,0,0.15) 2px, rgba(0,0,0,0.15) 4px
  );
  pointer-events: none;
}
```

### Chromatic Aberration (CSS text-shadow)
```css
.glitch {
  text-shadow:
    2px 0 0 rgba(126,244,232,0.8),   /* cyan right */
    -2px 0 0 rgba(244,114,182,0.8);  /* pink left */
  animation: chromatic 4s ease-in-out infinite;
}
@keyframes chromatic {
  0%, 90%, 100% {
    text-shadow: 2px 0 0 rgba(126,244,232,0.8), -2px 0 0 rgba(244,114,182,0.8);
  }
  92% {
    text-shadow: 6px 0 0 rgba(126,244,232,0.9), -6px 0 0 rgba(244,114,182,0.9);
    transform: skewX(-1deg);
  }
  94% {
    text-shadow: -4px 0 0 rgba(126,244,232,0.9), 4px 0 0 rgba(244,114,182,0.9);
    transform: skewX(1deg);
  }
  96% {
    text-shadow: 2px 0 0 rgba(126,244,232,0.8), -2px 0 0 rgba(244,114,182,0.8);
    transform: skewX(0deg);
  }
}
```

### Vignette
```css
.vignette::after {
  background: radial-gradient(ellipse at center, transparent 50%, rgba(4,3,10,0.85) 100%);
}
```

---

## Phase 3: Font Selection

All three confirmed available on fonts.googleapis.com:

| Font | Style | Use |
|------|-------|-----|
| **Orbitron** | Geometric sans-serif, space-age, angular | Logo, primary headings |
| **Share Tech Mono** | Terminal monospace, CRT-authentic | Code blocks, terminal steps, stats |
| **Cinzel** | Roman inscriptional capitals, Art Deco | Classical quotes, subheadings |

Google Fonts import URL:
```
https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;700;900&family=Share+Tech+Mono&family=Cinzel:wght@400;600;700&display=swap
```

Why these work together: Orbitron's geometric futurism + Cinzel's Roman classicism = "ancient wisdom meets machine intelligence" — perfect for Nous. Share Tech Mono grounds both in terminal authenticity.

---

## Phase 4: Wikipedia Image URLs

### School of Athens (Raphael)
The canonical Wikimedia Commons file is:
`File:Raphael_School_of_Athens.jpg`

Direct upload URL (well-established public domain image):
`https://upload.wikimedia.org/wikipedia/commons/4/49/Raphael_School_of_Athens.jpg`

Alternative (higher resolution, different crop):
`https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/Raphael_School_of_Athens.jpg/1920px-Raphael_School_of_Athens.jpg`

### Aristotle Bust
The canonical Wikimedia image is the Ludovisi copy at Palazzo Altemps, Rome.
Direct upload URL:
`https://upload.wikimedia.org/wikipedia/commons/a/ae/Aristotle_Altemps_Inv8575.jpg`

### Plato Bust
The canonical Wikimedia image is the Silanion copy, Munich Glyptothek.
Direct upload URL:
`https://upload.wikimedia.org/wikipedia/commons/8/88/Plato_Silanion_Musei_Capitolini_MC1377.jpg`

---

## Design Decision Log

- Canvas: `#04030a` — near-void black with faint violet undertone
- Grid lines in hero: `rgba(181,123,238,0.35)` (--accent-primary at low opacity)
- Hero image filter: `hue-rotate(240deg) saturate(2.5) brightness(0.35) contrast(1.2)` — pushes purples/blues, kills original warm tones
- Section padding: `120px 0`
- Card hover glow: `box-shadow: 0 0 30px rgba(181,123,238,0.25)`
- Canvas graph: spring constant k=0.003, damping d=0.88, 10 nodes, 14 edges
