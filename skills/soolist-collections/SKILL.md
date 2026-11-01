---
name: soolist-collections
description: Builds and edits Soolist collections — curated shelves of topics, not rating lists — including smart shelves that fill themselves from rules. Use when the user wants a shelf, a ranked list, a watch later pile, a "best of" that keeps itself up to date, or to add or remove topics from one.
---

# Collections

A collection is a shelf of topics. Scores still live on the topic's list.

## Quick start

1. Follow `soolist-session`.
2. `collections_list` before creating a duplicate name.
3. `collections_create` for a new shelf (`sort_mode`: `manual`, `rating_desc`, or `rating_asc`).
4. Resolve topic ids with `topics_list` / `topics_show`, then `collections_topics_attach`.
5. `collections_topics_detach` removes a topic from the shelf only.
6. `collections_reorder` sets the order of a hand-sorted shelf.

## Tier lists

A shelf with `layout: tiers` has its own tiers (S, A, B… or Must see, Maybe, Skip).

- `collections_update_tiers` replaces the tiers, best first. Keep a tier's `key` to keep its topics.
- `collections_seed_tiers` places every topic by the user's latest score; `collections_set_tier` moves one.
- `share_image_create` with `kind: collection` makes an image of the shelf to share.

Read [Collection flow](references/collections.md) before the first attach.

## Smart shelves

For "my 8+ books", "games I finished in 2025", or "everything I plan to watch", create the shelf with `is_smart: true` and `rules` instead of attaching topics. It fills itself with the owner's topics that match, now and later. See [Smart shelves](references/smart.md).

## Hard boundaries

- Never use `collections_create` when the user wants a rating list — that is `soolist-lists`.
- Do not invent topic ids. Attach only ids returned by list/show.
- `collections_delete` deletes the shelf, not the topics. Confirm first.
- Space shelves need `space_id` from `spaces_list`. Follow `soolist-spaces`.
- Smart shelves cannot be curated by hand: attach, detach, and tiers are refused. Change their `rules` with `collections_update` instead.

## Handover

- The user wants to score something on the shelf → `soolist-rate`.
- The user wants a new scoring list → `soolist-lists`.
