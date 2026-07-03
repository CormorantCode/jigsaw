# Daily Jigsaw Puzzle

A browser-based jigsaw puzzle with true interlocking piece shapes, built as a static
GitHub Pages site first, ported to Devvit later.

## Build order (per the original plan)

- [x] **Milestone 1 — tab curve + grid**: plain SVG outlines, no image. Confirmed
      the bezier "tab" shape looks right and that neighboring pieces truly mate
      along every shared edge. Final tuned values: tab height 26%, neck width
      16%, tab diameter 40%, edge bow 10%.
- [x] **Milestone 2 — image clip mask** (`index.html`, this commit): a real
      photo is now clipped to the piece outlines. Confirmed pixel-accurate
      against the source image (block-averaged diff of ~1/255, zero systematic
      offset found via shift-search) — the picture reads correctly across
      every cut, at both square and rectangular (e.g. 6x9) grids.
- [ ] **Milestone 3 — drag-and-drop + snap**: pieces draggable from a tray onto
      a board, snap to place when correct, lock once placed.
- [ ] **Milestone 4 — daily image rotation**: folder of preloaded images, one
      picked per day (by date), piece-count selector (16 / 100 / etc.),
      probably with a mobile-aware default piece count.
- [ ] **Milestone 5 — responsive layout**: board+tray reflow for portrait vs.
      landscape, touch-drag polish.
- [ ] **Port to Devvit**: once all of the above work smoothly as a plain page.

## Milestone 2 — what's in `index.html`

Still a single self-contained HTML file, now with an `images/` folder alongside
it holding the sample art. What's new since milestone 1:

- Every piece gets its own `<clipPath>` (its jigsaw-shaped outline) plus an
  `<image>` element. Critically, **every piece's `<image>` uses the identical
  `x`/`y`/`width`/`height` covering the whole board**, with
  `preserveAspectRatio="xMidYMid slice"` (the SVG equivalent of CSS
  `background-size: cover`). Only the clip differs per piece — so their
  visible slices always line up seamlessly, with no per-piece cropping math
  to get wrong.
- Works for non-square boards too (e.g. 6 cols x 9 rows): the image
  center-crops to cover the rectangle rather than stretching.
- A thumbnail picker switches between the three sample images live.
- An "outlines" checkbox overlays a faint stroke on the cut lines, useful for
  spotting alignment issues; off by default so you can judge how seamless it
  looks assembled.

## Running locally

Just open `index.html` in a browser — it's a static file with no dependencies.
The `images/` folder needs to sit alongside it (relative paths).

## Publishing to GitHub Pages

```bash
git init
git add .
git commit -m "Milestone 1: tab curve + grid"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

Then in the repo on GitHub: **Settings → Pages → Source → Deploy from a
branch → `main` / `root`**. The site will be live at
`https://<your-username>.github.io/<repo-name>/` a minute or two later.

## Next step

Milestone 3: drag-and-drop. Pieces start scattered in a tray, get dragged onto
the board, and snap into place (then lock) when dropped near their correct
position. Say the word and I'll build that next.
