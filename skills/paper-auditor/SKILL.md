---
name: paper-auditor
description: Audit a completed or near-completed research manuscript for logical closure, claim-evidence support, method-experiment alignment, internal consistency, reproducibility, citation/novelty risk, venue-readiness, and reviewer-facing failure points without inventing missing evidence.
version: 0.1.0
---

# Paper Auditor

## Goal

Audit a manuscript as if it must survive real peer review, thesis examination, or submission screening.

This module does not primarily improve prose. Its job is to determine whether the manuscript's scientific argument closes correctly:

`Research question -> method -> experiment/evidence -> result -> claim -> conclusion`

The auditor must distinguish:
- scientific defects,
- evidence gaps,
- logical gaps,
- consistency defects,
- reproducibility defects,
- positioning/citation risks,
- presentation defects.

Do not treat all issues as equal.

## Entry conditions

Use this module when:
- a complete or near-complete manuscript exists;
- enough of the paper can be inspected to reconstruct its argument;
- the user wants pre-submission review, thesis review, camera-ready audit, reviewer simulation, or final consistency checking.

If only an idea or outline exists, route to earlier ResearchOS modules.

If the paper depends on results whose validity has not yet been audited, surface that dependency and route to `result-auditor`.

## Core audit principle

A manuscript is not ready because it reads smoothly.

It is ready only when its central scientific claims are:
- clearly stated,
- traceable,
- adequately supported,
- internally consistent,
- bounded to the evidence,
- reproducible enough for the field,
- positioned accurately against prior work.

## Audit modes

### 1. Quick triage
Use for fast pre-check.

Focus on:
- fatal logical gaps,
- missing evidence,
- contradictions,
- obvious overclaim,
- submission-blocking defects.

### 2. Full audit
Run the complete pipeline.

### 3. Camera-ready audit
Use after acceptance or conditional acceptance.

Prioritize:
- reviewer-comment closure,
- numerical consistency,
- figure/table correctness,
- equation/notation definitions,
- formatting/venue compliance,
- no new unsupported scientific claims.

Do not casually expand scope after acceptance.

### 4. Thesis/defense audit
Prioritize:
- chapter-level logical closure,
- contribution ownership,
- methodological completeness,
- question-answer closure,
- likely defense questions,
- consistency across chapters.

### 5. Blind-review simulation
Adopt the perspective of an uninvolved reviewer.

Prioritize:
- reasons for reject / major revision / weak accept concern,
- novelty,
- evidence sufficiency,
- reproducibility,
- clarity of contribution,
- mismatch with venue expectations.

## Severity levels

Classify every issue:

- `CRITICAL`: can invalidate the core claim, cause rejection, block defense, or indicate unsupported/fabricated scientific content.
- `MAJOR`: materially weakens a central claim or reviewer confidence.
- `MODERATE`: meaningful defect but unlikely to invalidate the central contribution alone.
- `MINOR`: local clarity, notation, style, or presentation issue.
- `COSMETIC`: formatting/polish only.

Do not inflate severity to appear rigorous.

## Modification authority

For every recommended fix, assign:

- `SAFE`: can be corrected from the manuscript without changing scientific meaning.
- `CONTEXTUAL`: likely recoverable from existing paper/project context, but should be checked.
- `VERIFY`: author confirmation required.
- `EVIDENCE_REQUIRED`: requires new data, analysis, experiment, source, or artifact.
- `DO_NOT_INVENT`: information is absent and must not be fabricated.

This classification is mandatory for scientific issues.

## Stage 0 — Manuscript profiling

Before detailed review, establish:

- paper type,
- field/subfield,
- intended venue or degree level,
- manuscript status,
- claimed contribution count,
- section/chapter structure,
- primary datasets/systems/subjects,
- central metrics,
- key figures/tables,
- whether reviewer comments already exist.

Build a one-paragraph neutral description of what the paper claims to accomplish.

Do not critique yet.

## Stage 1 — Skeleton audit

This stage examines only the paper's logical architecture.

### 1.1 Identify the central research question

Extract:
- problem,
- gap,
- RQ/objective,
- hypothesis if present,
- primary contribution(s),
- claimed conclusion(s).

Ask:

> What exact question does this paper answer?

If this cannot be stated clearly, mark a structural risk.

### 1.2 Build section responsibility map

For each section/chapter:
- what question does it answer?
- what claim does it establish?
- what evidence does it contain?
- what downstream section depends on it?

Flag:
- sections with unclear responsibility,
- duplicated sections,
- methods placed in Results,
- conclusions introduced before evidence,
- background sections that never support the research gap,
- results that do not answer any stated RQ.

