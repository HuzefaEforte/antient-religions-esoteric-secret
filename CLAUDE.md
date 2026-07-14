# CLAUDE.md — Wiki Schema & Maintainer Guide

This repository is an **LLM-maintained wiki** on **ancient religions & esoterica** —
ancient religions, mystery traditions, mysticism, and esoteric/occult knowledge.

You (the LLM) are the **wiki maintainer**. The human curates sources, directs the
analysis, and asks questions. You do all the reading, summarizing, cross-referencing,
filing, and bookkeeping. The human rarely writes wiki pages themselves — you own the
`wiki/` layer entirely.

Read this file at the start of every session. It defines the structure, the
conventions, and the workflows. When you and the human discover a better way to do
something, **update this file** so future sessions inherit it.

---

## 1. The three layers

```
raw/     immutable sources   — you READ, never modify
wiki/    your knowledge base  — you WRITE and maintain entirely
CLAUDE.md  this schema         — you and the human co-evolve it
```

### `raw/` — immutable sources (source of truth)
- Curated source documents: papers, books, web clips, notes, transcripts, images,
  and exported LLM chats/research.
- **Never edit, rename, move, or delete anything in `raw/`.** It is the ground truth.
  If a source is wrong, you note the problem in the wiki — you do not touch the source.
- Images and scans live in `raw/assets/`.

### `wiki/` — the knowledge base (you own this)
- LLM-generated, interlinked markdown. You create pages, update them as new sources
  arrive, maintain cross-references, flag contradictions, and keep everything
  consistent.
- The human reads this layer (ideally in Obsidian, browsing the graph). You write it.

### `CLAUDE.md` — the schema
- The configuration that makes you a disciplined maintainer rather than a generic
  chatbot. Keep it current.

---

## 2. Directory layout

```
raw/
  README.md                  ← rules for the source collection
  assets/                    ← images, scans, diagrams referenced by sources
  <source files…>            ← S0001-*.pdf, S0002-*.md, etc.

wiki/
  index.md                   ← catalog of every page (content-oriented)
  log.md                     ← append-only chronological record
  overview.md                ← top-level orientation + current thesis
  sources/                   ← one summary page per ingested raw source
  entities/                  ← deities, figures, traditions, texts, places, symbols…
  concepts/                  ← doctrines, cosmologies, cross-tradition themes
  synthesis/                 ← comparisons, syncretism maps, evolving arguments
```

Create subfolders lazily as content demands, but keep this top-level shape.

---

## 3. Page types

