# assets/

Drop-in media for `index.html`. Everything here is **optional** — the page is
designed to look finished without any of it, and to upgrade itself the moment a
file appears.

---

## 1. Your portrait — `assets/ian-portrait.jpg`

This is the one file worth adding first. It renders in the hero, inside the
monitoring-console frame, and it is the first thing a recruiter sees.

| | |
|---|---|
| **Path** | `assets/ian-portrait.jpg` (exact name, lowercase) |
| **Aspect** | 4:5 portrait (the frame is `aspect-ratio: 4 / 5`) |
| **Size** | ~1200 × 1500px. Keep the file under ~400KB — export at quality 80. |
| **Crop** | Head and shoulders, eyes roughly a third of the way down. |

The photo you're using — dark blue checked shirt, arms folded, white perforated
wall behind you — is a good fit: the background is neutral enough that the
frame's green wash reads as intentional rather than a clash.

**Until the file exists** the frame shows an `IO` monogram card instead. No
console error, no broken-image icon — it just looks like a designed placeholder.

If your crop sits differently in the frame, adjust one line in the `<style>`
block:

```css
.portrait-img { object-position: 50% 22%; }   /* lower the % to show more head */
```

A `.webp` alongside the `.jpg` is a nice-to-have, not a requirement.

---

## 2. Real footage — `assets/reel/*.mp4`

The Ops Reel section ships with four **vector scenes** that animate in the
browser: alarm triage, KPI watch, SLA burn-down, and the automation pipeline.
They need no download and stay sharp at any size, so there is no obligation to
replace them.

If you do record real screen-capture or talking-head footage, put the files here
and point at them in `REEL_MEDIA`, near the bottom of `index.html`:

```js
const REEL_MEDIA = {
  alarm:      { video: 'assets/reel/alarm.mp4',      narration: null },
  kpi:        { video: 'assets/reel/kpi.mp4',        narration: null },
  sla:        { video: null,                         narration: null },
  automation: { video: 'assets/reel/automation.mp4', narration: null },
};
```

Any scene given a `video` path swaps its vector scene for a muted, looping
`<video>` — **only once the file actually loads**, so a typo or a missing file
degrades back to the vector scene rather than showing a black rectangle.

Encoding: H.264 MP4, 1920×1080 or 1280×720, ~8–12 seconds, under ~3MB each.
Each scene holds for 9 seconds, so anything shorter will loop seamlessly.

---

## 3. Narration — `assets/audio/*.mp3`

The reel's sound is **synthesised in the browser** with the Web Audio API: a
quiet filtered room tone plus sparse telemetry blips whose pitch and pace change
with the scene. It is off by default behind the `Sound off` button (browsers
require a click before any audio can start), it loops without a seam because
nothing is actually looping, and it costs zero bytes to download.

To use your own voice-over instead, add `narration` paths to the same
`REEL_MEDIA` object:

```js
sla: { video: null, narration: 'assets/audio/sla.mp3' },
```

That clip's narration plays instead of the synth bed while the scene is on
screen. Keep each under 9 seconds to match the scene duration.

---

## 4. Résumé

The footer has a résumé button pointing at `#`. Once you drop a PDF in here,
update that one `href`:

```html
<a href="assets/ian-ondieki-cv.pdf" ...>Résumé ↓</a>
```

The page also has a proper print stylesheet, so ⌘P / Ctrl-P already produces a
clean document if you would rather not maintain a separate PDF.
