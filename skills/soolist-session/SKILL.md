---
name: soolist-session
description: Handles Soolist MCP startup and orientation. Use when connecting to Soolist, starting a conversation, checking who the agent is acting as, or deciding which playbook to load.
---

# Soolist session

## Quick start

1. Call `session_orientation` at the start of a Soolist conversation.
2. State whose Soolist you are using (their name) before the first write.
3. Speak in the user's language from `locale`.
4. Follow the matching playbook below for anything more than a single lookup.

## Tool path

- `session_orientation` — signed-in name, username, locale, and personal counts.
- `search` — one search across topics, lists, collections, spaces and people, forgiving typos.
- `taste_profile_show` — a one-call summary of what the user likes, per list.
- `notifications_list` — what is new for them: requests, recommendations, reactions, replies, invitations.

## Which playbook

| User intent | Skill |
|---|---|
| Rate, score, log, or review something | `soolist-rate` |
| New list, scale, or dimensions; moving, merging, the trash | `soolist-lists` |
| Shelf, ranked pile, watch later, self-updating "best of" | `soolist-collections` |
| Clubs and shared spaces: content, members, invitations | `soolist-spaces` |
| Friends, their activity and profiles, reactions, public lists | `soolist-browse` |
| Started, finished, "on episode 5", "what next?" | `soolist-track` |
| A note or quote, where they left off, what people said, a reply | `soolist-notes` |
| What they like, taste match with someone, people they may know | `soolist-taste` |
| Recommend something to a friend, friends' recommendations | `soolist-recommend` |
| Stats, streaks, year in review | `soolist-stats` |

## Boundaries

- Every tool acts as the OAuth user. There is no tenant switch and no `viewer_username`.
- Public ids look like `dune-x7k2`. Never invent them; copy them from list/show responses.
- Talk about lists, topics, and ratings — not tables, tokens, or tool names.
- Notes, rating notes, and descriptions are Markdown and come back as stored. Private notes stay between you and the user.
- If a tool says the user must sign in, stop and tell them to connect Soolist OAuth. Do not retry with guessed credentials.
