---
name: source-ingestor
description: Ingest scholarly sources from PDF, DOI, arXiv, URL, bibliography entries, or local files into atomic, deduplicated, evidence-locatable ResearchOS source records. Verify bibliographic identity and version, inspect the actual source, preserve page/section/figure/table provenance, and only then expose the source to literature mapping and claim verification.
version: 0.2.0
---

# Source Ingestor

## Goal

Turn a source reference into an evidence-bearing ResearchOS source record.

This module exists because these are not equivalent:

- a paper title found in search,
- a BibTeX entry,
- an abstract page,
- a downloaded PDF,
- a paper that has actually been inspected and digested.

Preferred chain:

`candidate reference -> identity verification -> version resolution -> source acquisition -> content inspection -> evidence digest -> atomic registration`

A source becomes scientifically usable only after its evidence status is explicit.

## Core principle

> Bibliographic existence is not scientific evidence.

A paper may be cited for scientific support only to the degree that the relevant content was actually inspected.

## Entry conditions

Use this module when the user or another ResearchOS module provides:
- a local PDF,
- DOI,
- arXiv identifier,
- publisher URL,
- scholarly-index result,
- bibliography entry,
- paper title,
- supplementary file,
- dataset/benchmark paper,
- technical report,
- thesis/dissertation,
- standard/specification.

For a broad literature search with no identified candidate sources, use `literature-mapper` or `research-radar` first.

## Source states

Every candidate source uses one state:

- `CANDIDATE`: identity not yet verified.
- `IDENTIFIED`: bibliographic identity verified.
- `ACQUIRED`: inspectable content obtained.
- `DIGESTED`: scientific content inspected and structured.
- `VERIFIED_SOURCE`: digest complete enough for the intended research decision.
- `PARTIAL_SOURCE`: useful but incomplete access/inspection.
- `UNRESOLVABLE`: identity or content cannot be resolved reliably.
- `RETRACTED_OR_SUPERSEDED`: source status materially affects use.

Do not use `VERIFIED_SOURCE` merely because metadata are complete.

## Source authority classes

Classify the source:

- `PRIMARY_RESEARCH`
- `REVIEW_SURVEY`
- `PREPRINT`
- `CONFERENCE_PAPER`
- `JOURNAL_ARTICLE`
- `THESIS_DISSERTATION`
- `DATASET_BENCHMARK`
- `STANDARD_SPECIFICATION`
- `OFFICIAL_DOCUMENTATION`
- `TECHNICAL_REPORT`
- `SECONDARY_SUMMARY`
- `OTHER`

This class describes source type, not quality.

## Step 1 — Register the candidate

Create a provisional source ID before deep work.

Record:
- supplied identifier/reference,
- discovery provenance,
- linked decision question(s),
- why this source matters,
- current state.

Example:

```yaml
id: SRC-012
supplied_as: "arXiv:2601.12345"
found_via: S019
purpose:
  - novelty_check
  - mechanism_background
state: CANDIDATE
```

## Step 2 — Verify bibliographic identity

Resolve, when available:
- canonical title,
- authors,
- publication year,
- venue,
- DOI,
- arXiv ID,
- publisher URL,
- volume/issue/pages,
- publication status.

Use authoritative scholarly metadata where possible.

Identity confidence:
- `HIGH`
- `MEDIUM`
- `LOW`

Do not merge papers based only on similar titles.

## Step 3 — Resolve versions

Check whether the candidate has:
- preprint,
- conference version,
- journal extension,
- accepted manuscript,
- correction,
- retraction,
- supplementary material,
- author version.

Preferred scientific record:
- use the final peer-reviewed version when available and materially equivalent;
- preserve the preprint ID when it is useful for access/history;
- treat materially extended journal versions as related but not identical evidence;
- record corrections and retractions.

Version relations:
- `SAME_WORK_VERSION`
- `EXTENDED_VERSION`
- `CORRECTION`
- `SUPPLEMENT`
- `DISTINCT_WORK`
- `UNKNOWN`

Do not count a preprint and its final paper as independent evidence.

## Step 4 — Deduplicate

