# raw/ — immutable sources

This folder is the **source of truth**. It holds the original documents the wiki is
built from: papers, books, web clips, notes, transcripts, exported LLM chats/research,
and images.

## Rules

- **Immutable.** These files are read, never edited, moved, or deleted. If a source is
  wrong or contradicts another, that gets noted in the `wiki/` layer — the source itself
  stays untouched.
- **The one exception:** at ingest time the maintainer prefixes a new file with its
  sequential source ID (`S0007-corpus-hermeticum.pdf`) so every source is addressable.
- **Images and scans** go in `raw/assets/`. Source pages in the wiki reference them by
  relative path.

## How to add a source

1. Drop the file in here (or clip a web article to markdown and save it here).
2. Tell the LLM to process it. It will assign the next `S<NNNN>` ID, read the file,
   discuss takeaways, and integrate it into the wiki per the ingest workflow in
   `../CLAUDE.md` (§6).

Nothing here is wired up automatically — sourcing is the human's job, ingestion is the
LLM's.
