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

## [2026-07-20] ingest | S0002 — The Hidden Teaching
- Ingested second source: **"The Hidden Teaching"** — a comparative essay on the esoteric core of
  the world's religions (`source_type: llm-chat`/research, `reliability: llm-generated`). Text-only,
  no images. Renamed raw file → `raw/S0002-the-hidden-teaching.md`.
- Read fully. Assessed as **more methodologically careful than S0001**: self-flags interpretive
  status, foregrounds dissent, cites the real perennialism-vs-contextualism debate. Recorded the key
  epistemic caveat everywhere: **two LLM syntheses agreeing is NOT independent scholarly
  corroboration.**
- Curator decisions: **broad build**; **dissent gets both a hub page and inline threading**.
- Wrote **20 new pages**:
  - Source page [[S0002-the-hidden-teaching]].
  - Concepts (6): [[two-truths]], [[via-negativa]], [[lila]], [[axial-age]], [[remembrance]],
    [[esoteric-decoding]].
  - Entities — traditions (5): [[kabbalah]], [[christian-mysticism]], [[gnosticism]] (cross-links
    back to S0001's Hans Jonas ref), [[buddhism]], [[taoism]].
  - Entities — figures (7): [[meister-eckhart]], [[nagarjuna]], [[isaac-luria]],
    [[pseudo-dionysius]], [[al-ghazali]], [[laozi]], [[guru-nanak]].
  - Synthesis hub (1): [[convergence-and-its-critics]] — the four shared claims, the summit-level
    disagreements (Advaita identity vs. union-with-distinction vs. Buddhist no-self), and
    perennialists (Huxley/Guénon/Schuon/Nasr) vs. contextualists (Katz).
- **Enriched 15 existing pages** with S0002 corroboration + dissent and added S0002 to their
  `sources:`: [[non-duality]], [[wahdat-al-wujud]] (+wahdat al-shuhud/Sirhindi), [[emanation]]
  (+al-Ghazali/Avicenna, Aquinas, Kabbalah), [[tawil]] (+tanzil/PaRDeS), [[the-observer]] (+eye
  pointers), [[atman-brahman]] (+four mahavakyas, anatta dissent), [[fana]], [[maya]] (+rope/snake),
  [[al-hallaj]] (+Suhrawardi/Eckhart), [[advaita-vedanta]], [[sufism]], [[upanishads]], [[ibn-sina]],
  [[islam-hindu-esoteric-parallels]], [[perennialism-and-modern-overlay]] (+perennialism/contextualism).
- Updated `wiki/index.md` (counts now 2 sources · 27 entities · 18 concepts · 3 synthesis) and
  `wiki/overview.md` (thesis broadened across traditions, now held "with its critics attached").
- Key finding: S0002 corroborates S0001's **metaphysics** but contains **none** of S0001's
  wealth/manifestation/matrix material — strengthening the case for keeping that quarantined.
- Open threads: ingest a real `scholarly`/`primary` source to actually corroborate the core and the
  dissents (candidates: Steven Katz on contextualism; a Kabbalah survey; a Nagarjuna translation;
  Henry Corbin); check whether the Axial-Age thesis still holds in current scholarship; determine
  whether S0001 and S0002 share a lineage (which would further weaken their mutual agreement).
