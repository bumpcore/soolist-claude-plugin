# Smart shelves

A smart shelf has no hand-picked topics. Its `rules` choose from the owner's topics (their own, or the space's for a space shelf) every time it is opened.

## Rules

Every rule you send narrows the shelf; leave out what the user did not ask for.

| Rule | Meaning |
|---|---|
| `kinds` | Lists of these kinds: `book`, `movie`, `tv`, `game`, `music`, `podcast`, `app`, or `other` (lists without a kind) |
| `category_ids` | Only these lists (ids from `categories_list`, owned by the shelf owner) |
| `statuses` | Tracked as `planned`, `in_progress`, `finished`, `paused`, or `dropped` |
| `min_score` / `max_score` | Latest score as a position from 0 (the list's lowest score) to 10 (its highest), so one rule works across scales |
| `rated` | `rated` or `unrated` (default `any`) |
| `experienced_year` / `finished_year` | Rated as experienced in, or finished in, that year |
| `limit` | At most this many (1–200, default 50) |
| `sort` | `score_desc` (default), `recent`, or `random` (reshuffled daily) |

## Examples

- "My best books" → `kinds: ["book"]`, `min_score: 8`.
- "Games I finished in 2025" → `kinds: ["game"]`, `finished_year: 2025`.
- "My watchlist" → `kinds: ["movie", "tv"]`, `statuses: ["planned"]`, `sort: "random"`.

## Editing

- `collections_update` with `rules` replaces all rules — send the full set you want, not only the change.
- `is_smart: true` with `rules` turns a hand-picked shelf smart; its picked topics are kept but hidden. `is_smart: false` brings them back.
- `collections_show` lists what the rules match right now. Scores and statuses come from the owner; on a space shelf, from the viewer.
- Visitors only see matching topics they are allowed to see.
