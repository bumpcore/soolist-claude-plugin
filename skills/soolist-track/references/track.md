# Tracking details

## Statuses

| Status | Meaning | Side effects |
|---|---|---|
| `planned` | Wants to do it | none |
| `in_progress` | Started | stamps the start date; from `finished` it begins a new run (progress back to 0) |
| `finished` | Done | stamps the finish date; fills progress up to its total |
| `paused` | Stopped for now | none |
| `dropped` | Gave up | none |

Setting the status it already has changes nothing.

## Progress

- Units: `episode`, `page`, `chapter`, `hour`, `percent`, `item`. `percent` implies a total of 100.
- `total` and `unit` are remembered; send them once.
- Progress never goes below 0 or above the total.
- A day's movement is written to the topic's notes as one progress line.

Examples:

- "I'm on episode 5 of Severance, season has 10" → `current: 5, total: 10, unit: episode`.
- "Read 30 more pages" → `step: 30`.
- "Oops, I'm one episode back" → `step: -1`.

## Notes and history

- Notes, status/progress lines and ratings all live in the topic's notes: `notes_list` (see `soolist-notes`).
- Status and progress lines carry `event` with `from` and `to`. They can be deleted with `notes_delete` but not edited.

## Linking the real title

1. `works_search` with the topic's name and `kind` (book, movie, tv, game, music, podcast, app).
2. Pick the matching result with the user when it is not obvious.
3. `topics_link_work` with `provider`, `externalId` → `external_id`, `kind`, `title`, `year` copied exactly. It replaces an earlier link.
