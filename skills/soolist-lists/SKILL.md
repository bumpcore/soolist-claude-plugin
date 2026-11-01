---
name: soolist-lists
description: Creates and maintains Soolist lists (categories) and their rating dimensions, and tidies what is on them — moving topics between lists, merging duplicates, and the trash. Use when the user wants a new list, to change a scale or dimensions, to move or merge topics, or to get something deleted back.
---

# Lists

A list is a category with a score range and optional weighted dimensions. Topics live inside a list and share that scale.

## Quick start

1. Follow `soolist-session`.
2. `categories_list` (`owner_scope: own`) before creating a duplicate name.
3. Prefer `presets_list` + `categories_create` (`preset`, optional `dimension_keys`) for Movies, Shows, Games, Books, Restaurants, or Hotels.
4. `categories_show` before editing dimensions so existing axis ids are preserved.

Read [List editing](references/lists.md) before changing dimensions or deleting a list.

## Hard boundaries

- Do not create a second personal list with the same name unless the user asks.
- `categories_update` with `dimensions` replaces the scale axes. Include each existing dimension `id` you want to keep.
- `dimension_history_policy` is `preserve` unless the user wants old scores on removed axes deleted (`remove`).
- `categories_delete` removes the list, its topics, and their ratings. Confirm first.
- Space lists need `space_id` from `spaces_list`. Follow `soolist-spaces`.

## Tidying

- Move topics to another list → `topics_move`. Notes and statuses move along, but their ratings are deleted for good (a rating belongs to its list's scale): say so and get a yes first.
- The same thing added twice → `topics_find_duplicates`, then `topics_merge` (the duplicate's ratings and notes move to the kept topic; the duplicate goes to the trash).
- Something deleted → `trash_list`, then `trash_restore`. A delete or merge answers with the trash id to restore at once.
- `trash_delete` deletes for good. Only when the user asks for exactly that.

## Naming

Talk about “lists” with the user. “Category” stays inside tool arguments.

## Handover

- Rate a topic on the list → `soolist-rate`.
- Shared workspace → `soolist-spaces`.
