---
name: soolist-rate
description: Rates something in Soolist in one call — by list and name, adding the topic when the list does not have it yet. Use when the user wants to rate, score, log, or review a movie, book, game, meal, place, or any other topic. The experience date is optional.
---

# Rate something

## Quick start

1. Follow `soolist-session` first.
2. `categories_list` (`owner_scope: own`, `query` = the type) gives the list, its scale and the names of its dimensions. If it is missing, create it (`soolist-lists`).
3. Confirm the scores and the date with the user.
4. `ratings_create` with `category_id` + `topic_name` and the scores. The topic is found on the list by name, or added when it is not there. Dimensions can be named (`{"id": "Story", "score": 8}`).
   - A link the user pasted (IMDb, Goodreads, Steam, YouTube, a store…) goes in `link`: it names the topic and links it to that exact title with its cover.
   - Otherwise, for a new real-world title (a film, book, game, album…), `works_search` first and pass the result's `provider` and `externalId` as `work_provider` and `work_external_id`.
   - When the user means an existing topic you already have, pass `topic_id` instead.

Read [Rating flow](references/rating.md) before the first write.

## Hard boundaries

- The same topic can be rated more than once with different `experienced_at` dates. An existing rating is not a blocker.
- Use `ratings_create` for a new score. Omit `experienced_at` when they do not remember the date. Use `ratings_update` only when the user wants to change a specific existing rating (`ratings_list` finds it).
- When the list has dimensions, send one score per dimension. When it has none, send `overall_score`.
- Scores sit on that list's scale (`scaleMin`–`scaleMax`). On scales of ten steps or fewer one decimal is allowed (7.5, 7.9); on longer scales such as 0–100 only whole numbers. 0 is valid only when `scaleMin` is 0.
- Several things to add without scores (a reading list) → `topics_add_many`, with `status: planned` when they are plans.
- Confirm deletes (`ratings_delete`, `topics_delete`) out loud. Creating a rating does not need a second confirmation once the user stated the scores.

## Asking well

Ask one compact question for anything still open:

> Which list should this go in — Movies or a new one? And what date did you watch it?

Do not ask field-by-field. Do not name tool arguments.

## Handover

- New list or dimensions → `soolist-lists`.
- Put it on a shelf → `soolist-collections`.
- Shared workspace list → `soolist-spaces`.
- Started, finished, or partway through it → `soolist-track`.
- A longer thought or quote to keep → `soolist-notes`.
- A picture of the rating to share → `share_image_create` with `kind: rating`.
