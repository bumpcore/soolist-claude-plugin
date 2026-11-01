---
name: soolist-recommend
description: Sends and answers recommendations between friends on Soolist — recommend a topic to friends with a note, see what friends recommended to the user, add a recommendation to their own list, or set it aside. Use when the user wants to tell a friend about something, or asks what friends recommended to them.
---

# Recommendations between friends

## Quick start

1. Follow `soolist-session`.
2. Recommending: find the topic (`topics_list` or `search`), then `recommendations_friends` for who can receive it.
3. Answering: `recommendations_list`, then `recommendations_accept` or `recommendations_dismiss`.
4. Say what happened in one sentence, by name ("Sent Dune to Ayşe").

## Tool path

| The user says | Tool |
|---|---|
| "Recommend Dune to Ayşe", "tell Can about this" | `recommendations_friends`, then `recommendations_send` with their usernames |
| "What did my friends recommend?" | `recommendations_list` |
| "Add Ayşe's recommendation to my books" | `recommendations_accept` with `suggestedCategoryId` or a list they name |
| "Not interested in that one" | `recommendations_dismiss` |

## Hard boundaries

- Only friends who can see the topic and do not have it already can receive it. If a friend is missing from `recommendations_friends`, say why instead of retrying.
- A private topic cannot be recommended. Offer to change its visibility only if the user asks.
- Confirm the recipients and the note wording before `recommendations_send`; each friend is notified. At most 20 a day.
- `alreadySent: true` means it is still waiting with that friend — do not send it again.
- Accepting adds the topic to the user's list as planned and remembers who recommended it. When `suggestedCategoryId` is null, ask which list, or create one with `soolist-lists`.
- Dismissing cannot be undone and the friend is not told. Confirm first.

## Handover

- They finished a recommended topic and want to score it → `soolist-rate`.
- "Who else might like this?" or taste match with a friend → `soolist-taste`.
