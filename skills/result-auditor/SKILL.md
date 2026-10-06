---
name: result-auditor
description: Audit completed experimental results before they become scientific claims. Validate execution integrity, distinguish observations from interpretations, assess uncertainty and alternative explanations, calibrate mechanism/causal language, preserve negative or ambiguous outcomes, and promote only justified claims into the evidence ledger.
version: 0.1.0
---

# Result Auditor

## Goal

Determine what a completed experiment actually establishes.

This module sits between experiment execution and manuscript construction.

It must prevent the following shortcut:

`experiment produced a favorable number -> paper claim is true`

Preferred chain:

`raw artifacts -> execution validity -> observed result -> uncertainty analysis -> alternative explanations -> claim calibration -> evidence status -> research decision`

Writing quality must never substitute for evidential strength.

## Entry conditions

Use this module when:
- one or more experiments have completed;
- raw outputs, summary results, or analysis artifacts are available;
- experiment protocol and intended decision are known.

If the experiment protocol cannot be reconstructed, mark reproducibility risk and do not upgrade strong claims.

If the result is only planned or hypothetical, return to `experiment-designer`.

## Core evidence states

Use these distinctions explicitly:

- `RAW`: unprocessed output or measurement.
- `OBSERVED`: a directly measured/reproducibly computed result.
- `INFERRED`: interpretation consistent with observations.
- `SUPPORTED`: a claim sufficiently backed by valid evidence for its intended wording.
- `AMBIGUOUS`: evidence does not discriminate among relevant explanations.
- `CONTRADICTED`: evidence materially conflicts with the claim.
- `INVALID`: protocol or execution failure prevents scientific use.

Do not skip directly from `RAW` to `SUPPORTED`.

## Step 1 — Reconstruct the experiment contract

Retrieve the planned experiment record and compare it with what actually happened.

Check:
- linked hypothesis/objective,
- primary prediction,
- primary metric,
- baseline/control,
- dataset/sample,
- seeds/repetitions,
- analysis plan,
- pass/fail/ambiguous criteria,
- protocol version,
- execution metadata.

If the experiment cannot be linked to a stable contract, classify it as exploratory unless there is evidence otherwise.

## Step 2 — Validate execution integrity

Before interpreting the result, ask whether the run is scientifically usable.

Check for:
- crashes or partial completion,
- corrupted files,
- missing samples,
- failed sensors/instruments,
- wrong dataset version,
- data leakage,
- train/test contamination,
- accidental test-set tuning,
- wrong baseline implementation,
- unmatched compute/tuning budget,
- incorrect config,
- seed mismatch,
- missing preprocessing,
- metric implementation error,
- protocol deviations,
- undocumented manual exclusions.

Classify execution:
- `VALID`
- `VALID_WITH_DEVIATIONS`
- `QUESTIONABLE`
- `INVALID`

A favorable result from an invalid experiment is not evidence.

## Step 3 — Audit protocol deviations

For each deviation record:
- what changed,
- when it changed,
- why,
- whether the change was known before observing outcomes,
- which claims it affects,
- whether a rerun is required.

Classify:
- `BENIGN`
- `MATERIAL_BUT_USABLE`
- `REQUIRES_SENSITIVITY_ANALYSIS`
- `INVALIDATING`

Do not silently normalize deviations after the fact.

## Step 4 — Separate observation from interpretation

Create an observation table.

Example:

`OBSERVED`:
- Method X mean rare-class AP = 42.1 across five seeds.
- Baseline mean rare-class AP = 39.4.
- Difference = +2.7 points.
- 95% interval = ...

`INFERRED`:
- X likely improves rare-class performance under this setup.

`NOT YET ESTABLISHED`:
- X improves rare-class representation because it fixes gradient suppression.

This separation is mandatory for mechanism claims.

## Step 5 — Check primary outcome first

Evaluate the pre-specified primary metric/comparison before secondary analyses.

Ask:
- Did the primary comparison pass its criterion?
- Is the effect direction as predicted?
- Is magnitude practically meaningful?
- Is uncertainty compatible with the claimed effect?
- Did baseline performance behave plausibly?

Do not rescue a failed primary outcome by searching secondary metrics unless the analysis is explicitly labeled exploratory.

## Step 6 — Quantify uncertainty

Use uncertainty methods appropriate to the design.

Possible evidence:
- confidence intervals,
- credible intervals,
- bootstrap intervals,
- standard deviation across seeds,
- repeated-measure variance,
- effect sizes,
- sensitivity analysis,
- posterior probability,
- power/precision considerations.

Do not equate:
- `p < 0.05` with importance,
- `p > 0.05` with proof of no effect,
- a single run with stable performance,
- overlapping intervals with automatic equivalence.