Use identifiers in this order when available:

1. DOI
2. arXiv/other stable preprint identifier
3. publisher identifier
4. normalized title + first author + year
5. title similarity only as a candidate signal

If a duplicate exists:
- link the new access path/version to the existing source record,
- do not create a second independent paper entry.

If two versions differ materially, preserve both under one work family or as explicitly linked records.

## Step 5 — Acquire inspectable content

Possible content:
- full PDF,
- HTML article,
- supplementary PDF,
- source-data spreadsheet,
- appendix,
- official repository/artifact,
- abstract only.

Record access status:

- `FULL_TEXT`
- `FULL_TEXT_PLUS_SUPPLEMENT`
- `ABSTRACT_ONLY`
- `METADATA_ONLY`
- `PARTIAL_TEXT`
- `ACCESS_FAILED`

Do not imply full-paper inspection when only the abstract was available.

## Step 6 — Validate file/content integrity

When content is downloaded or supplied:
- confirm expected file type,
- ensure non-empty/readable content,
- detect obvious HTML login pages masquerading as PDF when possible,
- record file hash/version when practical,
- preserve original source path/URL.

For local/user files, record provenance without changing the original.

## Step 7 — Inspect structure before extracting conclusions

Locate:
- Abstract,
- Introduction,
- Related Work/Background,
- Methods,
- Results,
- Discussion,
- Limitations,
- Conclusion,
- References,
- supplementary sections when relevant.

Identify key figures/tables/equations.

Do not summarize the paper solely from Abstract and Conclusion when method/result evidence is needed.

## Step 8 — Build the evidence digest

The digest should be decision-oriented.

Extract:

### Problem and scope
- research problem,
- population/task/domain,
- stated gap,
- research question/objective.

### Method
- method family,
- central mechanism/idea,
- important implementation/protocol details,
- baselines/controls where relevant.

### Evidence
- data/sample,
- experimental design,
- primary metrics,
- key results,
- uncertainty/statistics when reported,
- ablations/mechanism tests,
- failure/negative results when material.

### Claims
Separate:
- author-reported claims,
- directly observed evidence,
- ResearchOS interpretation.

### Limitations
Separate:
- author-stated limitations,
- ResearchOS-inferred limitations.

### Relevance
Record how the source:
- supports a gap,
- weakens a gap,
- supports a mechanism,
- contradicts a mechanism,
- defines a baseline,
- defines a benchmark,
- affects feasibility,
- affects novelty.

## Step 9 — Preserve evidence locations

Every important extracted item should have a locator when possible.

Locator types:
- page,
- section,
- paragraph/heading,
- figure,
- table,
- equation,
- appendix,
- supplementary item.

Example:

```yaml
- id: EV-SRC012-03
  statement: "Method X improves rare-class recall under severe imbalance."
  evidence_type: result
  locator:
    page: 7
    section: "4.2 Long-tail evaluation"
    table: "Table 3"
```

If only an abstract is available, state that explicitly in the locator.

## Step 10 — Distinguish source claim from ResearchOS interpretation

Use:

`SOURCE_REPORTS`
What the authors explicitly state/report.

`SOURCE_SHOWS`
What can be directly verified from a table/figure/equation/data item.

`RESEARCHOS_INFERS`
A synthesis or interpretation by ResearchOS.

Never phrase `RESEARCHOS_INFERS` as though the paper itself established it.

## Step 11 — Handle figures, tables, and equations

When relevant to the research decision, record:
- figure/table ID,
- caption summary,
- what variable/result it displays,
- linked extracted evidence,
- whether the visual is sufficient to support the cited claim.

For equations:
- record symbol/metric definition,
- equation number,
- relevant assumptions.

For PDF figures/tables that contain scientifically important information not present in extracted text, inspect the visual rather than relying only on OCR/text extraction.

## Step 12 — Handle supplementary material

Supplementary files may contain:
- implementation details,
- additional experiments,
- raw tables,
- source data,
- statistical methods,
- ablations,
- limitations.

Record supplements as linked artifacts.

Do not let supplementary evidence disappear from provenance merely because it is outside the main PDF.

