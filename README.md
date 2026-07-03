# Daily Jigsaw Puzzle

A browser-based jigsaw puzzle with true interlocking piece shapes, built as a static
GitHub Pages site first, ported to Devvit later.

## Build order (per the original plan)

- [x] **Milestone 1 — tab curve + grid** (`index.html`, this commit): plain SVG
      outlines, no image. Confirms the bezier "tab" shape looks right and that
      neighboring pieces truly mate along every shared edge.
- [ ] **Milestone 2 — image clip mask**: apply a real photo as a clip path over
      the piece outlines, confirm the picture reads correctly across piece
      boundaries at various piece counts.
- [ ] **Milestone 3 — drag-and-drop + snap**: pieces draggable from a tray onto
      a board, snap to place when correct, lock once placed.
- [ ] **Milestone 4 — daily image rotation**: folder of preloaded images, one
      picked per day (by date), piece-count selector (16 / 100 / etc.).
- [ ] **Milestone 5 — responsive layout**: board+tray reflow for portrait vs.
      landscape, touch-drag polish.
- [ ] **Port to Devvit**: once all of the above work smoothly as a plain page.

## Milestone 1 — what's in `index.html`

A single self-contained HTML file (no build step, no dependencies) that:

- Builds an edge-grid for an arbitrary `cols x rows` piece count and randomly
  assigns each interior edge a tab direction (in/out), seeded so results are
  reproducible.
- Traces each piece's 4-sided outline as an SVG path, reusing **one** bezier
  "tab" curve for every interior edge (mirrored/flipped per edge), and a flat
  line for border edges — exactly the "one stamp, reused everywhere" approach
  from the original plan.
- Exposes sliders for tab size, neck width, and organic jitter, plus a seed
  and piece-count controls, and an exploded-view toggle — so you can do the
  "tweak a control point, look, tweak again" loop live in the browser instead
  of editing code each round.

Open `index.html` directly in a browser (no server needed) to play with it.

## Running locally

Just open `index.html` in a browser — it's a static file with no dependencies.

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

Milestone 2: pick one source image, crop it into the piece grid, and clip
each piece's image slice to its SVG path so the photo reads correctly across
piece boundaries. Say the word and I'll build that next, using this same
tab-curve/grid code as the foundation.
