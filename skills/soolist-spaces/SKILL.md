---
name: soolist-spaces
description: Works with Soolist spaces — shared places such as a film club or a family, with their own lists, collections and members. Use when the user mentions a club, workspace or shared list, wants to start one, invite or remove people, join with an invitation or a link, or leave one.
---

# Spaces

A space is a shared place with members (owner, admins, members). Lists and collections created with `space_id` belong to that space, not the personal account.

## Quick start

1. Follow `soolist-session`.
2. `spaces_list` shows the user's spaces and the invitations waiting for them. If several match, ask.
3. Pick the path:
   - What is inside → `spaces_show`, then search with `space_id` (`categories_list`, `topics_list`, `collections_list`) or read its activity with `feed_list` (`space_id`).
   - Add content → `categories_create` / `collections_create` with `space_id`; rate on a space list with `soolist-rate`.
   - Start one → `spaces_create`; change it → `spaces_update`.
   - People → `spaces_members_list`; invite by username → `spaces_invite`; a link to share in a chat → `spaces_invite_link_create`; change a role → `spaces_members_update`; remove someone → `spaces_members_remove`.
   - The user's own membership → `spaces_join` (an invitation from `spaces_list`, or a link someone shared), `spaces_decline`, `spaces_leave`.

## Hard boundaries

- Only owners and admins invite, change roles or remove members. The owner cannot leave.
- `spaces_delete` deletes the space with everything in it for good — no trash. Name what will be lost and get a clear yes first.
- Do not put personal content in a space unless they asked.
- Prefer `visibility: space_members` for new space lists and shelves unless they asked otherwise.

## Handover

- Personal list instead of a space → `soolist-lists`.
- Rate a topic already on a space list → `soolist-rate`.
