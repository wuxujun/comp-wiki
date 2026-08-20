---
title: "c-wiki compatibility entry"
description: "Compatibility metadata pointing @Wiki workflows to the repository-root knowledge base."
created: 2026-08-20
freshness_threshold: 70
---

# Wiki Configuration

## Scope

The canonical knowledge base is the repository root: `../raw/`, `../wiki/`, and `../mocs/`. Its structure and writing rules are defined by `../AGENTS.md`.

## Conventions

- Treat `../raw/` as immutable ground truth.
- Write curated pages only under `../wiki/` and navigation pages only under `../mocs/`.
- Use `../wiki/index.md` as the master content index and `../wiki/log.md` as the append-only knowledge-base log.
- Read `../mocs/Home.md` first for queries and follow the repository's incremental MOC rules.
- Apply `../AGENTS.md` when it differs from generic llm-wiki defaults.

## Compatibility Boundary

This `.wiki/` directory was created by an earlier local initialization and is retained only as a discovery and compatibility entry. The empty `.wiki/raw/`, `.wiki/wiki/`, and `.wiki/output/` scaffolds are not content roots and must not receive new sources, articles, or outputs.

The bundled llm-wiki CLI assumes its own directory and frontmatter schema, which differs from this repository. Do not run CLI write or `--fix` operations against this project until a reviewed adapter or migration plan exists; natural-language `@Wiki` workflows should operate directly on the repository-root paths above.
