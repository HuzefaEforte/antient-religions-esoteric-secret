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

## [2026-07-14] ingest | S0001 — Ancient Religions' Esoteric Secrets Revealed
- Ingested first source: a ~60-turn **Gemini chat export** (`source_type: llm-chat`,
  `reliability: llm-generated`). Renamed raw file → `raw/S0001-ancient-religions-esoteric-secrets.md`.
- Read fully (text + a second pass on all **9 embedded base64 images**). Catalogued the images;
  flagged two as **mislabeled** ("ancient" Boehme/Freher engraving; the alchemical "Hand of the
  Philosopher") and identified image 2 as a genuine Persian ʿIrfan scan, image 7 as a modern UML of
  al-Farabi's cosmology.
- Curator decisions at ingest: **full build (~20+ pages)**; **contain & flag** the
  wealth/manifestation/semen-retention/suicide material (no standalone concept pages).
- Wrote the source page + **30 wiki pages total**:
  - Concepts (12): [[non-duality]], [[emanation]], [[drama-in-heaven]], [[tawil]],
    [[wahdat-al-wujud]], [[fana]], [[four-states-of-consciousness]], [[maya]], [[atman-brahman]],
    [[the-observer]], [[seven-hermetic-principles]], [[dream-interpretation]].
  - Entities (15): figures [[al-hallaj]], [[ibn-arabi]], [[rumi]], [[al-farabi]], [[ibn-sina]],
    [[plotinus]], [[imam-hussain]], [[hermes-trismegistus]]; traditions [[sufism]],
    [[advaita-vedanta]], [[tayyibi-ismailism]], [[hermeticism]]; texts [[upanishads]], [[kybalion]];
    symbol [[ouroboros]].
  - Synthesis (2): [[islam-hindu-esoteric-parallels]] (core comparison table) and
    [[perennialism-and-modern-overlay]] (reliability quarantine for the speculative/self-help layer).
- Every claim tagged by reliability voice; contradictions (tradition conflation, anachronistic
  images, "science proves it" claims, Karbala history vs. esoteric reading) recorded on the source
  page and affected pages.
- Updated `wiki/index.md` (counts + full catalog) and `wiki/overview.md` (working thesis: non-duality
  as claimed common core, held with caution).
- Seeded a syncretism hub on [[hermes-trismegistus]] (Thoth↔Hermes) for future expansion.
- Open threads: corroborate the Tayyibi/Corbin attribution, the al-Hallaj reading, and the
  Perennialism claim with `scholarly`/`primary` sources; ~15 book recommendations noted as
  candidate future sources (Corbin, Plotinus, Kirmani, Ibn ʿArabi, etc.).
