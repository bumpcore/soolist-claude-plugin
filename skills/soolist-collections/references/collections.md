# Collection flow

## Create

- `collections_list` (`owner_scope: own`, `query` = the name) so you do not duplicate.
- `collections_create`: `name` required. `sort_mode` is `manual` unless the user wants the shelf ordered by score (`rating_desc` / `rating_asc`). Optional `preset` (`classic`, `podium`, `verdict`) defines the tier view up front; it does not change list order.
- Default visibility is `private`. List and tier views coexist on every collection.

## Attach / detach

1. Resolve each topic with `topics_list` or `topics_show`. If the name is ambiguous, ask.
2. `collections_topics_attach` with the collection `id` and `topic_ids`. Already-attached topics are skipped.
3. `collections_topics_detach` takes the same shape and only unshelves — it never deletes the topic or its ratings.

## Inspect

`collections_show` returns the shelf and both views: list order (`sorting`) and tier placement (`tierKey`, `tierSorting`). `defaultView` is the owner's preferred starting view. Use it after attach/detach to confirm the result, then summarize names — not ids — to the user.
