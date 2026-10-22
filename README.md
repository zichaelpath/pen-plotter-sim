# 🖊️ PlotterSim — Pen Plotter Simulator

Feed it an image. It draws the **outlines first, colour by colour**, then **fills everything in like a real marker** — back-and-forth strokes, pen lifts, pen swaps at the dock and all — on a virtual pen plotter. Made for producing those oddly-satisfying plotter videos for TikTok / Reels / Shorts / YouTube.

**▶ Try it live: https://zichaelpath.github.io/pen-plotter-sim/**

100% client-side: your images never leave your device. No build step, no dependencies — one self-contained `index.html`.

## How to use it

1. **Drop in an image** (or tap the drop zone), or start with a built-in demo (star / berry / rocket). Flat, cartoony and anime-style art works best.
2. **Press Play** and watch it draw: outlines in a darker shade of each colour first, then the marker fill, light colours before dark.
3. **Record video**: pick a format (Square 1:1, or Portrait 9:16 for TikTok), pick a target video length, hit **● Record video**. It replays the drawing at exactly that length and downloads the video, ready to post.
4. Or grab the **final PNG** of the finished drawing.

## Real photos work too — the Paint by Order simplifier

Turn on **Photo simplifier** (on by default) and a real-life photo gets the same treatment as the *Paint by Order* converter:

1. Smooth the photo (shrink-and-upscale blur) to kill sensor noise and JPEG speckle.
2. Quantize it to a small pen palette (median-cut, 3–14 colours).
3. Flood-fill it into connected regions, then apply the **"no confetti" rule**: every region smaller than the detail threshold is absorbed into the neighbouring region with the closest colour.
4. Detail is a slider: **Relaxed** = big chunky regions and few pens, **Classic** = balanced/cartoonish, **Detailed** = smaller regions, more faithful.

The simplified preview in the side panel shows you exactly what the plotter will draw — if it passes the squint test there, it'll draw well.

## Controls

| Control | What it does |
|---|---|
| Colours | How many pens (palette size) |
| Marker thickness | Width of the fill marker — thicker = chunkier, faster fill |
| Fill pattern | Back-and-forth rows / diagonal / cross-hatch |
| Outline style | Darker shade per colour / colour as-is / classic black / none |
| White = paper | Treats near-white as blank paper (great for line art on white) |
| Playback speed | 0.25×–6× for previewing |
| Video format | Square 1:1 or Portrait 9:16 (TikTok/Reels/Shorts) |
| Recorded video length | 8–60 s — recording auto-speeds the drawing to fit |
| Caption | Text burned into portrait videos |

## How it works (under the hood)

- **Outlines:** marching-squares contour tracing on each colour mask, chained into polylines.
- **Fill:** scan-line runs clipped to each colour mask, drawn back-and-forth (boustrophedon) with slight deterministic wobble and 86% opacity, so overlapping passes band darker like a real marker.
- **Plotter:** a tiny state machine — *swap pen → travel (pen up) → pen down → draw → pen up* — driving a gantry + carriage + pen rendered over the paper each frame.
- **Video:** `canvas.captureStream()` + `MediaRecorder`. MP4 where the browser supports it (Chrome/Edge), otherwise WebM — TikTok's web uploader accepts both.

## Roadmap ideas

- SVG / G-code export for driving a *real* plotter later
- Batch mode: folder of images → folder of videos for a posting queue
- Pen sounds / paper texture themes

## License

MIT © 2026 Zachary Shade
