# Wiki Audit Report — 2026-08-20

## Verdict

**Usable with caveats.** The repository wiki is structurally sound, internally navigable, current, and generally cautious about promotional evidence. Trust is limited mainly by a split canonical root, uncommitted content, undocumented licensing, coarse or live-only provenance, and four unresolved or weakened contradiction cases.

## Scope

- Canonical content audited: `raw/`, `wiki/`, `mocs/`
- Markdown pages scanned: 421
- Synthesized articles: 13
- Source records: 403
- Raw sources: 389
- Output deliverables: 0
- Truth escalations: 5

The repository `AGENTS.md` was treated as the content authority. The empty `.wiki/` scaffold was audited as operational state because it conflicts with that authority.

## Clean Checks

| Check | Result |
|---|---:|
| Frontmatter errors | 0 |
| Broken relative links | 0 |
| Orphan pages | 0 |
| Pages stale over 90 days | 0 |
| Heading or code-fence errors | 0 |
| MOCs containing detailed prose | 0 |
| Domain MOCs missing from Home | 0 |
| Broken source references | 0 |
| Confirmed duplicate pages | 0 |
| Decisions without outcomes | 0 of 0 decisions |

All 389 raw files have exactly one per-file provenance note. The 388 generated content fingerprints are unique; the remaining raw file uses the earlier hand-authored PBL source note. Similar titles correspond to variants or related competitions, not confirmed duplicates.

## High-Priority Findings

### A01 — Canonical root conflict

`AGENTS.md` defines `wiki/` and `mocs/` as the curated knowledge layer, but [.wiki/config.md](../.wiki/config.md) directs compilation into `.wiki/wiki/` and `.wiki/raw/`. [.wiki/_index.md](../.wiki/_index.md) still reports zero sources and zero articles while the repository layer contains 421 Markdown pages.

Because Wiki resolution normally prefers `.wiki/`, future commands can silently target the empty scaffold. Choose one canonical root or add an explicit bridge before further ingest.

### A02 — Most knowledge is not versioned

At audit time, the working tree contained 807 untracked and 7 modified paths. Git tracked only one raw path and six wiki/MOC paths, so most of the corpus and synthesis lacked committed history.

This does not make current content false, but it substantially weakens durability, reviewability, rollback, and provenance.

## Medium-Priority Findings

### A03 — Licensing status is undocumented

All 389 raw-source provenance notes record local provenance but omit license or permission status; 71 also say the external origin was not recorded. This is a rights and redistribution gap, not evidence that use is unauthorized.

### A04 — Eleven pages violate the language rule

Seven Chinese source notes summarize English-only external sources, and four Chinese PBL synthesis pages depend only on those notes. Their claims are supported, but their language conflicts with the repository policy requiring pages to match source language.

Affected synthesis pages:

- [项目式学习的定义与设计](../wiki/concepts/project-based-learning-definition-and-design.md)
- [项目式学习的证据与效果边界](../wiki/concepts/project-based-learning-evidence.md)
- [项目式学习的评价与实施](../wiki/concepts/project-based-learning-assessment-and-implementation.md)
- [项目式学习与问题式学习](../wiki/comparisons/project-based-vs-problem-based-learning.md)

### A05 — External research is live-URL-only

Seven external PBL source notes retain URLs, abstracts, key claims, and credibility scores, but no immutable source capture. The links were resolvable during this audit, yet the research cannot be fully replayed if publisher pages change or disappear.

### A06 — Six synthesis pages have coarse provenance

Six pages cite `raw/docs/` as a directory rather than naming the source records supporting individual claims. They link to catalogs and use cautious wording, but claim-level reproduction requires searching the whole corpus.

### A07 — Contradictions require refinement

Five pages contain four distinct contradiction cases:

| Case | Verdict | Audit result |
|---|---|---|
| PBL weekly workload | Unresolved | One provider document says both “at least two hours” and “one-to-two hours.” |
| Sir Isaac Newton Exam format | Weakened | It is delivered online but requires in-person local supervision, so “online” and “offline” describe different dimensions. |
| International Economics Olympiad format | Weakened | MainTrack is normally on-site; OpenTrack and exceptional editions may be online. |
| Intermediate/Senior Physics Challenge format | Unresolved | Available material distinguishes standard and Online variants, but the primary BPhO site returned HTTP 403. |

Official evidence: [Waterloo SIN Exam](https://uwaterloo.ca/centre-advanced-science-education/science-contests/sir-isaac-newton-exam), [IEO Regulations](https://ieo-official.org/regulations), and [IEO OpenTrack](https://ieo-official.org/opentrack).

## Content Quality

The 13 synthesis pages averaged 80/100; none scored below 50. Two pages are narrow but adequate for their scope:

- [Vanessa Ruales](../wiki/entities/vanessa-ruales.md) depends on one promotional source and correctly marks its biographical claims as unverified.
- [面向客户与非面向客户的教学](../wiki/comparisons/client-facing-vs-non-client-facing-instruction.md) is concise but sufficient for the CT/NCT terminology distinction.

The strongest cluster is the general PBL research layer. Live verification supported its design definitions, positive-but-uncertain evidence conclusion, assessment guidance, and distinction between Project-Based and Problem-Based Learning. The PBLWorks page remains appropriately treated as a first-party framework rather than independent effect evidence.

## Security and Privacy

- No credential, API-token, or private-key patterns were found.
- No email addresses or phone numbers were copied into `wiki/` or `mocs/`.
- Nine raw files contain email-like strings, including two Gmail addresses; review these before committing or distributing raw material.
- Apparent 18-digit ID matches were URL identifiers, and wiki-side matches were substrings of content hashes rather than personal identity numbers.

## Provenance and Outputs

No output deliverables exist; `.wiki/output/` contains only an empty index, so output drift checks were not applicable. Before this audit there was no topic-local session event log or checkpoint. Repository logs and an external redacted session digest provide only coarse historical provenance.

This audit created topic-local event records for the audit itself. Historical ingest and research remain only partially replayable.

## Recommended Order of Work

1. Decide whether `.wiki/` or repository `wiki/` + `mocs/` is canonical, then align configuration and indexes.
2. Review and commit the intended corpus while excluding local noise such as `.DS_Store` and unwanted Obsidian state.
3. Record license or permission status for all raw sources, prioritizing material intended for redistribution.
4. Resolve the language-policy decision for the 11 English-source/Chinese-output pages.
5. Refine the three competition-format notes using delivery mode, supervision mode, track, year, and region as separate fields.
6. Add exact source-note references to the six coarse-provenance synthesis pages.
7. Ask the course provider to clarify the PBL workload conflict.

## Audit Artifacts

- [Machine-readable audit](scan-results.json)
- [Librarian report](../.librarian/REPORT.md)
- [Librarian scan data](../.librarian/scan-results.json)

