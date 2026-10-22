# Endo Rotation: Operation Homeostasis

A 14-day gamified endocrinology rotation for internal medicine residents, built as an installable, offline-capable web app (PWA). Content is adapted from *Endocrine Secrets* (2009), with amber "2026 Update" notes where current guidelines differ.

No build step and no dependencies. It's plain HTML, CSS, and JS.

## Play locally

```powershell
powershell -ExecutionPolicy Bypass -File tools\serve.ps1 -Port 8080
```

Open http://localhost:8080. Opening `index.html` directly also works, but offline caching only activates over http(s).

## Publish (GitHub Pages)

```powershell
gh auth login
gh repo create endo-rotation-game --public --source . --push
gh api -X POST repos/{owner}/endo-rotation-game/pages -f "source[branch]=main" -f "source[path]=/"
```

The game will be at `https://<your-username>.github.io/endo-rotation-game/`.

No-tools alternative: drag this folder onto https://app.netlify.com/drop.

## Install on your phone

- **iPhone (Safari):** open the URL, tap Share, then **Add to Home Screen**.
- **Android (Chrome):** open the URL and tap **Install** in the app, or use ⋮ → **Install app**.

Progress (XP, badges, scores) is saved on the device in localStorage.

## Adding a day

1. Create `content/dayN.js` that sets `window.ENDO_CONTENT[N] = { scene, objectives, source, stations: [...] }`. Use `content/day1.js` as the template. Station types are `consult`, `pager`, `match`, `sort`, `boss`, and `pearls`.
2. Add a `<script src="content/dayN.js">` tag in `index.html`.
3. Add the file to `ASSETS` in `sw.js` and bump `CACHE`.

## Testing

With the local server running, open `http://localhost:8080/tools/selftest.html`. It plays through all of Day 1 automatically and reports the score for each station and any errors.

Icons are regenerated with `tools\make-icons.ps1`.
