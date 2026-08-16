# EditStream — project page

Source for the EditStream project page.

**Live site:** https://real-time-video-research.github.io/editstream/

## What's here

```
index.html          the whole page (52 KB, no build step, no dependencies)
assets/video/*.mp4  21 demo clips, H.264, faststart, silent
assets/img/*.jpg    poster frames (one per clip) + the reference-edit still
.nojekyll           tells GitHub Pages to serve the files as-is
```

The page is a single static HTML file with inline CSS and JS. There is no
framework, no bundler, and no external network request — it renders offline
from this directory.

## Running it locally

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Opening `index.html` directly via `file://` also mostly works, but some
browsers block video playback from the file protocol, so the local server is
the reliable way to preview.

## Deploying

Any static host works. For GitHub Pages, push to the default branch and set
**Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)`**.

## Regenerating the clips

Every clip is a re-encode of an EditStream inference output. Hero clips are
1280×704 @ 16 fps, demo clips 1024 px wide, all CRF 23–25 with
`-movflags +faststart` so playback can begin before the file finishes
downloading. Each has a matching poster frame in `assets/img/` so the page
paints instantly and only fetches video on scroll (`preload="none"`).

## Credit

Videos are outputs of the released 4-step causal student model. See the page
itself for authors, method, and citation.
