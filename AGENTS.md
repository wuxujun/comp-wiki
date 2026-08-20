# AGENTS.md

## Project Structure & Module Organization

This repository is a Markdown-based knowledge base.

Unprocessed reference material lives under `raw/`, read-only, organized by source type:
- `raw/articles/`, `raw/docs/`, `raw/repos/`, `raw/transcripts/`

Curated content lives under `wiki/`:
- `wiki/index.md` — content-oriented master index
- `wiki/log.md` — append-only changelog of notable updates
- `wiki/concepts/` — topic/technology pages
- `wiki/comparisons/` — head-to-head evaluations
- `wiki/entities/` — people, projects, companies, tools
- `wiki/decisions/` — architecture/tooling decisions and their reasoning
- `wiki/sources/` — one structured note per ingested raw file

Lightweight navigation layer under `mocs/` (Maps of Content):
- `mocs/Home.md` — single entry point, links to all domain MOCs
- `mocs/<Domain> MOC.md` — one per theme (e.g. "RAG MOC", "Agent Frameworks MOC")

MOCs only contain links and one-line descriptions — no detailed content. This keeps the read path cheap.

## Roles

You maintain this knowledge base. The user provides raw material and asks questions.
`raw/` is read-only ground truth — never edit it. `wiki/` and `mocs/` are fully yours to
create, rewrite, and reorganize.

## Page Frontmatter

Every `wiki/` and `mocs/` page opens with:

```yaml
---
title: Page Title
type: concept | comparison | entity | decision | source | moc
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: [raw-file-1, raw-file-2]
tags: [tag1, tag2]
---
```

## MOC Creation & Maintenance Rule

MOCs are not planned upfront — they are generated incrementally as content grows.

1. `mocs/Home.md` is created on the first ingest ever run in this repo. It only lists
   domain MOCs and a short "Recently Active" section — never page-level details.
2. When a new `wiki/concepts/`, `wiki/comparisons/`, `wiki/entities/`, or `wiki/decisions/`
   page is created, check if an existing `mocs/<Domain> MOC.md` covers its topic.
   - If yes, add a one-line link to it under the correct section (Concepts / Comparisons /
     Entities / Decisions).
   - If no matching domain MOC exists and there are now 3 or more related pages without
     one, create `mocs/<Domain> MOC.md` and backfill links to all existing related pages.
3. Whenever a new domain MOC is created, add a link to it from `mocs/Home.md`.
4. After every ingest, update the "Recently Active" section in `mocs/Home.md` to list the
   5 most recently touched pages (title + relative link), dropping the oldest entry.
5. A MOC must never contain prose explanations, summaries, or detail — only a one-line
   description of scope plus links. If a MOC accumulates real content, move that content
   to a proper page and leave only the link behind.

## Ingest Workflow

Triggered when the user says "ingest this", "sync the wiki", "fold this in", or runs `/wiki-sync`.

1. Read the new file(s) under `raw/`.
2. Read `wiki/index.md` and the relevant `mocs/<Domain> MOC.md` to understand current coverage and avoid duplicating existing pages.
3. Write a source note in `wiki/sources/<slug>.md` (2-3 sentence abstract, key claims, provenance).
4. Extract concepts, entities, comparisons, and decisions worth their own page. Update existing pages before creating new ones — write "current understanding," not edit history; old content can be overwritten since `log.md` preserves the trail.
5. If a technical/architectural choice was made or changed, create or update a page in `wiki/decisions/` (context, options considered, decision, consequences).
6. Cross-link every new or updated page with related pages using relative links, e.g. `[Concept](../concepts/concept-name.md)`.
7. Update `wiki/index.md` with a one-line entry for every page touched.
8. Apply the MOC Creation & Maintenance Rule above for every page touched.
9. If new information contradicts an existing page, do not silently overwrite it — add a `## Contradictions` section presenting both versions with sources, and flag it for the user to resolve.
10. Append one line to `wiki/log.md`: `## [YYYY-MM-DD] ingest | <source> -> <pages touched>`.
11. Summarize what changed in your reply (pages created/updated, MOCs created/updated, contradictions flagged).

## Query Workflow

Triggered by any question that isn't an ingest request.

1. Start at `mocs/Home.md`, then the relevant domain MOC — never scan the whole wiki.
2. Load only the specific pages needed to answer (aim for 7 or fewer).
3. If a wiki page lacks sufficient detail, fall back to the `raw/` source referenced in its `wiki/sources/` note.
4. Answer citing which wiki page(s) informed the response, using relative links.
5. If the question surfaces a gap (no page or MOC covers it), say so instead of guessing, and offer to ingest relevant material if available. Update the wiki afterward so the same question is cheap next time.

## Maintenance Workflow

Run periodically or on request. Check for and report:
- Orphan pages (no inbound links, including from any MOC)
- Duplicate or near-duplicate pages
- Broken relative links (in pages and in MOCs)
- Stale pages (not updated in 90+ days)
- MOCs that have drifted into containing prose/detail instead of links
- Domain MOCs missing from `mocs/Home.md`
- Unresolved `## Contradictions` sections
- Decisions with no linked outcome or follow-up

## Build, Test, and Development Commands

No build system or application runtime. Work directly with Markdown files. Before submitting changes, run:

```sh
git diff --check
rg --files raw wiki mocs
```

`git diff --check` detects whitespace errors. `rg --files` confirms new content is stored in the intended directory.

## Coding Style & Naming Conventions

- One `#` heading per page, hierarchical `##`/`###` headings below it.
- Blank lines around headings, lists, and fenced code blocks.
- Prefer relative links between repository pages.
- Name files with descriptive lowercase kebab-case (`distributed-systems.md`).
- Keep `raw/` faithful to source verbatim. Rewrite `wiki/` content for clarity and your own voice — a living synthesis, not a copy.
- Every `wiki/` page opens with a 2-3 sentence self-contained summary before any detail.

## Testing Guidelines

Review every changed page in a Markdown preview. Confirm:
- Relative links resolve to real files.
- Headings are properly nested (no skipped levels).
- Frontmatter is present and valid.
- Code fences close.
- Source claims have a corresponding entry in `wiki/sources/`.
- MOC links resolve and MOCs contain no prose content.

## Commit & Pull Request Guidelines

Short, imperative commit subjects with optional scope, e.g. `docs(concepts): explain consensus models`. Keep commits focused on one topic. Pull requests should summarize content changes, identify important sources, list moved/renamed pages, and link related issues.

## Security & Source Hygiene

Do not commit credentials, private transcripts, personal data, or copyrighted source dumps without permission. Record source provenance and licensing when importing external material into `wiki/sources/`.

## Language Policy

- Wiki pages must match the language of their source material in `raw/`.
- Chinese sources → Chinese wiki pages; do not translate to English.
- Technical terms, proper nouns, and code identifiers may remain in English within Chinese pages.
- `wiki/index.md`, `wiki/log.md`, and `mocs/` may use English headers for consistency; content summaries match the source language.

## Model-Agnostic Consistency

Because different models may perform ingest over time, always:
- Re-read 2-3 existing wiki pages of the same type before writing a new one, to match style and depth.
- Strictly follow the frontmatter schema and page structure — do not improvise new fields or sections.
- If uncertain whether something qualifies as a `decision`, default to `concept` and let human review reclassify it.