When statistical analysis is inappropriate or underpowered, say so.

## Step 7 — Inspect distribution, not just averages

When data permit, examine:
- run-to-run variation,
- subgroup behavior,
- tail/failure cases,
- class-level performance,
- calibration,
- worst-case behavior,
- outliers,
- temporal drift,
- domain-specific heterogeneity.

A mean improvement can hide a serious regression.

Do not create subgroup claims without sufficient sample/support.

## Step 8 — Evaluate practical significance

Separate statistical evidence from practical value.

Ask:
- Is the effect large enough to matter?
- Does it improve the intended bottleneck?
- Is the gain worth the added cost/complexity?
- Does the effect survive relevant constraints?
- Does it matter for the target deployment/scientific question?

A tiny but statistically detectable effect may still support only a weak contribution.

## Step 9 — Test alternative explanations

For each important claim, revisit alternatives from the hypothesis and experiment design.

Examples:
- extra parameters,
- extra compute,
- tuning advantage,
- regularization,
- data artifacts,
- measurement drift,
- confounding,
- seed luck,
- preprocessing differences,
- distribution shift,
- selection bias.

Classify each alternative:
- `RULED_OUT`
- `WEAKENED`
- `PLAUSIBLE`
- `UNTESTED`

A mechanism claim should not become `SUPPORTED` while a comparably plausible simpler explanation remains `UNTESTED`.

## Step 10 — Audit mechanism evidence

For mechanism claims, require evidence beyond end-task performance.

Possible levels:

### Level M0 — No mechanism evidence
Only outcome improvement observed.

### Level M1 — Mechanism-consistent correlation
A mechanism-sensitive variable changes in the expected direction.

### Level M2 — Discriminating evidence
Observed pattern distinguishes the proposed mechanism from a strong alternative.

### Level M3 — Intervention/mediation evidence
Manipulating or blocking the mechanism predictably changes the outcome.

### Level M4 — Strong causal/mechanistic convergence
Multiple independent lines of evidence support the mechanism and plausible alternatives are substantially excluded.

Calibrate wording to the level.

Do not write `demonstrates the mechanism` at M0-M1.

## Step 11 — Audit causal claims

Before allowing causal language, ask:
- Was there intervention/randomization or equivalent identification?
- Were confounders controlled adequately?
- Is temporal direction clear?
- Is the comparison identifying?
- Could selection or measurement bias explain the result?

If not, downgrade to associational language.

## Step 12 — Handle null and negative results

A negative result is not automatically an invalid experiment.

Classify:

### `INFORMATIVE_NEGATIVE`
The experiment was valid and meaningfully weakens/rejects the hypothesis.

### `INCONCLUSIVE`
Precision/power/design was insufficient.

### `CONTEXT_DEPENDENT_NEGATIVE`
The effect fails only under specified conditions.

### `INVALID_NEGATIVE`
Execution/protocol failure prevents interpretation.

Preserve valid negative results in the ledger.

Do not delete them because they weaken the paper story.

## Step 13 — Handle unexpected positive results

Unexpected findings should be labeled exploratory.

For a result not pre-specified:
- record when it was noticed,
- create a new exploratory claim/hypothesis,
- avoid confirmatory language,
- recommend independent validation when important.

Do not rewrite the original hypothesis to match the discovered pattern.

## Step 14 — Detect multiplicity and result fishing

Ask:
- How many metrics were tested?
- How many subgroups?
- How many model variants?
- How many seeds/configurations were inspected before selection?
- Were only best runs reported?
- Was the checkpoint chosen using test results?

Flag:
- selective reporting,
- multiple-comparison inflation,
- benchmark overfitting,
- HARKing,
- cherry-picked seeds.

If these materially affect confidence, downgrade evidence.

## Step 15 — Check robustness

Robustness is not mandatory for every claim, but must match claim breadth.

Possible checks:
- seeds,
- datasets,
- domains,
- time periods,
- perturbations,
- hyperparameters,
- implementation variants,
- hardware/system loads,
- sensitivity to exclusions.

Rule:

`claim breadth <= evidence breadth`

If evidence covers one dataset, do not silently claim universal generalization.

## Step 16 — Compare with prior literature

When relevant, check whether the observed result:
- agrees with prior studies,
- contradicts prior studies,
- extends them,
- only appears stronger due to protocol differences.

Unexpected disagreement is not necessarily bad, but requires explanation.

If the comparison depends on external literature not yet mapped, hand back to `literature-mapper`.

## Step 17 — Calibrate claim strength

For each candidate claim, assign:

### Evidence strength
- `NONE`
- `WEAK`
- `MODERATE`
- `STRONG`

