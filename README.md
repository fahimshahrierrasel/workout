# APEX Split — 7-Day Workout Protocol

A zero-friction, single-page workout reference built for GitHub Pages. Open the page and today's training day is already on screen — no logging, no accounts, no timers.

## Features

- **Automatic day detection** — `new Date().getDay()` maps the visitor's local day to the correct split (Monday = Day 1 … Sunday = Day 7) with a `TODAY` badge on the active tab
- **7-day split viewer** — interactive tabs (grid on desktop, swipeable carousel on mobile) with hash deep links (`#day-push`, `#day-pull`, `#day-legs-abs`, `#day-upper`, `#day-shoulders-legs`, `#day-rest-thu`, `#day-rest-sun`, or `#day-1`…`#day-7`)
- **YouTube form guides** — every exercise links to a search in the format `how to do [exercise] proper form` (opens in a new tab, `rel="noopener noreferrer"`, 48×48 px touch targets on mobile)
- **Missed Gym Protocol** — the golden rule, absence-duration playbook (1–2 / 3–5 / 6–10 / 10–14+ days) and a practical field example
- **General Training Guidelines** — 6 core principles plus a personalization disclaimer
- **Responsive** — exercise tables + full nav on desktop; card-stack layout, collapsible drawers and bottom nav on mobile
- **Zero dependencies to build** — one static HTML file

## Design system

APEX Split dark theme (see `Requirements.md` and the `desktop/` / `mobile/` reference artifacts):

| Token | Value |
| --- | --- |
| Base dark | `#0c0e11` / `#111317` |
| Surfaces | `#1a1c1f` → `#333538` |
| Accent (high-voltage lime) | `#c3f400` |
| YouTube action red | `#93000a` / `#ffb4ab` |
| Headline font | Space Grotesk |
| Body font | Manrope |

## Editing the plan

All workout data lives in a single commented block in `index.html` — search for `MASTER PLAN DATA`. Each day has its exercises, sets × reps, execution cues and YouTube search topic. Edit there and the entire page (tables, cards, tabs, links) updates automatically.

## Run locally

Just open `index.html` in a browser, or serve the folder:

```bash
npx serve .
# or
python -m http.server 8080
```

## Deploy to GitHub Pages

1. Push this repository to GitHub.
2. In the repo: **Settings → Pages → Build and deployment**.
3. Set **Source: Deploy from a branch**, **Branch: `main`**, folder **`/ (root)`**, and save.
4. The site goes live at `https://<username>.github.io/<repo-name>/` (allow a minute or two for the first build).

`.nojekyll` is included so GitHub serves the files as-is without Jekyll processing.

> Optional: add a custom domain under Settings → Pages after the first deploy.
