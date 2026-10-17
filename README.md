# ads-sponsor

Remote content for the sponsor slot in **pingping**, **fogping** and **json-ping**.
Change the ads by editing files here — no new software release needed.

## Layout

```
pingping/   sponsors.json + slide-1.png … slide-3.png
fogping/    sponsors.json + slides
json-ping/  sponsors.json + slides
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
    { "image": "slide-1.png", "link": "https://example.com", "alt": "Example Co.", "title": "optional caption" }
  ]
}
```

- `slides`: up to **3** entries; extra entries are ignored.
- `image`: path relative to the manifest (e.g. `slide-1.png`) or an absolute **https** URL.
- `link`: click-through URL; only `http://` and `https://` are accepted (`mailto:` is rejected).
  Slides with an invalid or missing link are shown but not clickable.
- `alt`: required in practice (accessibility text). `title`: optional caption shown next to the dots.
- `version` / `updated`: bump when you change the manifest; informational only.

## Image size

- **1456 × 180 px PNG** (displayed at 728 × 90 CSS px, i.e. the standard leaderboard size at 2× for sharp screens).
- Aspect ratio must be **8.09 : 1 (728:90)**; other ratios are cropped to fit (`object-fit: cover`).
- Keep files small (< 150 KB). PNG, JPEG, WebP or GIF all work.
- In pingping at a 1850 px wide window the sponsor box is ~1800 px wide and the carousel occupies up to 728 px of it.

## How to swap an ad

1. Replace `<product>/slide-N.png` (same file name) or add a new image and point `image` at it.
2. Edit `link`, `alt`, `title` in `<product>/sponsors.json`; bump `version`.
3. Commit to `main`. That's it.

## Caching

`raw.githubusercontent.com` is served through a CDN with roughly a **5-minute** cache, so changes
appear within ~5 minutes. If you replace an image under the same name and want it to show immediately,
use a new file name instead (e.g. `slide-1-v2.png`).

## Behaviour in the apps

- Rotates the slides every ~5.5 s with small dots; pauses on hover; links open in a new tab
  (`rel="noopener noreferrer sponsored"`).
- Fails closed: offline / intranet / timeout (3 s) / bad JSON / no image loads → the app shows its
  built-in sponsor text exactly as before. Broken images are never shown.

## Contact

Want the slot? Email **route66traffic66@gmail.com**.
