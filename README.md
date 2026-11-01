# Soolist for Claude

![Soolist](assets/icon.png)

[Soolist](https://soolist.com) is where you keep what you watch, read, play, eat and visit: rated on scales you
design yourself, with weighted dimensions, organised in categories and collections, and shared with friends and in
spaces. This plugin connects Claude to your own Soolist account, so you can ask in plain words:

- "Rate the film I just watched an 8, with a note."
- "What did I rate highest this year?"
- "Make a collection of my favourite sci-fi books."
- "I'm on episode 5 of Severance."
- "Based on my taste, what should I watch next?"

## What it includes

- **The Soolist connector** (`.mcp.json`): Soolist's remote MCP server at `https://mcp.soolist.com/`.
- **Skills** (`skills/`): playbooks that show Claude how to work with Soolist well.
  - `soolist-session`: who you are acting as, your language, ids, and how to load the other playbooks.
  - `soolist-rate`: find or create the list and topic, then save a dated score.
  - `soolist-lists`: create and edit rating lists (categories) and their dimensions.
  - `soolist-collections`: curated shelves of topics, and smart shelves that fill themselves from rules.
  - `soolist-spaces`: work inside a shared space you already belong to.
  - `soolist-browse`: look at friends' and public lists, topics and collections.
  - `soolist-track`: status and progress, linking the real title, and a random pick of what to do next.
  - `soolist-notes`: a topic's notes, replies and @mentions.
  - `soolist-taste`: your taste profile, taste comparison with another person, and people you may know.
  - `soolist-recommend`: recommend topics to friends and answer their recommendations.
  - `soolist-stats`: stats for a period and the yearly recap.

The plugin contains no code that runs on your computer: only Markdown playbooks and the connector's address.

## Install

In Claude Code:

```
/plugin install soolist --marketplace bumpcore/soolist-plugin
```

## Connecting

The first time Claude uses Soolist, it asks you to sign in to Soolist and allow access (OAuth, scope `mcp:use`).
You need a Soolist account; it is free at [soolist.com](https://soolist.com). Step-by-step instructions for Claude on
the web, desktop, phone and Claude Code: [soolist.com/help/connect-claude](https://soolist.com/help/connect-claude).

## Data and privacy

When you ask for something, Claude sends the request (for example a title, a score, a note or a search) to
Soolist's server at `mcp.soolist.com`, which reads or changes your Soolist account and answers with the result. The
plugin sends nothing anywhere else. Soolist only reaches what your account can see, never asks Claude for your
conversation, and keeps what you save under its [privacy policy](https://soolist.com/privacy) and
[terms](https://soolist.com/terms). You can disconnect at any time from Claude's connector settings or from your
Soolist account settings.

## Support

Questions or problems: [soolist.com/contact](https://soolist.com/contact), or open an issue in this repository.
