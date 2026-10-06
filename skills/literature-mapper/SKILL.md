---
name: literature-mapper
description: Build an auditable literature map for a research question, idea, gap, mechanism, or novelty claim. Use reproducible search logs, paper-level evidence extraction, citation chasing, gap calibration, and SOTA synthesis before hypothesis or experiment design.
version: 0.1.0
---

# Literature Mapper

## Goal

Build a traceable model of the relevant research landscape.

This module is not primarily a prose-writing tool. Its first job is to determine:
- what is already known,
- what is uncertain or disputed,
- what prior work is most relevant,
- whether the proposed gap is real,
- whether the proposed novelty survives contact with the literature,
- what unresolved question should be handed to the next research stage.

The output should support decisions, not merely produce a long bibliography.

## Core principle

A literature claim is only as strong as the evidence chain behind it.

Prefer:

Research question -> search strategy -> candidate papers -> verified papers -> extracted evidence -> synthesis -> gap status -> next research decision

Do not jump directly from search snippets to conclusions.

## When to use

Use this module when the project needs any of the following:

- state-of-the-art mapping,
- novelty checking,
- research-gap validation,
- literature support for a hypothesis,
- prior-art comparison,
- mechanism/background mapping,
- contradiction discovery,
- citation chasing,
- targeted update of an existing literature map,
- a foundation for Related Work or Introduction.

Do not use this module as a substitute for:
- systematic review methodology when the user explicitly needs a publication-grade systematic review or meta-analysis;
- final citation formatting only;
- paper writing before the evidence map is stable.

## Inputs

Use whatever is already available:

- research question or topic,
- candidate method/idea,
- claimed gap,
- candidate contribution,
- target population/task/system,
- known papers,
- date range,
- target venue or field,
- user-provided PDFs or bibliography,
- constraints on databases or access.

Missing information should be recorded as `UNKNOWN`.

## Search modes

Choose the narrowest mode that matches the decision.

### 1. Rapid reconnaissance

Use when:
- the idea is early,
- the user wants to know whether an area already exists,
- the goal is vocabulary discovery and obvious prior art.

Output:
- canonical terminology,
- seed papers,
- major method families,
- obvious novelty conflicts,
- high-value next search.

This mode is not sufficient to support strong "no prior work" claims.

### 2. Targeted novelty check

Use when:
- a specific contribution is proposed,
- the key question is whether something substantially similar already exists.

Search both:
- exact formulation/keywords,
- conceptual equivalents and alternative terminology.

Novelty search must include:
- direct keyword search,
- backward citation chasing from close papers,
- forward citation chasing when possible,
- neighboring method families that may implement the same idea under different names.

### 3. Full literature map

Use when:
- the project is moving from idea to hypothesis/experiment,
- a defensible SOTA map is needed,
- multiple method families or competing explanations matter.

Produce:
- search log,
- paper ledger,
- SOTA matrix,
- gap matrix,
- unresolved contradictions,
- search stopping rationale,
- handoff recommendations.

### 4. Systematic/scoping review preparation

Use only when explicitly needed.

This mode should:
- preserve database-specific queries,
- define inclusion/exclusion criteria before broad screening where possible,
- track duplicates and screening stages,
- distinguish protocol deviations,
- avoid claiming systematic completeness unless the actual process justifies it.

When the request requires formal PRISMA-style systematic review, meta-analysis, or discipline-specific review standards, route to or incorporate a dedicated systematic-review protocol rather than pretending a general SOTA search is equivalent.

## Step 1 — Define the decision question

Before searching, rewrite the user request into one or more decision questions.

Examples:

- Does prior work already address the proposed mechanism?
- Is the claimed failure mode documented?
- Which method families currently dominate this task?
- Is the proposed contribution novel at the method, mechanism, application, or experiment level?
- Which unresolved limitation is most strongly supported by the literature?

Store each decision question explicitly.

Do not search broadly until the decision target is clear.

## Step 2 — Decompose the concept

Build a concept table before search.

At minimum consider:

- problem/task,
- population/domain,
- method/architecture,
- mechanism,
- outcome/metric,
- failure mode,
- synonyms,
- historical terminology,
- neighboring terminology,
- broader parent concept,
- narrower child concept.

For novelty checks, explicitly generate semantic equivalents.

Example:

"minority-class feature propagation" may overlap with literature under:
- long-tail representation learning,
- minority gradient suppression,
- class-imbalanced optimization,
- rare-class feature learning,
- gradient conflict,
- reweighting or decoupled representation learning.

Do not assume the user's vocabulary is the vocabulary used by prior work.

## Step 3 — Design search families

Create several query families instead of one long query.

Recommended families:

### A. Problem search
Find evidence that the problem/failure mode exists.

### B. Solution-family search
Find established approaches solving the problem.

### C. Exact novelty search
Search the proposed combination, mechanism, or formulation.

### D. Semantic novelty search
Search equivalent ideas under different wording.