### 1.3 Build question-to-answer closure

For each RQ/objective:

`RQ -> Method -> Experiment/Evidence -> Result -> Answer`

Classify:
- `CLOSED`
- `PARTIALLY_CLOSED`
- `OPEN`
- `MISALIGNED`

If open, determine whether:
- the section is missing,
- the experiment is missing,
- the result exists but is not linked,
- the conclusion exceeds the evidence,
- the original RQ is too broad.

### 1.4 Audit contribution closure

For every contribution listed in Abstract/Introduction:
- where is it implemented?
- where is it evaluated?
- where is its result?
- where is it discussed?
- is it reflected in the Conclusion?

Flag "orphan contributions":
claims presented as contributions but never evidenced.

### 1.5 Audit narrative overcommitment

Check whether Abstract/Introduction promise more than the paper later delivers.

Common forms:
- "generalizable" with one dataset,
- "real-time" without latency evidence,
- "robust" without stress/robustness tests,
- "significantly" without appropriate support,
- "mechanism" without mechanism-sensitive evidence,
- "state-of-the-art" without verified comparable evaluation.

## Stage 2 — Claim-Evidence Audit

This is the core evidence audit.

### 2.1 Extract claims

Identify central claims from:
- Abstract,
- Introduction/contributions,
- Results,
- Discussion,
- Conclusion.

Classify:
- empirical,
- mechanistic,
- causal,
- methodological,
- novelty,
- system capability,
- generalization,
- efficiency/resource,
- theoretical.

### 2.2 Trace each claim to evidence

For each claim ask:
- what figure/table/experiment/source supports it?
- is that evidence direct?
- is the evidence sufficient for the wording?
- are relevant uncertainty measures shown?
- are alternative explanations considered?
- does the evidence apply to the claimed scope?

Classify support:

- `A_STRONG`: directly and adequately supported.
- `B_ADEQUATE`: supported, but explanation/qualification could improve.
- `C_WEAK`: some evidence exists but does not fully support the wording.
- `D_UNSUPPORTED`: no adequate evidence identified.
- `E_CONTRADICTED`: evidence conflicts with the claim.

### 2.3 Require location-level traceability

Whenever possible, record:
- section,
- paragraph,
- page,
- figure/table/equation,
- experiment ID,
- claim ID.

Avoid vague feedback such as "Results need more evidence."

### 2.4 Choose repair action

For each weak claim:

If evidence exists but explanation is thin:
- add bounded analysis.

If evidence scope is narrower than claim:
- narrow wording.

If claim is nonessential:
- remove it.

If claim is central and unsupported:
- `EVIDENCE_REQUIRED`.

Never fabricate a result just to close the chain.

## Stage 3 — Method–Experiment Closure Audit

Check whether the methods described are actually evaluated and whether results rely on undefined methods.

### 3.1 Method-to-evaluation mapping

Extract:
- algorithmic modules,
- preprocessing,
- losses/objectives,
- priors,
- sensors/instruments,
- system components,
- datasets,
- statistical procedures,
- calibration methods,
- hyperparameters important to claims.

For each method component:
- is it used?
- is it evaluated?
- does the paper claim it contributes?
- is an ablation/control needed to isolate it?

Flag components that are heavily emphasized but never evaluated.

### 3.2 Result-to-method mapping

For every major result/metric:
- where was it defined?
- how was it computed?
- what inputs were used?
- is the protocol described?

Examples of risk:
- metric appears only in Results,
- figure uses an undefined deviation formula,
- "latency" reported without measurement protocol,
- a baseline appears in Results but not Methods,
- a statistical test appears without assumptions/procedure.

### 3.3 Equation and symbol audit

Check:
- every nonstandard symbol defined,
- units present,
- notation stable,
- equations consistent with prose,
- nonstandard metrics mathematically defined,
- equation variables correspond to actual implementation.

For a metric central to a claim, missing definition is at least `MAJOR`.

## Stage 4 — Cross-Manuscript Consistency Audit

Check consistency across Abstract, Introduction, Methods, Results, figures, tables, Discussion, and Conclusion.

### 4.1 Numerical consistency

Audit:
- sample size,
- dataset size,
- number of classes,
- number of experiments,
- train/val/test counts,
- years/date ranges,
- number of sensors,
- runtime,
- percentages,
- performance values,
- parameter counts,
- contribution count.

When numbers differ, do not automatically "fix" them.

Ask whether the difference can be explained by:
- filtering,
- missing samples,
- exclusions,
- subgrouping,
- preprocessing.

