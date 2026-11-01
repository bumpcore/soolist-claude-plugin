# Browse scopes

Use these `owner_scope` values on `categories_list`, `topics_list`, and `collections_list`.

| Scope | What it returns |
|---|---|
| `own` | The signed-in user's personal content |
| `friends` | Friends' visible content only |
| `spaces` | Content in spaces the user belongs to |
| `user_owned` | Personal content for the user plus friends (no spaces) |
| `accessible` | Everything the user can see |

Optional filters:

- `query` — name/description search
- `owner_username` — one person's personal lists/topics/collections
- `space_id` — one space (with `owner_scope: spaces` or `accessible`)
- `category_id` — topics on one list
- `rated_by_viewer` — topics the signed-in user has already scored

Open a single result with `categories_show`, `topics_show`, `collections_show`, or `spaces_show` before talking about dimensions or scores.