### E. Evaluation search
Find standard datasets, baselines, metrics, and evaluation conventions.

### F. Contradiction search
Actively search for evidence that weakens the proposed gap or mechanism.

Record:
- query string,
- database/source,
- date,
- mode,
- result count when available,
- notes on query changes.

## Step 4 — Source hierarchy

Prefer evidence in roughly this order when the claim allows it:

1. original peer-reviewed research,
2. authoritative conference/journal versions,
3. accepted manuscripts or official preprints when publication is unavailable,
4. major surveys/reviews for orientation and terminology,
5. benchmark or dataset papers,
6. official standards/documentation where methodologically relevant,
7. secondary summaries only for discovery.

Rules:

- Use review papers to discover the landscape, not as the sole basis for every technical claim.
- Prefer the final published version over an earlier preprint when materially different.
- Mark preprints as preprints.
- Do not treat blog posts, generated summaries, repository READMEs, or search snippets as primary scientific evidence when a paper exists.
- In fast-moving fields, intentionally include recent preprints but keep their status visible.

## Step 5 — Seed-paper strategy

Identify a small number of seed papers that are:

- highly relevant,
- influential or canonical,
- recent enough to expose current terminology,
- methodologically close,
- or explicitly cited by the user's known references.

Use seeds for:
- backward citation chasing,
- forward citation chasing,
- author/lab tracing when appropriate,
- terminology expansion,
- method-family discovery.

Do not equate citation count with quality or relevance.

## Step 6 — Screening and triage

For every candidate, classify:

- `CORE`: directly affects the research decision.
- `CONTEXT`: useful background or adjacent method.
- `POSSIBLE_CONFLICT`: may undermine novelty or gap.
- `METHOD_REFERENCE`: useful for implementation/evaluation conventions.
- `EXCLUDE`: not relevant after inspection.

Record an exclusion reason when exclusion matters to completeness.

Possible reasons:
- wrong task,
- wrong population/domain,
- conceptual mismatch,
- only superficial keyword overlap,
- not primary research,
- insufficient methodological detail,
- superseded duplicate,
- inaccessible full evidence.

## Step 7 — Verify bibliographic identity

Before a paper is used as evidence, verify as much as possible:

- title,
- authors,
- year,
- venue,
- DOI/arXiv/other stable identifier,
- publication status,
- version if relevant.

A citation is not considered verified merely because a search engine snippet displays a title.

If identity cannot be verified:
- keep the paper in the ledger,
- mark `citation_verified: false`,
- do not use it for a high-stakes novelty or factual claim without warning.

## Step 8 — Extract evidence at paper level

Do not summarize a paper as a single vague paragraph.

For each core paper extract, where applicable:

- research problem,
- research question/objective,
- method,
- dataset/population,
- experimental setting,
- key result,
- claimed contribution,
- explicit limitations,
- implicit limitations,
- relevance to current project,
- which gap claims it supports,
- which gap claims it weakens,
- which mechanism claims it supports,
- important differences from current idea.

Distinguish:
- what authors directly report,
- what ResearchOS infers,
- what remains unknown.

Use the root epistemic states.

## Step 9 — Build the SOTA matrix

For a full literature map, synthesize core papers by comparable dimensions.

Suggested columns:

- paper ID,
- year,
- problem,
- method family,
- mechanism,
- data/domain,
- evaluation protocol,
- major result,
- limitation,
- relation to proposed idea,
- novelty conflict level.

The comparison dimensions should be chosen for the actual research decision.

Do not mechanically compare papers on irrelevant fields merely because a template has those columns.

## Step 10 — Build the gap matrix

A gap must be evidence-backed.

Classify candidate gaps into one or more types:

- `EXPLICIT_LIMITATION`: prior work directly identifies the limitation.
- `UNRESOLVED_CONTRADICTION`: literature reports conflicting results/explanations.
- `UNDEREXPLORED_REGIME`: a meaningful condition/domain/population is sparsely studied.
- `METHOD_LIMITATION`: current approaches share a documented technical weakness.
- `MECHANISM_GAP`: performance is known but explanation/mechanism remains uncertain.
- `EVALUATION_GAP`: current evidence does not test an important claim or setting.
- `TRANSFER_GAP`: effectiveness outside the original setting is unresolved.
- `SCALE_OR_RESOURCE_GAP`: current approaches fail under practical compute/data/resource constraints.
- `REPRODUCIBILITY_GAP`: existing evidence is too incomplete or inconsistent to validate a claim.

For each gap record:
- statement,
- supporting paper IDs,
- contradicting paper IDs,
- directness of evidence,
- confidence,
- consequences for the proposed project.

## Step 11 — Calibrate novelty claims

Novelty is multidimensional.

Evaluate separately:

- problem novelty,
- method novelty,
- mechanism novelty,
- application novelty,
- experimental novelty,
- system/integration novelty,
- dataset/resource novelty.