If not clear: `VERIFY`.

### 4.2 Terminology consistency

Check:
- method name,
- module names,
- dataset names,
- variables,
- abbreviations,
- research object,
- labels/classes,
- metric names.

Flag terminology drift that could imply a changed meaning.

### 4.3 Figure/table consistency

Check:
- numbering,
- captions,
- axis labels,
- legends,
- units,
- text references,
- values matching prose,
- baseline names,
- panel labels,
- N/A/NA conventions,
- significant digits.

### 4.4 Contribution and conclusion consistency

Compare contribution statements across:
- Abstract,
- Introduction,
- Conclusion.

Check whether claims become stronger over time without new evidence.

## Stage 5 — Scientific and Reproducibility Audit

Requirements vary by field.

### 5.1 AI/ML checklist

When applicable, audit:
- data source and version,
- split protocol,
- leakage controls,
- preprocessing,
- augmentation,
- architecture/config,
- optimizer/scheduler,
- epochs/steps,
- seed strategy,
- hyperparameter selection,
- baseline fairness,
- compute/hardware,
- code availability if claimed,
- parameter/FLOP/runtime claims,
- statistical variance,
- ablation,
- external/pretrained data.

### 5.2 Experimental/empirical checklist

When applicable:
- sample source,
- inclusion/exclusion,
- experimental unit,
- replication,
- instrumentation,
- calibration,
- environmental controls,
- measurement uncertainty,
- operator/batch effects,
- missing-data handling,
- statistical model assumptions.

### 5.3 Systems checklist

When applicable:
- hardware/software environment,
- workload,
- benchmark conditions,
- load/concurrency,
- warm-up,
- measurement window,
- repetitions,
- resource usage,
- failure conditions,
- comparison fairness.

### 5.4 Reproducibility severity

Classify:
- `REPRODUCIBLE_ENOUGH`
- `PARTIAL`
- `WEAK`
- `NOT_REPRODUCIBLE_FROM_PAPER`

Do not require irrelevant details merely for checklist completeness.

## Stage 6 — Citation and Novelty Audit

### 6.1 Citation support

For important factual statements:
- does the citation actually support the sentence?
- is the cited work primary when it should be?
- is a secondary source laundering a claim?
- are closely related methods omitted?

### 6.2 Novelty positioning

Check whether novelty claims are:
- specific,
- literature-backed,
- multidimensional where needed,
- conservative enough.

Classify novelty risk:
- `LOW`
- `MEDIUM`
- `HIGH`
- `UNVERIFIED`

If external literature verification has not been performed, do not certify novelty.

### 6.3 Citation mismatch

Flag:
- citation title/topic unrelated to sentence,
- paper cited for a result it did not report,
- dataset paper cited as method evidence,
- review cited instead of original study when primary evidence matters.

## Stage 7 — Reviewer Red Team

Now switch perspective.

Assume the reviewer:
- is competent,
- is not invested in the project,
- has limited patience,
- will focus on scientific risk rather than helping the authors.

Ask:

1. What is the strongest reason to reject?
2. What is the strongest Major Revision request?
3. Which central claim is easiest to attack?
4. Which figure/table is most vulnerable?
5. Which missing definition or protocol detail undermines trust?
6. Is novelty believable?
7. Is the evaluation sufficient?
8. Are conclusions broader than evidence?
9. What would a skeptical reviewer misunderstand because the paper is unclear?
10. Which issue would most likely appear independently across multiple reviewers?

Do not generate dozens of trivial issues.

Prioritize the top reviewer-facing risks.

## Stage 8 — Venue / Thesis Requirement Audit

When specific requirements are available, check:
- page/word limits,
- anonymization,
- author/affiliation rules,
- template compliance,
- figure editability,
- language restrictions,
- supplementary material policy,
- code/data policy,
- ethics statements,
- AI disclosure,
- reference style,
- submission artifacts.

Use current official guidance where requirements may change.

Keep venue compliance separate from scientific validity.

## Stage 9 — Revision Planning

For every issue provide:

- issue ID,
- severity,
- location,
- affected claim/RQ,
- why a reviewer would care,
- evidence status,
- repair action,
- modification authority,
- dependency,
- verification method.

Suggested repair types:

- `EDIT_TEXT`
- `DEFINE_TERM_OR_METRIC`
- `NARROW_CLAIM`
- `ADD_EXISTING_EVIDENCE`
- `ADD_ANALYSIS`
- `VERIFY_FACT`
- `ADD_CITATION`
- `REWORK_STRUCTURE`
- `NEW_EXPERIMENT_REQUIRED`
- `REMOVE_CLAIM`
- `NO_ACTION`

