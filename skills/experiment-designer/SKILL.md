---
name: experiment-designer
description: Convert stable research questions, hypotheses, mechanisms, or engineering objectives into decision-oriented experiments with discriminating predictions, baselines, controls, fairness constraints, statistical plans, failure criteria, reproducibility requirements, and resource-aware prioritization.
version: 0.1.0
---

# Experiment Designer

## Goal

Design the smallest set of experiments that can materially change a research decision.

This module should answer:

- What exactly is being tested?
- Which observation would support or weaken the hypothesis?
- Which alternative explanations must be ruled out?
- What controls and baselines are necessary?
- What would count as failure?
- How much evidence is enough to justify the next decision?
- What is the cheapest experiment that can kill a weak idea early?

Do not optimize for experiment count. Optimize for decision value.

## Entry conditions

Use this module when:
- the research question or engineering objective is explicit;
- the main hypothesis/mechanism is stable enough to test;
- at least one measurable prediction exists;
- major alternative explanations are known well enough to guide controls.

If these conditions are not met:
- route to `hypothesis-builder`;
- if the missing dependency is prior work/evaluation conventions, route to `literature-mapper`.

## Experiment contract

Every experiment must have:

1. linked RQ/hypothesis/objective,
2. purpose,
3. discriminating prediction,
4. independent/manipulated variables or comparison,
5. dependent/outcome variables,
6. controls,
7. baselines,
8. confounders and fairness constraints,
9. data/sampling/split plan,
10. metrics,
11. repetition/statistical plan,
12. stopping/failure criteria,
13. resource estimate,
14. reproducibility metadata,
15. expected decision impact.

An experiment missing several of these fields is a draft, not execution-ready.

## Step 1 — Define the decision

Start with the decision the experiment is intended to change.

Examples:
- keep or kill H1,
- choose between mechanism A and B,
- determine whether X adds value beyond parameter count,
- determine whether the system satisfies latency/accuracy constraints,
- decide whether a full-scale experiment is justified.

Write:

`If result R occurs, decision D changes in way W.`

If no plausible result would change a decision, the experiment may have low value.

## Step 2 — Map claims to experiments

Create a claim-experiment matrix.

For each important claim:
- identify required evidence,
- identify planned experiment(s),
- mark whether evidence is direct or indirect,
- identify any unsupported claim.

Prefer experiments that support multiple tightly related claims without creating interpretation ambiguity.

Do not use one broad experiment as evidence for several unrelated claims.

## Step 3 — Derive discriminating predictions

Use predictions from `hypothesis-builder`.

For each hypothesis:
- what pattern is expected?
- what pattern is expected under the strongest alternative?
- what observation differentiates them?

Weak:
"Method X should improve accuracy."

Stronger:
"If X works through mechanism M, improvement should increase with imbalance severity and shrink when M is independently controlled."

Mechanism claims require mechanism-sensitive measurements, not only end metrics.

## Step 4 — Choose experiment type

Select the smallest appropriate design.

Possible types:
- baseline comparison,
- ablation,
- controlled intervention,
- factorial design,
- sensitivity analysis,
- robustness/stress test,
- subgroup analysis,
- scaling experiment,
- cross-dataset/cross-domain validation,
- mechanism probe,
- simulation,
- observational analysis,
- prospective/retrospective study,
- system benchmark,
- user study,
- case study,
- replication.

Do not force every project into the same design template.

## Step 5 — Define baselines

Baselines should answer specific questions.

Possible baseline roles:
- established SOTA,
- simple/strong conventional baseline,
- no-intervention/control,
- same architecture without the proposed component,
- matched-compute baseline,
- matched-parameter baseline,
- oracle/upper bound where meaningful,
- random/trivial baseline where meaningful.

Every baseline should have a rationale.

Avoid:
- cherry-picking weak baselines,
- using outdated methods only because they are easy to beat,
- tuning the proposed method more heavily than comparators without disclosure.

## Step 6 — Define controls and fairness constraints

List what must remain equivalent.