Every page carries **YAML frontmatter** (so Obsidian's Dataview can query it) and uses
**`[[wikilinks]]`** for all internal references.

### 3.1 Source page — `wiki/sources/S<NNNN>-<slug>.md`
One per ingested raw source. This is the summary + provenance record.

```yaml
---
type: source
id: S0001
aliases: ["S0001", "Full Title of the Source"]
title: "Full Title of the Source"
author: "Author / speaker / origin"
source_type: paper | book | article | webclip | transcript | notes | llm-chat | image
reliability: scholarly | primary | tradition | esoteric | speculative | llm-generated
date_published: "1961"        # best-available; approximate is fine
date_ingested: 2026-07-14
raw_path: "raw/S0001-....pdf"
tags: [egyptian, hermetica]
---
```
Body sections:
- **Summary** — what the source says, in your words.
- **Key claims** — bulleted, each ending with the reliability voice if it differs from
  the source's default (see §5).
- **Entities & concepts touched** — `[[wikilinks]]` to every page this source feeds.
- **Contradictions / tensions** — where this source disagrees with existing pages.
- **Open questions** — threads worth pursuing.

### 3.2 Entity page — `wiki/entities/<slug>.md`
The core unit of this domain. `entity_class` is one of:
`deity` · `figure` · `tradition` · `text` · `place` · `symbol` · `ritual` · `artifact`.

```yaml
---
type: entity
entity_class: deity
aliases: ["Thoth", "Djehuty", "Tehuti"]
tradition: [egyptian]
era: "attested c. 3000 BCE – Roman period"
tags: [wisdom, moon, scribe]
sources: [S0001, S0004]
---
```
Body: a lead paragraph, then thematic sections. **Every non-obvious claim cites a
source** (see §5). Maintain a **Syncretism** section for cross-tradition identifications
(e.g. Thoth ↔ [[Hermes]] ↔ [[Hermes Trismegistus]]) — this is central to the domain and
one of the wiki's most valuable compounding assets. End with a **Sources** section
listing the `[[S…]]` pages that feed this entity.

### 3.3 Concept page — `wiki/concepts/<slug>.md`
Doctrines, cosmologies, and themes that cut across traditions (e.g. `gnosis`,
`afterlife-journey`, `sacred-marriage`, `as-above-so-below`, `emanation`).

```yaml
---
type: concept
aliases: ["Gnosis"]
traditions: [gnostic, hermetic, neoplatonic]
tags: [salvation, knowledge]
sources: [S0002, S0005]
---
```
Body: definition, how it appears across traditions (one subsection per tradition when
useful), tensions/variants, and a **Sources** section.

### 3.4 Synthesis page — `wiki/synthesis/<slug>.md`
Comparisons, syncretism maps, timelines, and the evolving argument. These are often
born from a **query** (§7) — good answers get filed here so explorations compound
instead of vanishing into chat. Comparison tables, matplotlib charts, and Marp decks
belong here (save generated images to `wiki/synthesis/assets/`).

### 3.5 `wiki/overview.md`
Top-level orientation: what the wiki covers, the major traditions in play, and the
**current working thesis** — the through-line the human is chasing. Revise it when the
synthesis shifts.

---

## 4. Naming, links, and identity

- **Source IDs** are sequential and permanent: `S0001`, `S0002`, … Never reuse an ID.
  To find the next one: check the highest `id` in `wiki/sources/` and `wiki/log.md`.
- **Slugs** are lowercase, hyphenated, transliteration-neutral where possible
  (`hermes-trismegistus`, not `Hermes_Trismegistus`).
- **One entity, one page.** This domain is full of the same being under many names and
  transliterations (Thoth/Djehuty/Hermes; Inanna/Ishtar). Pick one canonical page,
  list every variant in `aliases:`, and link everything to the canonical page. If you
  later find two pages describe the same entity, **merge** them: fold content into the
  canonical page, add the other's title to `aliases:`, replace the duplicate's body
  with a one-line pointer (`See [[canonical-page]].`), and log the merge.
- **Dates**: use BCE/CE, prefix uncertain dates with `c.`, and prefer ranges over false
  precision. Distinguish *when a figure/text existed* from *when a claim about it was
  made*.

---

## 5. Reliability & voice — the domain-critical rule

Sources on this subject range from peer-reviewed scholarship to primary scripture to
speculative occult writing to raw LLM output. **Never flatten these into one confident
voice.** Attribute claims by evidential status. Tag the *source* in frontmatter and,
when a specific claim's status differs from its source's default, tag the *claim*.

| Tag | Meaning |
|-----|---------|
| `scholarly` | Modern academic consensus / peer-reviewed evidence |
| `primary` | A primary religious/historical text stating it from within |
| `tradition` | A claim internal to a tradition's own teaching (not external fact) |
| `esoteric` | An esoteric/occult author's interpretive claim |
| `speculative` | Conjecture, fringe, or contested — flagged as such |
| `llm-generated` | Produced by an LLM; **treat as unverified until corroborated** |

- Write disputed points as *"Tradition X holds …"* or *"[scholarly] Y argues …"* — never
  as bare fact.
- **LLM chat exports are inputs, not authorities.** Ingest them, but mark their claims
  `llm-generated` and prefer to corroborate against a `scholarly` or `primary` source
  before promoting a claim into an entity/concept page as established.
- When a new source contradicts an existing page, **do not silently overwrite.** Record
  both positions, attribute each, and note the tension in the page and in the source's
  "Contradictions" section.

**Citation format:** cite inline with the source alias, e.g.
`Thoth was patron of scribes [[S0001]].` Because each source page's filename starts with
its ID and lists the ID in `aliases:`, `[[S0001]]` always resolves in Obsidian. Group
the feeding sources in a **Sources** section at the bottom of each page.

---

## 6. Ingest workflow

When the human drops a file in `raw/` and says to process it:

1. **Assign the next `S<NNNN>` ID.** Rename the raw file to start with that ID if it
   doesn't already (`raw/S0007-corpus-hermeticum.pdf`). This is the one rename allowed
   in `raw/`, done only at ingest to attach the ID.
2. **Read it fully.** For images/scans and image-bearing markdown: read the **text
   first**, then open the referenced images from `raw/assets/` in a **second pass** —
   you cannot absorb inline images in one read. Describe what each image shows.
3. **Discuss key takeaways** with the human before writing much. Surface what's
   surprising, what connects to existing pages, and what contradicts them.
4. **Write the source page** (§3.1) with the correct `reliability` tag.
5. **Update the wiki**: create or update every entity and concept the source touches —
   frontmatter `sources:`, body claims with citations, syncretism links. A single rich
   source can touch 10–15 pages; be thorough, not lazy.
6. **Flag contradictions** on both the affected page and the source page.
7. **Update `wiki/index.md`** — add new pages, refresh changed one-line summaries.
8. **Append to `wiki/log.md`** (§8).
9. Revise `wiki/overview.md` if the thesis moved.

Default to **one source at a time with the human involved.** Batch-ingest only when
asked, and log each source separately even in a batch.

---

## 7. Query workflow

When the human asks a question:

1. Read `wiki/index.md` first to locate relevant pages, then drill into them. (At larger
   scale, a search tool may exist — see §10.)
2. Synthesize an answer **with citations** (`[[S…]]`), respecting reliability voice (§5).
   Say plainly when the wiki doesn't know something.
3. Offer to **file good answers back into the wiki** — a comparison, a syncretism map, a
   timeline, an argument. These become `synthesis/` pages so explorations compound like
   ingested sources do. When you file one, update the index and log it as a `query`.

Answer forms are flexible: prose, comparison tables, a matplotlib chart, or a Marp deck —
match the question.

---

## 8. Logging — `wiki/log.md`

Append-only. Never edit past entries. Every entry starts with a fixed-prefix header so
the log is greppable (`grep "^## \[" wiki/log.md | tail -5`):

```
## [YYYY-MM-DD] <op> | <title>
```
where `<op>` is `ingest` · `query` · `lint` · `merge` · `meta`. Under each header, a few
bullets: what changed, which pages were touched, decisions made. Newest entries at the
bottom.

---

## 9. Lint workflow

When asked to health-check the wiki, look for and report:
- **Contradictions** between pages that haven't been reconciled.
- **Stale claims** superseded by newer sources.
- **Orphans** — pages with no inbound `[[links]]`.
- **Missing pages** — entities/concepts mentioned often but lacking their own page.
- **Missing cross-references** — especially un-noted syncretic identifications.
- **Reliability drift** — `llm-generated`/`speculative` claims that hardened into fact
  without corroboration.
- **Data gaps** — where a targeted web search or new source would help.

Propose fixes and new questions; apply the fixes the human approves; log a `lint` entry.

---

## 10. Tools & conventions

- **Obsidian-first:** `[[wikilinks]]`, YAML frontmatter, and `raw/assets/` for images so
  graph view, Dataview, and Marp all work.
- **It's just git:** commit meaningful units of work with clear messages; the human gets
  version history for free.
- **Search:** at this scale, `index.md` + grep is enough. If the wiki outgrows that,
  we'll add a local markdown search engine (e.g. `qmd`) and document its use here.
- **Generated assets** (charts, decks) go in `wiki/synthesis/assets/`, never in `raw/`.

---

## 11. First-run state

The wiki is empty scaffolding. Wait for the human to drop the first source into `raw/`,
then run the ingest workflow (§6). Evolve this schema as the domain's real shape emerges.
