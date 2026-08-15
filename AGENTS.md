# AGENTS.md

## Project Structure & Module Organization

This repository is a Markdown-based knowledge base. Keep unprocessed reference material under `raw/`, organized by source type:

- `raw/articles/` for articles and essays
- `raw/docs/` for documentation and notes
- `raw/repos/` for repository-derived material
- `raw/transcripts/` for audio or video transcripts

Publish curated content under `wiki/`. Use `wiki/index.md` as the main entry point and `wiki/log.md` to record notable content updates. Place topic pages in `wiki/concepts/`, comparisons in `wiki/comparisons/`, named subjects in `wiki/entities/`, and source notes in `wiki/sources/`.

## Roles

You maintain this knowledge base. The user provides raw material and asks questions. `raw/` is read-only ground truth — never edit it. `wiki/` is fully yours to create, rewrite, and reorganize.

## Ingest Workflow

Triggered when the user says "ingest this", "sync the wiki", "fold this in", or runs `/wiki-sync`.

1. Read the new file(s) under `raw/`.
2. Read `wiki/index.md` to understand current coverage and avoid duplicating existing pages.
3. Write a source note in `wiki/sources/<slug>.md` summarizing the raw material (2-3 sentence abstract, key claims, provenance).
4. Extract concepts, entities, and comparisons worth their own page. Create new pages under the correct subfolder, or update existing ones — write "current understanding," not edit history, since old content can be safely overwritten.
5. Cross-link every new or updated page with related pages using relative links, e.g. `[Concept](../concepts/concept-name.md)`.
6. Update `wiki/index.md`: add or revise the entry (title, one-line summary, relative link) for every page touched.
7. If new information contradicts an existing page, do not silently overwrite it. Add a `## Contradictions` section presenting both versions with sources, and flag it for the user to resolve.
8. Append one line to `wiki/log.md`: `## [YYYY-MM-DD] ingest | <source> -> <pages touched>`.
9. Summarize what changed in your reply to the user (pages created/updated, contradictions flagged).

## Query Workflow

Triggered by any question that isn't an ingest request.

1. Read `wiki/index.md` first to identify which pages are relevant.
2. Load only the specific pages needed to answer — don't load the whole wiki.
3. If the wiki page lacks sufficient detail, fall back to the underlying `raw/` source referenced in its `wiki/sources/` note.
4. Answer citing which wiki page(s) informed the response, using relative links.
5. If the question surfaces a gap (no page covers it), tell the user instead of guessing, and offer to ingest relevant material if they have it.

## Build, Test, and Development Commands

There is no build system or application runtime. Work directly with Markdown files. Before submitting changes, run:

```sh
git diff --check
rg --files raw wiki
```

`git diff --check` detects whitespace errors. `rg --files` provides a quick inventory to confirm new content is stored in the intended directory. If a Markdown linter is introduced later, document and run its repository-provided command rather than relying on a global installation.

## Coding Style & Naming Conventions

- One `#` heading per page, hierarchical `##`/`###` headings below it.
- Blank lines around headings, lists, and fenced code blocks.
- Prefer relative links between repository pages, e.g. `[Concept](../concepts/concept-name.md)`.
- Name files with descriptive lowercase kebab-case (`distributed-systems.md`); avoid spaces and ambiguous abbreviations.
- Keep `raw/` material faithful to its source verbatim. Rewrite `wiki/` content for clarity, consistency, and your own voice — it is a living synthesis, not a copy.
- Every `wiki/` page opens with a 2-3 sentence self-contained summary before any detail, so it can be understood without reading the whole page.

## Testing Guidelines

Review every changed page in a Markdown preview. Confirm that:

- Relative links resolve to real files.
- Headings are properly nested (no skipped levels).
- Code fences close.
- Source claims have a corresponding entry in `wiki/sources/` when appropriate.

No automated test framework or coverage threshold is configured yet.

## Commit & Pull Request Guidelines

Use short, imperative commit subjects with an optional scope, e.g. `docs(concepts): explain consensus models`. Keep commits focused on one topic. Pull requests should:

- Summarize the content added or revised.
- Identify important sources.
- List moved or renamed pages.
- Include screenshots only when rendered layout changes need visual review.
- Link related issues when available.

## Security & Source Hygiene

Do not commit credentials, private transcripts, personal data, or copyrighted source dumps without permission. Record source provenance and licensing details when importing external material into `wiki/sources/`.
