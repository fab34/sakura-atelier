**English | [繁體中文](README.zh-TW.md)**

# Sakura Atelier

An interactive, scroll-driven single-page site for a fictional ink-and-blossom atelier — built as a design demo combining scroll storytelling, SVG line-drawing animation, and a real-time GPU fluid simulation.

**Live demo:** https://fab34.github.io/sakura-atelier/

## Features

- **Scroll-driven parallax** — multiple background layers per section move at independent speeds and directions as you scroll.
- **Scroll-scrubbed SVG line drawing** — an ink branch, an ensō circle, decorative flourishes, and a torii gate are "painted" stroke-by-stroke as the corresponding section scrolls into view (GSAP `ScrollTrigger`, `stroke-dashoffset` technique).
- **Blinds-mask section transition** — the quote section peels open into the closing section using an animated multi-strip mask, inspired by the [tympanus SVG mask scroll transition](https://tympanus.net/Tutorials/SVGMaskScrollTransition/).
- **Suminagashi (墨流し) fluid ink background** — the hero section runs a full GPU fluid simulation (velocity/dye advection, curl & vorticity confinement, divergence, jacobi pressure solve, gradient subtraction) rendered with Three.js. Click or drag to stir the ink; pick from four traditional ink colors, toggle ambient auto-play, or wash the canvas clean.
- Fully responsive layout with reduced-motion-aware autoplay behavior.

## Tech stack

- Static HTML/CSS/JS — no build step, no framework, no backend.
- [GSAP](https://greensock.com/gsap/) + `ScrollTrigger` — scroll-linked animation and pinning.
- [Three.js r128](https://threejs.org/) — WebGL rendering for the fluid simulation.
- Google Fonts: Cormorant Garamond, Noto Serif JP, Shippori Mincho.

## Project structure

```
.
├── index.html   # entire site — markup, styles, and scripts in one file
└── README.md
```

## Running locally

No build step is required. Serve the folder with any static file server, for example:

```bash
python3 -m http.server 8080
# then open http://localhost:8080
```

Opening `index.html` directly via `file://` will not work — the fluid simulation and font loading require an HTTP context.

## Deployment

The site is deployed with **GitHub Pages**, served from the `main` branch root. Pushing to `main` updates the live site automatically.

## Browser support

Requires a modern browser with WebGL support. The fluid simulation auto-detects the best available texture precision (float → half-float → byte) and degrades gracefully on lower-end GPUs; it pauses automatically when the hero section is scrolled out of view or the tab is hidden.

## License

No license specified — all rights reserved by the author.
