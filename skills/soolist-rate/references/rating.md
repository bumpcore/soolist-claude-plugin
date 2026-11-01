# Rating flow

## Find or create the list

1. `categories_list` with `query` and `owner_scope: own` for a personal list.
2. If nothing fits, `presets_list`. Use `categories_create` with `preset` and optional `dimension_keys`.
3. Preset keys: `movie`, `show`, `game`, `book`, `restaurant`, `hotel`. Food is `restaurant`. Places is `hotel` (5-point scale).
4. Without a preset, `categories_create` needs `name` and may include `dimensions` (`name`, `weight` 1–10), `rating_scale` (max, 2–100), and `rating_scale_min` (`0` or `1`, default `1`).
5. Default visibility is `private`. Only raise visibility when the user asks.

## The topic

1. `ratings_create` with `category_id` and `topic_name` rates the list's topic of that name (any case), and adds it when the list has none. The answer's `topic.created` says which happened.
2. When the user may mean one of several similar topics, look first: `topics_list` with `category_id` and `query`. If several match, ask which one and pass its `topic_id`. Do not pick the closest name yourself.
3. For a new real-world title, `works_search` first (a pasted link works as the query) and pass `work_provider` and `work_external_id`, so it gets its cover.

## Score

1. `categories_list` names each list's `dimensions`; `topics_show` also gives the scale and the user's earlier ratings.
2. Each `dimension_ratings` item is `{ id, score }`; `id` is the dimension's name (Story) or its id.
3. `score` runs from `scaleMin` to `scaleMax`. On scales of ten steps or fewer one decimal is allowed (7.5, 7.9); on longer scales such as 0–100 only whole numbers. Never 8.95 or 31. 0 is valid only when `scaleMin` is 0.
4. Send a score for every dimension the list currently has. Do not invent extra axes. An unknown dimension is refused with the list's real ones, and nothing is added.
5. `experienced_at` is `YYYY-MM-DD`. Use the date the user experienced it, not today, unless they said today. Omit it or send null when they do not remember.
6. `ratings_create` adds a new score. `ratings_update` changes one existing rating id (`ratings_list` finds them, also by date). Send `experienced_at: null` to clear a date.
7. `notes` is a short Markdown note in the user's words: bold, italic, lists, quotes, links — no headings or @mentions. Longer thoughts belong in the topic's notes (`soolist-notes`).

## Afterward

- Summarize the overall score and any note in the user's language.
- Offer a collection only if they ask to shelf it (`soolist-collections`).
