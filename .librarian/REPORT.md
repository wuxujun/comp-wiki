# Librarian Report — 2026-08-20

> Scanned 13 synthesized articles and checked 403 source records in the repository-defined knowledge layer.

## Summary

| Metric | Result |
|---|---:|
| Synthesized articles | 13 |
| Source records | 403 |
| Stale over 90 days | 0 |
| Low quality below 50 | 0 |
| Thin but adequate | 2 |
| Average quality | 80/100 |
| Broken source chains | 0 |
| Confirmed duplicate articles | 0 |
| Pages containing contradictions | 5 |

## Quality Findings

- `wiki/entities/vanessa-ruales.md` is intentionally narrow and depends on one promotional course document; its biographical claims remain unverified.
- `wiki/comparisons/client-facing-vs-non-client-facing-instruction.md` is concise but adequate for its bounded terminology purpose.
- Six synthesis pages use `raw/docs/` as a directory-level source. Their prose is careful and links to catalogs, but claim-level provenance is coarse.
- The four general PBL synthesis pages are the strongest content cluster, with multiple independent research sources and explicit evidence limits.

## Policy Findings

- Seven Chinese external-source notes summarize English-only sources.
- Four Chinese PBL synthesis pages depend only on those English sources.
- These 11 pages conflict with the repository rule that wiki pages match the language of their source material.
- The repository frontmatter schema intentionally has no `verified` or `confidence` fields; absence of those fields was not scored as a schema error.

## Duplicate Review

No synthesized articles or exact source records are duplicates. Title similarity surfaced AMC grade variants, separate online/standard competition variants, and generic hash-labeled achievement notes; their content fingerprints are distinct and they should not be merged automatically.

## Recommendation

Keep the current synthesis pages, but resolve the canonical wiki root before further ingest. Then address language-policy mismatches, add claim-level source references to the six coarse-provenance pages, and review the two narrow single-source pages when independent evidence becomes available.

