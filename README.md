# ads-sponsor

Remote content for the sponsor slot in **pingping**, **fogping**, **json-ping** and **traffic66**.
Change the ads by editing files here — no new software release needed.

## Layout

```
pingping/   sponsors.json + ethicalads.png, carbonads.png, buysellads.png, baidu-cloud.png
fogping/    sponsors.json + slides
json-ping/  sponsors.json + slides
traffic66/  sponsors.json + slides (a strip across the top of the page in unregistered installations)
```

Each app's browser page fetches
`https://raw.githubusercontent.com/githubflyideas/ads-sponsor/main/<product>/sponsors.json`
directly (the server never contacts GitHub).

## sponsors.json

```json
{
  "version": 1,
  "updated": "2026-10-17",
  "slides": [
    { "id": "optional-campaign-id", "image": "ethicalads.png", "link": "https://example.com", "alt": "Example Co.", "title": "optional caption" }
  ]
}
```

- `slides`: up to **4** entries (traffic66: up to **6**); extra entries are ignored.
- `image`: path relative to the manifest (e.g. `ethicalads.png`) or an absolute **https** URL.
- `link`: click-through URL; only `http://` and `https://` are accepted (`mailto:` is rejected).
  Slides with an invalid or missing link are shown but not clickable.
- `id`: optional; traffic66 uses it as `utm_campaign` (falls back to a slug of `alt`).
- `alt`: required in practice (accessibility text). `title`: optional caption shown next to the dots.
- `version` / `updated`: bump when you change the manifest; informational only.

## Image size

**traffic66** is different from the other three: **1456 × 180 px** (728 × 90 at 2×, ratio 8.09 : 1).
The strip across the top of the page puts as many of them side by side as the window has room for
and rotates the rest. Other ratios are cropped to fit.

The others (pingping, fogping, json-ping):


- **468 × 120 px PNG** (displayed at **234 × 60** CSS px — the IAB "half banner" — at 2× for sharp screens).
- Aspect ratio must be **3.9 : 1 (234:60)**; other ratios are cropped to fit (`object-fit: cover`).
- Keep files small (< 100 KB). PNG, JPEG, WebP or GIF all work (no SVG). Keep text short and large:
  at display size a 30 px (2×) headline is ~15 px on screen.
- The slot sits in the page header, centred between the title and the controls. If the window is too
  narrow for it to fit beside them, it moves to its own row under the header.
- Releases before pingping v0.6.2 / fogping v1.2.2 / json-ping v3.2.2 show the slot at the bottom at
  728 × 90 and will crop these images.

## How to swap an ad

1. Replace an image in `<product>/` (same file name) or add a new image and point `image` at it.
2. Edit `link`, `alt`, `title` in `<product>/sponsors.json`; bump `version`.
3. Commit to `main`. That's it.

## Caching

`raw.githubusercontent.com` is served through a CDN with roughly a **5-minute** cache, so changes
appear within ~5 minutes. If you replace an image under the same name and want it to show immediately,
use a new file name instead (e.g. `ethicalads-v2.png`).

## Behaviour in the apps

- Rotates the slides every ~5.5 s with small dots; pauses on hover; links open in a new tab
  (`rel="noopener noreferrer sponsored"`).
- Fails closed: offline / intranet / timeout (3 s) / bad JSON / no image loads → the app shows its
  built-in sponsor text exactly as before. Broken images are never shown.

## Contact

Want the slot? Email **route66traffic66@gmail.com**.
