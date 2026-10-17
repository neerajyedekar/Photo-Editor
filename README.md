# Darkroom

A photo editor that runs entirely in the browser. No server, no upload, no build step — one HTML file.

Open `index.html`, or use the hosted copy once GitHub Pages is enabled:
**https://neerajyedekar.github.io/Photo-Editor/**

## What it does

**Crop**
- Drag to move the crop box, grab an edge or corner to resize
- Aspect locks: free, original, 1:1, 4:5, 5:4, 3:2, 2:3, 16:9
- **Exact size** — enter width × height in inches, centimetres or pixels with a dpi setting, and the crop locks to that shape. 5 × 5 in at 300 dpi exports at exactly 1500 × 1500 px. Presets for 4×6, 5×5, 5×7, 8×10, A4, 1080² and 1920×1080.
- Rotate 90°, flip horizontal/vertical, and a straighten slider that auto-zooms so corners never go blank

**Presets**
- Eight built-in looks, each previewed as a thumbnail of the loaded photo
- Save the current settings as your own preset (kept in the browser's local storage)

**Fine-tune**
- Exposure, contrast, saturation, warmth, fade, vignette, grain

**Export**
- Resize by long edge, or let a locked crop set the output dimensions
- JPEG, PNG or WebP with a quality slider
- **Fit to size** — set a KB or MB ceiling and the encoder binary-searches quality down to land under it, dropping resolution only if quality alone can't get there
- "Measure current" reports the resulting file size without saving

## How it works

A single `<canvas>` pipeline. Geometry (rotation, straightening, flips) is applied with canvas transforms; tonal adjustments use `ctx.filter`; warmth, fade, vignette and grain are composited passes. Export re-renders at full resolution rather than scaling the preview, so output quality is independent of screen size. Intermediate canvases are capped at 8192 px on the long edge to stay inside browser limits.

Everything happens in the page. No image data is sent anywhere.

## Browser support

Any current browser. Chrome, Edge, Safari and Firefox all handle the canvas features used here. WebP export depends on the browser's encoder; the page reports it if encoding fails.

## Licence

MIT — see [LICENSE](LICENSE).