## Step 13 — Assess evidence usability

For the intended research decision, classify the source:

### `VERIFIED_SOURCE`
Required scientific content was inspected and identity/version are sufficiently reliable.

### `PARTIAL_SOURCE`
Some relevant content is usable, but important evidence remains inaccessible/unverified.

### `IDENTIFIED_ONLY`
Bibliographic identity exists, but scientific content was not inspected enough.

### `UNRESOLVABLE`
Source cannot be reliably identified/accessed.

The same paper may be adequate for a background statement but inadequate for a high-stakes novelty/mechanism claim.

Record the intended-use boundary.

## Step 14 — Atomic registration

A digest is considered atomically complete when all required pieces land together:

- source identity,
- version relation,
- access/provenance,
- structured digest,
- evidence locators,
- usability status,
- literature-ledger link/index entry.

If a run fails halfway:
- keep a working checkpoint,
- do not mark the source `DIGESTED` or `VERIFIED_SOURCE`.

This prevents metadata-only papers from silently entering the evidence base.

## Step 15 — Update Literature Ledger

After successful ingestion:
- link source ID to the relevant paper entry,
- set `citation_verified`,
- set source/digest reference,
- preserve triage status,
- attach gap/claim relationships.

Literature Mapper should consume the digest rather than re-inventing the paper summary from memory.

## Step 16 — Citation use rules

A citation may be used at different levels:

### Bibliographic mention
Identity verified; scientific content need not be deeply inspected.

### Background factual support
Relevant section/abstract inspected.

### Technical/method claim
Methods/equations inspected.

### Empirical result claim
Results/table/figure inspected.

### Novelty conflict
Closest-work method/contribution evidence inspected.

### Mechanism support
Mechanism-sensitive evidence inspected.

The stronger the manuscript/research claim, the deeper the required source inspection.

## Step 17 — Retractions, corrections, and status changes

When discovered:
- record status,
- link correction/retraction notice,
- identify affected evidence units,
- downgrade or invalidate dependent claims where necessary.

Do not silently continue using superseded evidence.

## Step 18 — Ingestion depth modes

### Quick identity
Use for:
- deduplication,
- bibliography cleanup,
- candidate triage.

Does not authorize scientific claims.

### Focused digest
Use for:
- one decision question,
- novelty comparison,
- one mechanism/result.

Inspect only the necessary authoritative sections.

### Full digest
Use for:
- core prior work,
- closest competitor,
- survey synthesis,
- paper-review evidence,
- central benchmark/method paper.

Inspect all relevant major sections and important supplements.

## Step 19 — Output contract

For each ingested source return:

1. Source ID.
2. Canonical citation.
3. Identity confidence.
4. Publication/source class.
5. Version relations.
6. Access status.
7. Digest depth.
8. Research problem/objective.
9. Method/mechanism.
10. Evidence units with locations.
11. Author claims.
12. Limitations.
13. Relevance to current ResearchOS questions/claims/gaps.
14. Usability status.
15. Unresolved source risks.
16. Ledger/index updates.

## Source digest discipline

Use `source_digest.yaml` for one source/work version.

Use `source_index.yaml` for project-level source registry and dedup/version relations.

Do not put long free-form notes where structured evidence locators are required.

## Handoff rules

### To `literature-mapper`
When:
- verified digests are ready for comparison/synthesis.

### To `paper-auditor`
When:
- a cited source must be checked against a manuscript claim.

### To `paper-builder`
When:
- a verified source supports Introduction/Related Work text.

### Back to discovery/search
When:
- the source is irrelevant, duplicate, or cannot resolve the target decision.

## Failure modes to flag

- citation metadata treated as evidence,
- abstract-only reading presented as full-paper review,
- preprint and final paper double-counted,
- closest prior work summarized from memory,
- no page/figure/table locator for a critical extracted claim,
- supplementary evidence ignored,
- correction/retraction status ignored,
- search-engine snippet used as technical support,
- paper identity guessed from an ambiguous title,
- ingestion marked complete after only metadata extraction,
- ResearchOS inference attributed to source authors.
