---
name: soolist-track
description: Tracks where the user is with a topic in Soolist — planned, started, on episode 5, finished, paused, dropped — links it to the real book, film, series or game it is about, and picks something to do next at random. Use when the user says they started, finished, gave up on, or are partway through something, or cannot decide what to do next.
---

# Track progress

## Quick start

1. Follow `soolist-session` first.
2. Find the topic with `topics_list` (`owner_scope: own`, `query` = the name). If it is missing, create it (`soolist-rate` steps 2–3).
3. Call `topics_show`: `tracking` is their current status and progress, `work` the real-world title (with `totalUnits` when known).
4. Write with the matching tool below, then say what changed in one sentence.

Read [Tracking details](references/track.md) for status rules and examples.

## Tool path

| The user says | Tool |
|---|---|
| "I want to watch / read …", "add to my plans" | `topics_set_status` `planned` |
| "I started …", "picked it back up" | `topics_set_status` `in_progress` |
| "I finished …" | `topics_set_status` `finished`, then offer to rate it (`soolist-rate`) |
| "I paused / gave up on …" | `topics_set_status` `paused` / `dropped` |
| "I'm on episode 5", "page 120 of 400" | `topics_update_progress` with `current` (+ `total`, `unit` the first time) |
| "watched two more", "one more chapter" | `topics_update_progress` with `step` |
| A thought, quote, or where they left off | `notes_create` (`soolist-notes`) |
| "What did I write?", "when did I start?" | `notes_list` (`soolist-notes`) |
| "What am I in the middle of?" | `topics_list` with `status: in_progress` |
| "This is the 2021 Dune film" | `works_search`, then `topics_link_work` |
| "What should I watch / read next?", "pick something" | `topics_pick_random` (`kind` or `category_id` to narrow; `except_topic_id` for another), then `topics_set_status` `in_progress` if they take it |

## Hard boundaries

- Tracking is only for the user's own topics and their spaces' topics. On a friend's or public topic, the answer is a shared note (`soolist-notes`) — do not retry.
- Progress moving forward starts the topic; reaching the total finishes it. Do not also call `topics_set_status` for the same change.
- Never send `current` and `step` together. Use `total` only when the user said it or `work.totalUnits` shows it.
- Status and progress changes appear in the topic's notes, shared or private like the user's notes (`permissions.defaultVisibility` in `notes_list`).
- `topics_link_work` takes the `provider` and `externalId` of a `works_search` result. If several titles fit (remake, adaptation, same name), ask which one — show title, year and creator.

## Handover

- Finished and want to score it → `soolist-rate`.
- A note about it, or talk with friends about it → `soolist-notes`.