For AI/ML, consider:
- train/val/test split,
- preprocessing,
- augmentation,
- backbone,
- parameter count,
- FLOPs/latency,
- optimizer,
- training steps,
- scheduler,
- hyperparameter budget,
- random seeds,
- early stopping,
- external data,
- checkpoint selection.

For empirical/experimental work, consider:
- environment,
- instrument,
- operator,
- batch,
- time,
- specimen/source,
- demographic/domain covariates,
- exposure,
- measurement protocol.

Mark fairness constraints as:
- `MUST_MATCH`
- `MAY_DIFFER_WITH_JUSTIFICATION`
- `INTENTIONALLY_MANIPULATED`

## Step 7 — Identify confounders

For each planned conclusion ask:

> What else could explain this result?

Create a confounder register.

For each confounder:
- mechanism of bias,
- likelihood,
- impact,
- mitigation,
- residual risk.

If a fatal confounder cannot be mitigated, mark the experiment `NOT_IDENTIFYING`.

## Step 8 — Design ablations

Ablation should answer "which part matters?" rather than merely generate more rows.

Types:
- component removal,
- component substitution,
- mechanism-targeted ablation,
- hyperparameter sensitivity,
- interaction ablation,
- resource-matched ablation.

For multi-component methods, distinguish:
- necessity,
- sufficiency,
- interaction.

Do not claim a component is "necessary" merely because removing it lowers performance if removal also changes compute, optimization, or capacity.

## Step 9 — Plan data and sampling

Specify:
- dataset/source,
- version,
- inclusion/exclusion rules,
- unit of analysis,
- split logic,
- leakage controls,
- sampling method,
- class/group balance,
- sample size rationale where applicable,
- handling of missing data.

For ML:
- avoid test-set iteration;
- separate hyperparameter tuning from final evaluation;
- document external/pretrained data when material.

For repeated-measures or hierarchical data:
- identify the true experimental unit;
- avoid pseudoreplication.

## Step 10 — Choose metrics

Every metric should map to a claim.

Classify:
- primary metric,
- secondary metric,
- diagnostic metric,
- mechanism metric,
- resource/system metric.

Avoid "metric shopping" after results are known.

If multiple metrics can conflict, define priority in advance.

For imbalanced problems, include metrics that expose minority behavior instead of relying only on aggregate accuracy.

## Step 11 — Plan repetition and uncertainty

Specify appropriate uncertainty handling.

Possible approaches:
- multiple random seeds,
- repeated trials,
- confidence intervals,
- bootstrap,
- cross-validation,
- hierarchical modeling,
- power analysis,
- effect sizes,
- Bayesian posterior summaries,
- nonparametric methods.

Do not default to p-values for every project.

For ML:
- report seed variance when stochasticity can materially affect claims;
- distinguish run-to-run variance from dataset uncertainty.

## Step 12 — Predefine analysis

Before execution, define:
- primary comparison,
- aggregation rule,
- exclusion rule,
- outlier handling,
- statistical test/model if applicable,
- correction for multiple comparisons when applicable,
- success threshold,
- failure threshold,
- ambiguous zone.

Avoid retrofitting the analysis to maximize significance.

## Step 13 — Define stopping and failure criteria

Possible statuses:
- `PASS`
- `FAIL`
- `AMBIGUOUS`
- `INVALIDATED`

Examples:
- PASS: predicted direction and effect exceed predefined threshold.
- FAIL: primary prediction not observed under adequate power/repetition.
- AMBIGUOUS: evidence insufficient or alternatives remain indistinguishable.
- INVALIDATED: leakage, protocol violation, broken measurement, or implementation defect makes the run unusable.

Do not convert `FAIL` into `INVALIDATED` without concrete evidence of protocol failure.

## Step 14 — Plan cheapest-kill-first sequence

Rank experiments by expected decision value per resource cost.

Suggested order:
1. sanity checks,
2. fatal-assumption tests,
3. small discriminating pilot,
4. matched baseline,
5. core experiment,
6. mechanism tests,
7. robustness/generalization,
8. expensive scaling/extension.

This ordering is preferred over immediately running the largest benchmark suite.

## Step 15 — Estimate resources

Record:
- compute,
- wall-clock time,
- equipment,
- data collection effort,
- annotation effort,
- monetary cost,
- human labor,
- storage,
- external dependencies.