Use conservative wording.

Preferred language:
- "I did not find prior work in the searched sources that..."
- "The closest identified work differs in..."
- "Novelty appears plausible but remains uncertain because..."

Avoid:
- "No one has ever..."
- "This is the first..."
- "Completely novel..."

unless the search process and evidence justify that level of certainty.

A targeted search can support "no close prior work found in the searched set"; it usually cannot prove universal absence.

## Step 12 — Search for disconfirming evidence

Before accepting the gap, deliberately ask:

- Is there a paper that already solves this?
- Is the proposed limitation actually no longer true?
- Is there a better-known term for the same mechanism?
- Does a neighboring field already contain the same idea?
- Is the proposed "gap" simply a dataset artifact?
- Is the desired contribution already standard practice but not framed as novelty?

Record disconfirming searches in the log.

A literature map that only searches for supporting evidence is incomplete.

## Step 13 — Determine search saturation

Do not search forever.

Search can pause when the marginal decision value becomes low.

Possible saturation indicators:
- new searches mostly return already-known paper families,
- citation chasing repeatedly loops back to the same core works,
- newly found papers do not change the gap or novelty assessment,
- the main competing methods are represented,
- the most important contradiction searches have been attempted,
- the next research decision would not materially change with one more ordinary search.

Record:
- why search stopped,
- what areas remain incomplete,
- confidence in coverage.

Use:
- `LOW`,
- `MEDIUM`,
- `HIGH`

for coverage confidence.

Do not use `HIGH` when important databases, date ranges, or adjacent terminology remain unexplored.

## Step 14 — Produce decision-oriented synthesis

The final synthesis should answer:

1. What is the established research landscape?
2. What are the dominant solution families?
3. Which papers are closest to the proposed work?
4. Which claimed gaps survived?
5. Which claimed gaps weakened or disappeared?
6. What contradictions remain?
7. What novelty is still plausible?
8. What must be verified next?
9. What research decision should now change, if any?

Do not produce a generic chronological history unless that is useful to the decision.

## Citation evidence rules

### Rule 1 — Search result is not evidence

A title/snippet can trigger retrieval, but it is not enough for a scientific claim.

### Rule 2 — Evidence must point to the paper

When possible, preserve:
- paper identifier,
- relevant section/page/figure/table,
- extracted claim,
- ResearchOS interpretation.

### Rule 3 — Separate source claim from synthesis

Example:

`OBSERVED`: Paper P014 reports lower rare-class recall under setting X.

`INFERRED`: This may indicate a representation or optimization imbalance relevant to H1.

The second statement must not be written as though P014 directly proved the mechanism unless it did.

### Rule 4 — Citation chaining must preserve provenance

If Paper A cites Paper B for a factual claim, retrieve Paper B before treating it as the primary support when feasible.

### Rule 5 — Retractions/corrections/status matter

When discovered, record:
- retraction,
- expression of concern,
- major correction,
- superseding version.

## Literature ledger discipline

Update `literature_ledger.yaml` with:

- decision questions,
- search log,
- candidate/verified papers,
- SOTA families,
- gap claims,
- contradiction searches,
- search saturation,
- unresolved literature risks.

Update `research_state.yaml` with:
- gap statement,
- gap evidence IDs,
- novelty confidence,
- current blockers,
- next action.

If literature materially changes the research contract, add a `decision_log.md` entry.

## Required output

For a normal full literature-mapping run, return:

1. Decision question(s).
2. Search scope and strategy.
3. Canonical terminology and synonyms.
4. Core-paper shortlist.
5. SOTA map.
6. Closest prior work to the current idea.
7. Gap matrix.
8. Disconfirming evidence.
9. Novelty assessment by dimension.
10. Coverage confidence and stopping rationale.
11. Material unknowns.
12. Highest-decision-value next action.
13. Required state/ledger updates.

## Handoff rules

### To `idea-auditor`

Return when the literature invalidates or substantially changes:
- the problem,
- the gap,
- feasibility assumptions,
- publication ceiling.

### To `hypothesis-builder`

Return when:
- the gap is sufficiently supported,
- the project needs a falsifiable explanation/prediction.

### To `experiment-designer`

Return only when:
- the literature already supports a stable research question/hypothesis,
- experimental conventions and relevant baselines are sufficiently mapped.

### To `paper-builder`

Only after:
- claims are mature,
- the literature map is stable enough to support Introduction/Related Work,
- citations used in manuscript-level claims are verified.

## Failure modes to flag

- searching only exact user wording,
- using citation count as a proxy for truth,
- novelty claims based on one database,
- treating a survey as primary evidence for all claims,
- cherry-picking supportive papers,
- ignoring negative/contradictory work,
- using snippets without reading evidence,
- mixing preprint and final versions as separate independent evidence,
- claiming systematic completeness without systematic methods,
- writing Related Work before determining the literature structure,
- turning an absence of search results into proof of novelty.
