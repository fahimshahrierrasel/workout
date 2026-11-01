# 7-Day Workout Protocol

> Built by [@fahimshahrierrasel](https://github.com/fahimshahrierrasel)

A zero-friction, single-page workout reference built for GitHub Pages. Open the page and today's training day is already on screen — no logging, no accounts, no timers.

## Features

- **Automatic day detection** — `new Date().getDay()` maps the visitor's local day to the correct split (**Tuesday = Day 1 … Monday = Day 7**, rest days Friday & Monday) with a `TODAY` badge on the active tab
- **7-day split viewer** — interactive tabs (grid on desktop, swipeable carousel on mobile) with hash deep links (`#day-push`, `#day-pull`, `#day-legs-abs`, `#day-upper`, `#day-lower-abs`, `#day-rest-fri`, `#day-rest-mon`, or `#day-1`…`#day-7`)
- **Daily cardio** — every day carries a cardio banner: a 10–15 min moderate finisher after lifting on training days, skipped on leg days (Thu & Sun), and an optional 20–30 min easy walk on rest days
- **Exercise image pop-up** — tap/click any exercise thumbnail to open it full-size in a lightbox (browse with ← → arrows, close with Esc or backdrop tap); missing exercise photos render as dashed placeholders until the JPG is added
- **YouTube form guides** — every exercise links to a search in the format `how to do [exercise] proper form` (opens in a new tab, `rel="noopener noreferrer"`, 48×48 px touch targets on mobile)
- **Missed Gym Protocol** — the golden rule, absence-duration playbook (1–2 / 3–5 / 6–10 / 10–14+ days) and a practical field example
- **General Training Guidelines** — 6 core principles plus 4 Coach's Tips (double progression, deloads, protein & sleep, cardio pacing) and a personalization disclaimer
- **Responsive** — exercise tables + full nav on desktop; card-stack layout, collapsible drawers and bottom nav on mobile
- **Zero dependencies to build** — one static HTML file

## Design system

Dark theme tokens (as implemented in `index.html`):

| Token | Value |
| --- | --- |
| Base dark | `#0c0e11` / `#111317` |
| Surfaces | `#1a1c1f` → `#333538` |
| Accent (high-voltage lime) | `#c3f400` |
| YouTube action red | `#93000a` / `#ffb4ab` |
| Headline font | Space Grotesk |
| Body font | Manrope |

## Editing the plan

All workout data lives in a single commented block in `index.html` — search for `MASTER PLAN DATA`, between the `__DATA_START__`/`__DATA_END__` markers. It contains one `DAYS` array with 7 day objects (identity fields `n`, `code`, `name`, `slug`, `badge`; display fields `split`, `short`, `focus`, `target`, `hero`, `heroTag`, `rest`; the cardio banner's `cardio` and optional `cardioOff`; and `type: "train"` with an `exercises` array, or `type: "rest"` with an `items` array). Each exercise supports: `name`, `sets`, `cue`, `yt` (form-video search topic) and `img` (path under `workouts/`). `SLUG_MAP` right below maps hash links to day numbers. Edit there and the entire page (tables, cards, tabs, links) updates automatically.

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
