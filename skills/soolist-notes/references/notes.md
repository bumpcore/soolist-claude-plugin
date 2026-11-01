# Notes details

## Markdown

Note bodies are Markdown, up to 5000 characters:

- `**bold**`, `*italic*`, `~~strike~~`, `` `code` ``, `[link](https://…)`
- `## Heading` and `### Heading` (no `#` top-level heading)
- bullet (`- `) and numbered (`1. `) lists, `> quotes`
- `@username` mentions (shared notes only)

Rating notes and topic, list, and collection descriptions use the same Markdown **without headings or mentions**.

Bodies come back exactly as stored. The editor may have escaped characters (`\*`) — keep them when you edit.

## Reading the stream

- `notes_list` returns 20 items per page, newest first. Pass `nextCursor` back as `cursor` for earlier ones.
- `type: entry` items have `kind`: `note` (written), `status` or `progress` (recorded automatically, with `event.from` / `event.to`).
- `type: rating` items carry `score`, `notes`, and `experiencedAt`.
- Shared top-level notes carry `repliesCount` and their first replies (oldest first). Call `notes_list` with `note_id` for the rest.
- `visibility: private` items are always the user's own.

## Writing

- New note: `notes_create` with `topic_id` and `body`. Without `visibility`, the note follows `permissions.defaultVisibility` (the user's last choice on their own topics; always shared elsewhere).
- Reply: `notes_create` with `parent_id` set to a shared note (or one of its replies — the reply joins the same thread). Do not send `visibility: private` with a reply.

## Editing

- `notes_update` changes only the fields you send. `body` replaces the whole note: start from the stored body and change only what the user asked.
- `visibility` can switch only on the user's own top-level notes on their own or space topics, and a note with replies cannot become private.
- Status and progress lines cannot be edited, only deleted.

Examples:

- "Add a note to Severance: stopped at the elevator scene" → `notes_create` `{topic_id, body: "Stopped at the elevator scene."}`
- "Make my last Dune note private" → `notes_list`, find the user's newest `kind: note`, then `notes_update` `{id, visibility: "private"}`
- "Reply to Deniz that I agree" → `notes_list`, copy Deniz's note `id`, confirm the wording, then `notes_create` `{topic_id, parent_id, body: "Agreed, @deniz!"}`
