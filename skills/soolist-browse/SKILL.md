---
name: soolist-browse
description: Looks around Soolist and keeps up with friends — what friends rated lately, someone's profile, finding a person or a list, reacting to a friend's rating, and handling friend requests. Use when the user asks what a friend rated or thinks, what is new, who someone is, or wants to add, accept or remove a friend.
---

# Browse and friends

## Quick start

1. Follow `soolist-session`.
2. Pick the path:
   - What is new, what friends did lately → `feed_list` (or one space's with `space_id`).
   - Find anything by name → `search`; a topic, list or collection → its `*_show`.
   - A person → `profiles_show` with their `username` (their lists, showcase and latest ratings the user may see).
   - Friends and requests → `friends_list` (with `query` to find someone to add), then `friends_request`, `friends_accept`, `friends_decline` or `friends_remove`.
   - React to a friend's rating or note → `reactions_set` with the `reactions` target from `feed_list`; take it back with `reactions_remove`.

Read [Browse scopes](references/browse.md) when searching with `owner_scope`.

## Hard boundaries

- `owner_scope: friends` returns nothing when the user has no friends. That is correct — do not fall back to strangers.
- Never invent usernames. Use one only after the user named someone, or after a result showed it.
- Do not edit a friend's or public list. If `update`/`delete` is denied, say they can only view it.
- A friend's private list is not visible. If search is empty, say you cannot see it — do not imply it does not exist.
- Friend requests, removals and reactions reach another person: say what you are about to do before you do it.

## Asking well

> Do you want your own Movies list, or to look at what a friend rated?

## Handover

- Copy a topic you found into the user's own list or space → `topics_copy`.
- Rate something you found → `soolist-rate`.
- Recommend it to a friend → `soolist-recommend`.
- How their taste compares with someone's → `soolist-taste`.
- Read or reply to what people wrote on a topic → `soolist-notes`.
