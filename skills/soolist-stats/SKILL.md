---
name: soolist-stats
description: Reads the user's Soolist numbers and year in review — how much they rated and finished, average score, streaks, busiest months, favourite kinds and lists — and shares or unshares a yearly recap page. Use when the user asks how much they watched or read, for their stats or streak, or for their year in review.
---

# Stats and yearly recap

## Quick start

1. Follow `soolist-session`.
2. Numbers for a period → `stats_show` (`period`: `this_year`, `last_year`, `all`, or a year like `2024`).
3. Year in review → `recap_show` with `year`.
4. Answer with the few numbers that matter; do not dump every bucket.

## Reading it well

- `averageScore`, `average` and recap `score` are on a 0–10 scale, whatever the list's own scale.
- `finished` counts topics marked finished, plus rated topics they never tracked.
- `activity.buckets` are per month for a year, per year for `all`. `longestStreak` is days in a row with a rating.
- `insights[].message` is already in the user's language; you may quote it.
- `availableYears` lists years with ratings — offer those when the user is unsure.

## Sharing a recap

- `recap_share` with `shared: true` makes that year's recap a public page at `shareUrl`; only public topics appear there. Do it only when the user asks, and give them the link.
- `shared: false` takes the page down again. Check `isShared` from `recap_show` before offering either.

## Hard boundaries

- Stats and the private recap include private lists. Do not paste them anywhere public unless the user asks.
- Only the current year and earlier have a recap.

## Handover

- "What should I watch next?" → `soolist-track` (random pick) or `soolist-taste`.
