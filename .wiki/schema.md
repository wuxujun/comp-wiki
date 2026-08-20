---
title: "c-wiki Topic Guide"
schema_state: advisory
created: 2026-08-20
updated: 2026-08-20
summary: "Advisory compatibility guide mapping llm-wiki discovery to the repository's canonical AGENTS.md conventions."
---

# c-wiki Topic Guide

> This is an advisory compatibility guide. `../AGENTS.md` remains authoritative for page structure, source handling, language, navigation, and maintenance.

## State

- `schema_state`: `advisory`
- `advisory` means suggestions only.
- Keep this advisory until the librarian's topic-guide suggestions are consistently low-noise.
- `strict` is an advanced, explicit opt-in; it still never permits automatic content rewrites.

## Entity Types

| Type | Meaning |
|------|---------|
| `concept` | Bounded idea or mechanism under `../wiki/concepts/`. |
| `comparison` | Head-to-head evaluation under `../wiki/comparisons/`. |
| `entity` | Person, project, company, or tool under `../wiki/entities/`. |
| `decision` | Technical or architectural choice under `../wiki/decisions/`. |
| `source` | Structured provenance note under `../wiki/sources/`. |
| `moc` | Link-only navigation page under `../mocs/`, including the master index. |

## Relationship Verbs

- `cites`: a curated page cites a source note or raw source.
- `supports`: a source supports a claim or decision.
- `contradicts`: a source conflicts with another recorded claim.
- `supersedes`: newer evidence replaces an older understanding.
- `depends-on`: a concept or decision relies on another page.
- `implements`: an entity or decision implements a concept.
- `relates-to`: a weak relationship used when a stronger verb is not justified.

## Source Conventions

- Keep repository-root `../raw/` immutable; do not use `.wiki/raw/`.
- Compile durable synthesis under repository-root `../wiki/`; do not use `.wiki/wiki/`.
- Maintain link-only navigation under `../mocs/`.
- Record one structured provenance note under `../wiki/sources/` for each ingested raw file.
- Keep `../raw/` in its original language and use the repository's default Chinese synthesis language for `../wiki/`, while recording the source language and preserving original titles and technical terms.

## Adoption Notes

- Existing canonical pages remain governed by `../AGENTS.md`.
- Keep this guide advisory; it exists only to prevent `.wiki/` from becoming a second content root.
- Propose structural changes in an audit or implementation plan before applying them.
