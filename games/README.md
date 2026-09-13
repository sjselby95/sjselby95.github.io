# /games — integration notes

Three self-contained browser games. Drop-in static files: **no build step, no framework, no bundler, no npm.**

```
games/
  index.html              hub page listing the three games
  bone-quarry/
    index.html            the game
    voice.mp3             ~1 MB narration track, loaded by relative path
  plate-run/index.html
  thagomizer/index.html
```

## What Claude Code needs to do

1. **Link it from the main nav.** Add a `Games` entry pointing at `/games/`. On the motherboard
   navigation concept, these are a natural fit for a peripheral/expansion-slot component rather than
   one of the core cybersecurity pages.
2. **Restyle `games/index.html` if it drifts from the site.** It was written to match the existing
   look (true black, JetBrains Mono, `#2bbd79` / `#3fe39a` accents) but it does not share the site's
   stylesheet — it has its own inline `<style>`. If there is a shared CSS file, port it over and
   delete the inline block. The three game pages themselves have a deliberately different look and
   should be left alone.
3. **Leave the relative paths alone.** `games/index.html` links to `bone-quarry/`, `plate-run/`,
   `thagomizer/` relatively, and `bone-quarry/index.html` loads `voice.mp3` relatively. Nothing uses
   a root-absolute path, so the whole folder can be moved or renamed as a unit.

## Things worth knowing before changing anything

- **`voice.mp3` is required.** It is one audio sprite holding 169 clips — every dinosaur name, every
  sentence, and every individual word. `bone-quarry/index.html` contains a `VOX` map of
  `{id: [offsetSeconds, durationSeconds]}` and seeks into the file. Re-encoding the mp3 will shift
  every offset and desynchronise the narration. Replace both or neither.
- **Narration plays through an `<audio>` element, not the Web Audio API.** This is deliberate: on
  iOS, Web Audio is silenced by the hardware Ring/Silent switch and a media element is not. Do not
  "modernise" it back to `AudioContext`. Game sound effects *do* use Web Audio, which is fine —
  those are meant to be silenceable.
- **Playback only ever starts from a tap.** No autoplay anywhere. Do not add a preload-and-play
  warmup; an earlier version did that and it leaked audio on page load in mobile Safari.
- **Scores use `localStorage`** (`bonequarry.v1`, `platerun.best`, `thago.best`) wrapped in
  try/catch. Nothing is sent anywhere; there is no analytics, no cookies, no third-party script.
- **Google Fonts is the only external request.** Andika (a literacy typeface — the letterforms
  matter for the reading practice in Bone Quarry) and Saira Stencil One. If the site has a
  no-external-requests policy, self-host both and update the two `<link>` tags; every font stack
  already has a real fallback, so nothing breaks in the meantime.
- **Canvas games size themselves off a fixed 360-unit world height.** `resize()` recomputes the
  world width from the canvas aspect ratio. If a wrapper element changes the stage's dimensions,
  they adapt; no fixed pixel sizes to chase.

## Checks after wiring it up

- `/games/` loads and all three cards link correctly.
- Bone Quarry: open a dig site, finish it, press **Read it to me** — audio should play. If it is
  silent, `voice.mp3` did not get committed or is being served with the wrong content type.
- Plate Run and Thagomizer: play on a phone-width viewport and confirm the whole stage is visible
  without the page scrolling sideways.