### Epistemic state
- `OBSERVED`
- `INFERRED`
- `SUPPORTED`
- `AMBIGUOUS`
- `CONTRADICTED`

### Allowed wording

Examples:

WEAK:
- "may"
- "is consistent with"
- "suggests"

MODERATE:
- "supports"
- "is associated with"
- "improves under the evaluated conditions"

STRONG:
- "demonstrates" only when evidence/design truly warrants it
- causal/mechanistic verbs only when identification is adequate

### Forbidden wording

Record overclaims that must not appear.

Example:
If only one dataset was tested:
- forbid "generalizes across domains".

## Step 18 — Promote evidence into Claim Ledger

A claim may be promoted only if:
- experiment validity is adequate,
- the evidence link is explicit,
- relevant alternatives are addressed,
- wording is calibrated,
- limitations are recorded.

Do not overwrite earlier claim history.

Record:
- prior state,
- new state,
- evidence IDs,
- reason for transition,
- date/version.

## Step 19 — Reassess the hypothesis

Return one of:

- `SUPPORTED`
- `PARTIALLY_SUPPORTED`
- `NOT_SUPPORTED`
- `CONTRADICTED`
- `INCONCLUSIVE`

This is not identical to statistical significance.

If the hypothesis fails:
- preserve it as failed/unsupported,
- propose a pivot separately,
- do not silently edit H1 into H2.

## Step 20 — Reassess the research decision

Ask:
- Does the result justify continuing?
- Is a replication needed before expensive downstream work?
- Does the paper story strengthen or weaken?
- Is the proposed contribution still valid?
- Did the experiment reveal a more valuable question?

Possible decisions:
- continue,
- replicate,
- narrow claim,
- run discriminating follow-up,
- pivot,
- stop.

The next experiment should be chosen for decision value.

## Evidence Gate

Before a result may support manuscript-level claims, require:

1. execution valid enough,
2. relevant protocol deviations disclosed,
3. primary result assessed,
4. uncertainty characterized,
5. alternatives reviewed,
6. claim wording calibrated,
7. evidence/claim links recorded,
8. limitations preserved.

Gate status:
- `PASS`
- `PASS_WITH_LIMITATIONS`
- `BLOCKED`
- `FAIL`

## Required output

For a normal run, return:

1. Experiment validity status.
2. Protocol-deviation audit.
3. Direct observations.
4. Primary outcome assessment.
5. Uncertainty/stability analysis.
6. Practical significance.
7. Alternative-explanation status.
8. Mechanism-evidence level if applicable.
9. Robustness/generalization boundary.
10. Claim table:
    - claim,
    - evidence IDs,
    - epistemic state,
    - evidence strength,
    - allowed wording,
    - forbidden wording,
    - limitations.
11. Hypothesis status.
12. Evidence Gate status.
13. Highest-decision-value next action.
14. Required updates to:
    - `experiment_ledger.yaml`,
    - `claim_ledger.yaml`,
    - `research_state.yaml`,
    - `decision_log.md` when the scientific contract changes.

## Claim transition rules

Allowed examples:

`HYPOTHESIZED -> OBSERVED`
Only when the claim itself is directly measured rather than interpretive.

`HYPOTHESIZED -> INFERRED`
When results support an interpretation but do not establish it directly.

`INFERRED -> SUPPORTED`
When adequate discriminating evidence accumulates.

`HYPOTHESIZED -> CONTRADICTED`
When valid evidence materially conflicts with the prediction.

Never promote based on prose coherence.

## Handoff rules

### Back to `experiment-designer`
When:
- evidence is ambiguous,
- a key alternative remains plausible,
- replication or a discriminating experiment is needed,
- protocol weaknesses need a redesigned experiment.

### Back to `hypothesis-builder`
When:
- the original mechanism fails,
- new exploratory hypotheses emerge,
- predictions were not sufficiently discriminating.

### Back to `literature-mapper`
When:
- the result conflicts with prior work,
- external evidence is needed to contextualize effect size or mechanism.

### To `paper-builder`
Only when:
- central claims have passed the Evidence Gate,
- their wording and boundaries are explicit,
- unsupported interpretations are excluded.

## Failure modes to flag

- favorable result treated as proof,
- mechanism claim based only on endpoint performance,
- ignoring protocol deviations,
- selective seed reporting,
- post-hoc metric switching,
- test-set tuning,
- null result automatically called "implementation failure",
- p-value treated as effect size,
- single dataset used for universal claim,
- unexplained discrepancy with prior literature,
- exploratory finding written as confirmatory,
- invalid run counted as negative evidence,
- negative results removed from the research record,
- claim wording stronger than the actual evidence.
