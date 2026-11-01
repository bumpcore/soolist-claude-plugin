---
name: soolist-notes
description: Reads and writes the notes on a Soolist topic — the user's own thoughts, quotes and where they left off (shared or private), what friends wrote, replies, and @mentions — and edits or deletes the user's notes. Use when the user wants to jot something down about a topic, asks what they or others wrote, wants to reply to a friend, or wants to fix or remove a note.
---

# Notes

Every topic has one stream of notes. A note is either **shared** (`visibility: topic` — everyone who can see the topic reads it, and friends can reply) or **private** (`visibility: private` — only the user ever sees it). The stream also shows the user's status/progress changes and ratings.

## Quick start

1. Follow `soolist-session`.
2. Find the topic with `topics_list` (`owner_scope: own`, or `friends` for a friend's topic).
3. `notes_list` to read it. `permissions` says whether the user can write (`canPost`), keep private notes (`canPostPrivate`), and who a note is for by default (`defaultVisibility`).
4. Draft the note in the user's words, then `notes_create`.

Read [Notes details](references/notes.md) for Markdown, replies, and editing examples.

## Tool path

| The user says | Tool |
|---|---|
| A thought, quote, or where they left off | `notes_create` (omit `visibility` to use their usual choice) |
| "Just for me", "private", a personal feeling | `notes_create` with `visibility: private` |
| "Tell Deniz …", "reply to that" | `notes_create` with `parent_id` (always shared) |
| "What did I write?", "where was I?", "what did people say?" | `notes_list` |
| All replies of one note | `notes_list` with `note_id` |
| "Fix that note", "make it private", "mark it as a spoiler" | `notes_update` |
| "Delete that note" | `notes_delete` after confirming |

## Hard boundaries

- Private notes are only for the user. They can only be kept on the user's own topics and their spaces' topics — on a friend's or public topic every note is shared. Never quote a private note in a shared note, reply, or recommendation.
- A shared note is read by everyone who can see the topic. Show the exact wording and get a yes before posting it.
- Ask when a note sounds personal and the user did not say who it is for. Mark `spoiler: true` for endings and twists, and do not repeat someone else's spoiler note unless asked.
- Replies and `@username` mentions work on shared notes only. Copy usernames from notes, topics, or the user — never guess. A mention notifies only people who can see the topic.
- Edit and delete only notes whose `canEdit` / `canDelete` is true. A note people replied to stays shared, and deleting it leaves a "deleted" placeholder so the thread keeps its place.
- Deleted notes show `deleted: true` with no text. Do not speculate about what they said.
- Space topics: only members can write. If writing is refused, say so — do not retry.

## Asking well

> Want me to post "Loved the ending, @deniz — the soundtrack too!" as a reply to Deniz? Everyone who can see Dune will read it.

> Should this one be just for you, or shared with the people who can see the topic?

## Handover

- Started, finished, or on episode 5 → `soolist-track`.
- Wants to score it → `soolist-rate` (a rating has its own short note).
