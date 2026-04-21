# Live Hatching Studio

A browser-based creative coding tool that converts your webcam feed — or any uploaded image — into live cross-hatched drawings. Configure layer angles, thresholds, and stroke properties in real time. Export snapshots as PNG or as pen-plotter-ready SVG.

**Live demo:** `https://YOUR-USERNAME.github.io/YOUR-REPO/`

## Features

- Live webcam feed with adjustable sample resolution
- Image upload via file picker or drag-and-drop
- Four configurable hatching layers, each with its own angle, darkness threshold, and density
- Jitter and overshoot for a hand-drawn feel
- PNG export of the current frame
- SVG export grouped by layer — works with AxiDraw, vpype, saxi, and Inkscape plotter extensions
- Four built-in palettes (Classic / Blueprint / Rust / Night), plus custom color picking

## Deploy to GitHub Pages

1. Create a new public repository on GitHub
2. Upload `index.html` to the root of the repo (either via the web UI or `git push`)
3. In the repo: **Settings → Pages → Source → Deploy from a branch → `main` / `(root)`**
4. Wait ~60 seconds, then open `https://<your-username>.github.io/<your-repo>/`
5. Grant camera permission on first visit

## Local development

A single static HTML file — no build step. For local testing, serve it over HTTP (the camera API is blocked on `file://`):

```bash
python3 -m http.server 8000
# then open http://localhost:8000/
```

## Plotter export notes

For the cleanest plot:

- Set **Jitter** and **Overshoot** to `0` before clicking **Save SVG** — this avoids unnecessary pen-up/pen-down cycles
- In [vpype](https://github.com/abey79/vpype), post-process with `vpype read input.svg linemerge --tolerance 0.5 linesort write output.svg` to merge adjacent segments and optimize pen travel
- Each hatching layer is exported as its own `<g>` group (`id="layer-1"` etc.), so you can assign different pens per layer in your plotter toolchain
