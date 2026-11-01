# List editing

## Presets

Call `presets_list` and copy keys from the response. Starter keys:

| What the user says | `preset` | Default scale |
|---|---|---|
| Movies | `movie` | 10 |
| Shows / series | `show` | 10 |
| Games | `game` | 10 |
| Books | `book` | 10 |
| Food / restaurants | `restaurant` | 10 |
| Places / hotels | `hotel` | 5 |

- Omit `dimension_keys` to keep the core set.
- Pass extra keys from `presets_list` when the user wants optional axes (Acting, Soundtrack, …).
- `name` overrides the localized preset name when the user wants a custom title.

## Custom lists

Without `preset`, `categories_create` needs `name`. Optional: `rating_scale` (highest score, 2–100; default 10), `rating_scale_min` (`0` or `1`; default `1`), `dimensions` as `{ name, weight }` (weight 1–10), `visibility`, `description`.

## Updating dimensions

1. `categories_show` and copy every existing dimension `id`.
2. Build the full replacement list:
   - keep an axis → include its `id`, `name`, `weight`
   - rename an axis → same `id`, new `name`
   - add an axis → omit `id`
   - drop an axis → leave it out; keep `dimension_history_policy: preserve` unless the user asked to delete old scores
3. `categories_update` with that `dimensions` array.

Never send only the new axes. A partial list silently removes the rest.

## Visibility

`private` (default), `friends`, `unlisted`, `everyone`, `space_members`. Raise it only when the user asks.
