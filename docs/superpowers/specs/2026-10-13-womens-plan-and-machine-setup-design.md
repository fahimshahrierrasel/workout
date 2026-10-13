# Design: Women's Plan + Machine Setup Links

**Date:** 2026-10-13
**Status:** Approved by user (visual review via brainstorm companion, 3 iterations)

## Overview

Add a women's version of the 7-day workout plan to the single-page site, selectable via a Men/Women toggle. Machine-based exercises in **both** plans get a "machine setup" button that opens a YouTube search for how to set up that machine (same open-in-new-tab pattern as the existing form-guide links). Existing "Video Tutorial" form links stay unchanged.

## Approved Design Decisions

1. **Plan switcher** — segmented pill toggle in the hero section (option A): `♂ MEN'S PLAN | ♀ WOMEN'S PLAN` with silhouette icons + text. Active side: lime fill (`#c3f400`) with dark text. Selection persists in `localStorage`; switching re-renders title, day tabs, panels, and keeps the auto "TODAY" day detection working.
2. **Setup trigger** — small sliders-style settings icon (not gear) in its own **SETUP** table column (option B). Lime outline, 24×24 touch target. Appears **only** on machine exercises with seat/pin/pad/backrest adjustments. Plain cable and DB/barbell rows show an em-dash (desktop) or no button (mobile cards).
3. **Setup behavior** — **no popup**. Clicking the icon opens YouTube search results in a new tab (`rel="noopener noreferrer"`), query format: `how to set up {machine}` (e.g., "how to set up lat pulldown machine"). Existing per-exercise "Video Tutorial" links remain exactly as they are.
4. **Machines** — women's plan uses only equipment already present in the men's plan (no assisted pull-up, no abductor machine, no captain's chair).

## Women's Plan Data (final)

Split structure identical: Day 1–6 training, Day 4 & 7 rest. Rep ranges shifted to 8–15.

### Day 1 — PUSH (Chest • Shoulders • Triceps)
| Exercise | Sets × Reps | Setup | Image |
|---|---|---|---|
| Machine Press | 2–3 × 8–12 | ✓ | reuse Push Day |
| DB Shoulder Press | 2–3 × 8–12 | — | reuse Push Day |
| Low-To-High Cable Fly | 2–3 × 10–15 | — | reuse Push Day |
| DB Lateral Raise | 2–3 × 12–15 | — | reuse Push Day |
| Triceps Extensions | 2–3 × 10–12 | — | reuse Push Day |
| Overhead Extension | 2–3 × 10–12 | — | reuse Upper Day |

### Day 2 — PULL (Back • Rear Delts • Biceps)
| Exercise | Sets × Reps | Setup | Image |
|---|---|---|---|
| Lat Pulldown | 2–3 × 8–12 | ✓ | reuse Pull Day |
| Chest Supported Row | 2–3 × 8–12 | ✓ | reuse Pull Day |
| Face Pull | 2–3 × 12–15 | — | **NEW** |
| Reverse Pec Dec | 2–3 × 12–15 | ✓ | reuse Pull Day |
| Cable Curl | 2–3 × 10–12 | — | reuse Upper Day |
| Cable Hammer Curl | 2–3 × 10–12 | — | reuse Pull Day |

### Day 3 — GLUTES & LEGS (Glutes • Hamstrings • Quads)
| Exercise | Sets × Reps | Setup | Image |
|---|---|---|---|
| Barbell Hip Thrust | 2–3 × 8–12 | — | **NEW** |
| Bulgarian Split Squat (DB) | 2–3 × 8–10 | — | **NEW** |
| Romanian Deadlift | 2–3 × 8–10 | — | reuse Leg Day |
| Leg Extension | 2–3 × 10–12 | ✓ | reuse Leg Day |
| Leg Curl | 2–3 × 10–12 | ✓ | reuse Leg Day |
| Adductor Machine | 2–3 × 12–15 | ✓ | reuse Leg Day |

### Day 4 — REST & RECOVERY (shared content, unchanged)

### Day 5 — UPPER (Back • Chest • Shoulders • Arms)
| Exercise | Sets × Reps | Setup | Image |
|---|---|---|---|
| Lat Pulldown | 2–3 × 8–10 | ✓ | reuse Pull Day |
| Close-Grip Seated Row | 2–3 × 8–12 | ✓ | reuse Pull Day |
| DB Shoulder Press | 2–3 × 8–12 | — | reuse Upper Day |
| Pec Dec | 2–3 × 10–12 | ✓ | reuse Upper Day |
| DB Lateral Raise | 2–3 × 12–15 | — | reuse Push Day |
| Overhead Extension | 2–3 × 10–12 | — | reuse Upper Day |

### Day 6 — GLUTES, LEGS & ABS (Glutes • Quads • Calves • Core)
| Exercise | Sets × Reps | Setup | Image |
|---|---|---|---|
| Leg Press (high/wide stance) | 2–3 × 8–12 | ✓ | reuse Lower Day |
| Smith Sumo Squat | 2–3 × 8–10 | ✓ | **NEW** |
| Cable Glute Kickback | 2–3 × 12–15 | — | **NEW** |
| Smith Calf Raises | 2–3 × 12–15 | ✓ | reuse Lower Day |
| Cable AB Crunch | 2–3 × 12–15 | — | reuse Lower Day |
| Cable Reverse Crunch | 2–3 × 10–15 | — | **NEW** |

### Day 7 — REST & RECOVERY (shared content, unchanged)

**New photos needed (6):** Hip Thrust, Bulgarian Split Squat, Face Pull, Smith Sumo Squat, Cable Glute Kickback, Cable Reverse Crunch → new folders `workouts/Glute & Leg Day/` (Hip Thrust, Bulgarian Split Squat) and `workouts/Glute, Leg & Abs/` (Smith Sumo Squat, Cable Glute Kickback, Cable Reverse Crunch) plus `workouts/Pull Day/Face Pull.jpg`.

## Men's Plan Changes

No exercise/rep changes. Each machine exercise gains a `setupQuery` field:
Machine Press, Lat Pulldown, Chest Supported Row (Pull Day + Upper Day), Close-Grip Seated Row, Reverse Pec Dec, Pec Dec, Hack Squat, Leg Extension, Leg Curl, Seated Leg Curl, Leg Press, Adductor Machine, Smith Calf Raises. Cables and free weights get none.

## Architecture Changes (index.html only)

1. **Data:** refactor the single `MASTER PLAN DATA` block into `PLANS = { men: {...}, women: {...} }`. Each plan: title, subtitle, 7 day objects (name, focus, exercises). Exercise entry: `{ name, sets, reps, img, tutorialQuery, setupQuery? }`. Shared: missed-gym protocol, guidelines, rest-day copy.
2. **Renderer:** tab/panel build functions read from the active plan object. Toggle sets `activePlan`, saves to `localStorage('plan')`, re-renders, updates hero title + tabs + TODAY badge. Default: men's plan (first visit); restore saved choice on load. Hash deep-links (`#day-1`…) keep working.
3. **Setup column:** desktop table gains SETUP column; renderer emits the sliders-icon `<a>` when `setupQuery` exists, else muted em-dash. Mobile card layout: small icon link in the card meta row. `aria-label="Watch how to set up {machine}"`.
4. **Placeholder images:** `onerror` on exercise thumbnails swaps to a dashed-border placeholder div (name initials or 📷) so the 6 missing photos don't render as broken images. Once real JPGs are dropped into `workouts/`, they display automatically — no code change.
5. **Setup link URL:** `https://www.youtube.com/results?search_query=` + encoded `how to set up {machine}`.

## Files Touched

- `index.html` — data refactor, toggle, setup column, placeholder handling, meta description update
- `workout-plan.md` — add women's plan section (mirrors above), note shared sections
- `README.md` — document the plan switcher + machine setup links
- `.gitignore` — add `.superpowers/` (brainstorm mockups)

## Out of Scope

- Embedding videos (links only, per user)
- Curated/hand-picked setup video IDs (user chose automatic search)
- Cycle-aware training notes (not requested in final scope)
- Backend/accounts (none today)

## Testing Checklist

- Toggle swaps all 7 tabs, hero title, TODAY badge; choice persists across reload
- TODAY badge correct for both plans on any weekday
- Every form-tutorial link still opens correct search (both plans)
- Setup icon appears on exactly the machine rows, opens `how to set up {machine}` search in new tab
- 6 new exercises show placeholder, not broken image; adding a JPG makes the photo appear
- Mobile: tabs swipe, setup icon reachable, lightbox still works on both plans
- Missed-gym protocol + guidelines render once, shared by both plans
