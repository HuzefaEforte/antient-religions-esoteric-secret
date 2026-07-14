# Wiki Log

Append-only, chronological record of what happened and when. Newest entries at the
bottom. Every entry header uses a fixed prefix so the log is greppable:

```
grep "^## \[" wiki/log.md | tail -5
```

Header format — `## [YYYY-MM-DD] <op> | <title>` where `<op>` is one of
`ingest` · `query` · `lint` · `merge` · `meta`.

---

## [2026-07-14] meta | Wiki initialized
- Created the schema in `CLAUDE.md` for a wiki on **ancient religions & esoterica**.
- Scaffolded `raw/` (immutable sources, with `raw/assets/` for images) and `wiki/`
  (`sources/`, `entities/`, `concepts/`, `synthesis/`).
- Created `wiki/index.md` (catalog), `wiki/log.md` (this file), and a stub
  `wiki/overview.md`.
- Source mix planned: LLM chat exports & research, web clips, academic papers/books,
  images/scans, and notes/transcripts.
- Awaiting the first source in `raw/`.