Classify risk:
- `LOW`
- `MEDIUM`
- `HIGH`

If the full design exceeds constraints, propose:
- pilot,
- proxy,
- reduced-factor design,
- staged validation.

Do not hide feasibility problems.

## Step 16 — Reproducibility contract

Before execution, define what should be recorded.

Minimum when relevant:
- code commit,
- config,
- environment,
- dependency versions,
- hardware,
- dataset version/hash,
- random seeds,
- preprocessing,
- checkpoint selection rule,
- commands/workflow,
- raw-result artifact references.

A result that cannot be traced to an execution configuration should not be promoted into high-confidence evidence.

## Step 17 — Separate exploratory and confirmatory experiments

Classify each experiment:
- `CONFIRMATORY`
- `EXPLORATORY`
- `DIAGNOSTIC`
- `PILOT`

Exploratory results may generate new hypotheses.

Do not retroactively relabel exploratory experiments as confirmatory.

## Step 18 — Build dependency graph

Experiments may depend on prior results.

Example:

EXP-001 sanity
-> if valid -> EXP-002 matched baseline
-> if effect survives -> EXP-003 mechanism probe
-> if mechanism supported -> EXP-004 cross-domain validation

Do not schedule expensive downstream experiments when an upstream failure would make them irrelevant.

## Step 19 — Evaluate readiness

Classify each experiment:
- `READY`
- `READY_WITH_CONDITIONS`
- `BLOCKED`
- `NOT_IDENTIFYING`

A design is `READY` only if:
- decision is explicit,
- prediction is measurable,
- controls/baselines are adequate,
- major confounders are addressed,
- metrics and analysis are defined,
- failure criteria exist,
- resources are feasible.

## Experiment-design quality rubric

Evaluate:
- claim alignment,
- discriminating power,
- fairness,
- confounder control,
- statistical adequacy,
- reproducibility,
- feasibility,
- decision value.

Use:
- `STRONG`
- `USABLE_WITH_REFINEMENT`
- `WEAK`
- `NOT_IDENTIFYING`

Do not mechanically average.

## Required output

For a normal run, return:

1. Decision(s) being tested.
2. Claim-experiment matrix.
3. Experiment list ordered by decision value.
4. For each experiment:
   - linked hypothesis/objective,
   - prediction,
   - design,
   - baselines,
   - controls,
   - confounders,
   - data/sampling,
   - metrics,
   - repetition/statistics,
   - pass/fail/ambiguous criteria,
   - resource estimate,
   - reproducibility requirements,
   - readiness status.
5. Cheapest experiment that could kill the idea.
6. Expensive experiments that should wait.
7. Experiment dependency graph.
8. Required updates to `experiment_ledger.yaml`, `research_state.yaml`, and `decision_log.md`.

## Experiment ledger discipline

Every planned experiment receives a stable ID before execution.

Do not reuse an experiment ID for a materially changed protocol.

If the protocol changes:
- create a new version or experiment ID,
- record why it changed.

Failed and invalidated experiments remain in the ledger.

## Handoff rules

### Back to `hypothesis-builder`
When:
- no discriminating prediction can be derived,
- mechanism cannot be measured,
- alternatives cannot be distinguished,
- failure criteria are undefined.

### Back to `literature-mapper`
When:
- correct baselines are unknown,
- evaluation protocol is unclear,
- standard metrics/datasets need verification.

### To `result-auditor`
Only after:
- experiment execution is complete,
- raw outputs and protocol metadata are available,
- protocol deviations are recorded.

## Failure modes to flag

- experiment does not change any decision,
- only end-task metric measured for a mechanism claim,
- weak or cherry-picked baselines,
- unequal tuning budgets,
- data leakage,
- test-set iteration,
- no seed/repetition plan despite stochasticity,
- no primary metric,
- no predefined failure criterion,
- ablation changes several variables at once,
- pseudoreplication,
- post-hoc exclusion without logging,
- scaling up before a cheap discriminating pilot,
- invalid run presented as negative evidence,
- negative result dismissed as implementation failure without evidence.
