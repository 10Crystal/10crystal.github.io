# Monet Portrait Generator

Turn any photo into an impressionist oil painting in the style of Claude Monet. Runs entirely in the browser — no backend, no AI model, no dependencies.

> **🎨 [Try it live →](https://10crystal.github.io/monet-portrait-generator/)**

---

**Author:** Crystal  
**Date:** 2026-07-14  
**License:** [MIT](LICENSE)

---

## Table of Contents

1. [Background](#background)
2. [How It Works](#how-it-works)
3. [Usage](#usage)
4. [Parameters](#parameters)
5. [Setup](#setup)
6. [Files](#files)
7. [References](#references)

---

## Background

Impressionism is a 19th-century French art movement, with Claude Monet (1840–1926) as its most celebrated figure. Its defining traits include:

- Short, visible brushstrokes (broken colour)
- Emphasis on light and atmosphere over precise form
- Optical colour mixing — colours placed side by side on the canvas, blended by the viewer's eye
- Soft, luminous transitions and a dreamlike quality

This program simulates the style via a **painterly rendering** algorithm: thousands of semi-transparent elliptical strokes are layered from coarse to fine to "paint" the source image, with each stroke's colour nudged toward Monet's signature palette.

---

## How It Works

### Algorithm Pipeline

| Step | Operation | Description |
|------|-----------|-------------|
| 1. Sample | Read source pixels | Scale the uploaded image to the canvas, extract RGB values |
| 2. Stroke generation | Loop N strokes | For each stroke: random position → sample source colour → Monet palette shift → random jitter → draw ellipse |
| 3. Coarse to fine | Decreasing radius | First 20% of strokes ~12 px radius, last 20% ~2.5 px — mimicking how a real painter works |
| 4. Colour shift | HSL-space interpolation | Each sampled colour is interpolated toward the nearest Monet palette colour in HSL space (mix ratio = jitter value) |
| 5. Soft bloom | Gaussian blur overlay | The finished painting is blurred and overlaid at 35% opacity, producing Monet's characteristic soft glow |

### Monet Palette

Program's built-in Monet colours (HSL representation):

| Colour Name | Hue | Saturation | Lightness | Inspiration |
|-------------|-----|-----------|-----------|-------------|
| Lavender | 250° | 0.35 | 0.75 | *Nymphéas* (Water Lilies) |
| Sage Green | 155° | 0.20 | 0.60 | *Japanese Bridge* |
| Pond Blue | 200° | 0.30 | 0.65 | *Nymphéas* |
| Warm Gold | 35° | 0.40 | 0.75 | *Impression, Sunrise* |
| Rose | 345° | 0.18 | 0.72 | *Garden at Giverny* |
| Deep Water | 170° | 0.15 | 0.55 | *Water Lily Pond* |
| Sky Blue | 210° | 0.25 | 0.70 | *Argenteuil* |
| Peach | 25° | 0.35 | 0.78 | *Haystacks* |

---

## Usage

### Online

**[10crystal.github.io/monet-portrait-generator](https://10crystal.github.io/monet-portrait-generator/)**

### Local

1. Download `index.html`
2. Open it in any modern browser
3. Click the upload area or drag an image onto it
4. Adjust the sliders to your liking
5. Click **Re-render** to regenerate
6. Click **Download** to save the result as a PNG

---

## Parameters

| Parameter | Range | Default | Effect |
|-----------|-------|---------|--------|
| Strokes | 1 000 – 20 000 | 6 000 | More strokes = finer detail, longer render time |
| Size | 0.3 – 2.5 | 1.0 | Base size multiplier for brush ellipses |
| Jitter | 0 – 0.4 | 0.15 | Random colour deviation per stroke; higher = wilder |
| Softness | 0 – 12 | 4 | Post-processing blur strength in px (the Monet glow) |

### Recommended Presets

| Style | Strokes | Size | Jitter | Softness |
|-------|---------|------|--------|----------|
| Fine Portrait | 12 000 | 1.0 | 0.10 | 3 |
| Classic Impression | 6 000 | 1.0 | 0.15 | 4 |
| Bold Landscape | 3 000 | 1.8 | 0.25 | 8 |
| Quick Preview | 1 500 | 1.5 | 0.15 | 2 |

---

## Setup

### Requirements

- Any modern browser (Chrome / Firefox / Safari / Edge)
- No Node.js, Python, or any server-side environment needed
- Works fully offline — no internet connection required

### Browser Support

| Browser | Minimum Version |
|---------|----------------|
| Chrome | 60+ |
| Firefox | 55+ |
| Safari | 12+ |
| Edge | 79+ |

---

## Files

```
monet-portrait-generator/
├── index.html          ← Main app (double-click to open)
├── README.md           ← This file
├── LICENSE             ← MIT license
└── .gitignore
```

---

## References

1. **Monet, C.** (1906). *Nymphéas* [Oil on canvas]. Musée de l'Orangerie, Paris.  
   Monet's late Water Lilies series — the primary inspiration for the colour palette.

2. **Haeberli, P.** (1990). Paint by numbers: Abstract image representations. *ACM SIGGRAPH Computer Graphics*, 24(4), 207–214.  
   [DOI: 10.1145/97880.97902](https://doi.org/10.1145/97880.97902)  
   The seminal paper introducing stroke-based non-photorealistic rendering.

3. **Litwinowicz, P.** (1997). Processing images and video for an impressionist effect. *Proceedings of SIGGRAPH 97*, 407–414.  
   [DOI: 10.1145/258734.258893](https://doi.org/10.1145/258734.258893)  
   Classic impressionist rendering algorithm with gradient-guided stroke orientation.

4. **Hertzmann, A.** (1998). Painterly rendering with curved brush strokes of multiple sizes. *Proceedings of SIGGRAPH 98*, 453–460.  
   [DOI: 10.1145/280814.280951](https://doi.org/10.1145/280814.280951)  
   Multi-layered curved strokes of varying sizes — the theoretical basis for the coarse-to-fine strategy.

5. **Gooch, B. & Gooch, A.** (2001). *Non-Photorealistic Rendering*. A K Peters / CRC Press.  
   [ISBN: 978-1568811338](https://www.routledge.com/Non-Photorealistic-Rendering/Gooch-Gooch/p/book/9781568811338)  
   The authoritative textbook on non-photorealistic rendering.

---

## Acknowledgements

- Monet's works are in the public domain and freely reinterpretable.
- The algorithm draws on decades of NPR (non-photorealistic rendering) research.
- Thanks to [PavelDoGreat/WebGL-Fluid-Simulation](https://github.com/PavelDoGreat/WebGL-Fluid-Simulation) for inspiration during development.

---

> "Color is my day-long obsession, joy and torment." — Claude Monet