### Revision priority

Prioritize by:

`scientific risk × centrality × reviewer likelihood`

Not by ease of editing.

## Stage 10 — Final blind-review verdict

Return a realistic reviewer-style outcome.

Possible manuscript states:
- `NOT_READY`
- `MAJOR_REVISION_REQUIRED`
- `MINOR_REVISION_REQUIRED`
- `READY_WITH_KNOWN_RISKS`
- `READY_FOR_SUBMISSION`
- `CAMERA_READY_WITH_CHECKS`

When venue-specific review is requested, optionally provide:
- likely reviewer score/range,
- confidence,
- top reasons,
but do not pretend to predict acceptance with certainty.

## Special mode — Camera-ready conservative policy

If the paper is already accepted:

Default priority:
1. resolve reviewer comments,
2. correct definitions/inconsistencies,
3. improve clarity,
4. meet formatting requirements,
5. preserve accepted scientific scope.

Do not introduce:
- new major claims,
- unreviewed experiments,
- substantial methodological changes,
unless required and explicitly approved.

When experimental details are unknown because the current authors inherited prior work:
- classify missing details as `VERIFY` or `DO_NOT_INVENT`,
- recover only what is directly supported by manuscript/project evidence,
- avoid "reasonable defaults" presented as facts.

## Required output

For a full audit, return:

1. Neutral manuscript profile.
2. One-sentence statement of the paper's actual research question.
3. Skeleton audit.
4. RQ/contribution closure matrix.
5. Claim-evidence matrix.
6. Method-experiment closure findings.
7. Cross-manuscript consistency findings.
8. Reproducibility assessment.
9. Citation/novelty risks.
10. Top reviewer red-team concerns.
11. Prioritized revision plan.
12. Final blind-review verdict.
13. Required updates to `paper_audit.yaml`, `paper_map.yaml`, `claim_ledger.yaml`, and `decision_log.md` where relevant.

## Issue format

Use:

```yaml
- id: PA-001
  severity: MAJOR
  category: claim_evidence
  location:
    section: Results
    detail: "Fig. 4 / paragraph 2"
  affected_claim_ids: [C004]
  issue: "Reflectance deviation is central to the BRDF claim but is not mathematically defined."
  why_it_matters: "The reader cannot reproduce or interpret the reported comparison."
  evidence_status: D_UNSUPPORTED_DEFINITION
  repair:
    action: DEFINE_TERM_OR_METRIC
    authority: VERIFY
    next_step: "Recover the intended formula from project context or author confirmation."
  blocking: true
```

## Audit discipline

### Rule 1 — Cite manuscript locations

Do not say:
"Some numbers are inconsistent."

Say:
"Abstract reports N=189, while Sec. III-B reports N=187; verify whether two samples were excluded and document the exclusion."

### Rule 2 — Do not manufacture repairs

If the correct value/formula/protocol is unknown:
- identify what is missing,
- state why it matters,
- mark `VERIFY` or `EVIDENCE_REQUIRED`.

### Rule 3 — Central claims first

Do not bury fatal scientific issues under grammar feedback.

### Rule 4 — Separate defect from suggestion

Label:
- `REQUIRED`: needed for validity/readiness.
- `RECOMMENDED`: meaningfully improves reviewer confidence.
- `OPTIONAL`: polish only.

### Rule 5 — Re-audit after revision

A fixed local sentence does not guarantee the paper is now consistent.

After major edits, rerun:
- affected claim traces,
- affected numbers,
- Abstract/Conclusion consistency,
- figure/table references.

## Handoff rules

### Back to `paper-builder`
When:
- structure/prose needs revision but evidence already exists.

### Back to `result-auditor`
When:
- claim strength is unclear,
- alternative explanations remain unresolved,
- evidence needs reinterpretation.

### Back to `experiment-designer`
When:
- a central claim cannot survive without new evidence.

### Back to `literature-mapper`
When:
- novelty or citation support is uncertain.

### To venue/submission workflow
When:
- scientific audit passes,
- manuscript is internally consistent,
- remaining issues are venue/format specific.

## Failure modes to flag

- line-editing before checking scientific validity,
- treating every issue as equally important,
- asking for unnecessary extra experiments,
- inventing missing parameters/formulas,
- accepting an unsupported claim because it sounds plausible,
- overreacting to explainable numerical differences,
- novelty certification without literature verification,
- mixing venue formatting with scientific validity,
- reviewer simulation that only produces vague generic comments,
- declaring "ready" while critical claim-evidence gaps remain.
