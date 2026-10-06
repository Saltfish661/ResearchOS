---
name: hypothesis-builder
description: Convert a validated research gap or engineering objective into explicit, falsifiable hypotheses, mechanisms, predictions, alternative explanations, and discriminating tests while preserving uncertainty and avoiding post-hoc hypothesis rewriting.
version: 0.1.0
---

# Hypothesis Builder

## Goal

Turn a sufficiently supported research problem into a testable scientific contract.

This module should clarify:
- what is being explained or improved,
- what mechanism is proposed,
- what observable consequences follow,
- what competing explanations exist,
- what evidence would support or weaken each explanation,
- what must remain unknown until tested.

A hypothesis is not a polished restatement of the desired result.

## Entry conditions

Use this module when:
- the research problem/gap is sufficiently stable,
- relevant literature has been mapped enough to avoid obvious duplication,
- the user has a candidate mechanism, explanation, or engineering objective that needs operationalization.

If the gap or novelty is still materially uncertain, hand back to `literature-mapper`.

If the project is purely engineering-oriented, this module may define testable objectives and mechanism claims without forcing a classical causal hypothesis where one is not appropriate.

## Distinguish statement types

Classify every major statement as one of:

- `RQ`: research question.
- `OBJECTIVE`: engineering or empirical target.
- `HYPOTHESIS`: falsifiable proposition.
- `MECHANISM`: proposed process explaining why an effect should occur.
- `PREDICTION`: expected observable consequence if the hypothesis/mechanism is correct.
- `ALTERNATIVE`: competing explanation that could generate similar observations.
- `ASSUMPTION`: condition taken as given but not established.
- `EVIDENCE`: observation/source already available.

Do not collapse these categories.

## Core construction chain

Preferred chain:

Research gap
-> Research question
-> Hypothesis or engineering objective
-> Mechanism
-> Observable prediction(s)
-> Alternative explanation(s)
-> Discriminating evidence/test
-> Failure condition

For descriptive research, the chain may omit mechanism if no mechanism claim is made.

For systems/engineering research, the chain may begin with an objective and then add mechanism hypotheses for any explanatory claims.

## Step 1 — Restate the research question

A good research question should specify enough of:
- target phenomenon/system,
- population/task/domain,
- comparison or condition,
- outcome,
- uncertainty being resolved.

Avoid questions that already presuppose the answer.

Weak:
"How can our new model improve rare-class accuracy?"

Better:
"Under severe class imbalance, which training dynamics most strongly limit rare-class representation quality, and can intervention X mitigate that limitation without degrading majority-class performance?"

## Step 2 — Identify hypothesis class

Choose the most appropriate form.

### A. Effect hypothesis

Claims that intervention/condition X changes outcome Y.

Example structure:
`Under condition C, intervention X will change Y relative to baseline B.`

### B. Mechanism hypothesis

Claims that X affects Y through process M.

Example structure:
`X improves Y because it changes M; if M is prevented or measured, the expected pattern should change accordingly.`

### C. Comparative hypothesis

Claims that A differs from B under specified conditions.

### D. Interaction/moderation hypothesis

Claims an effect depends on condition Z.

### E. Descriptive/associational hypothesis

Claims a measurable pattern or relationship without causal language.

### F. Engineering objective

Use when the primary contribution is building a system satisfying measurable constraints.

Example:
`Achieve latency <= L and accuracy >= A under resource budget R.`

Do not manufacture causal hypotheses simply to make engineering work look more scientific.

## Step 3 — State the hypothesis minimally

A hypothesis should be:
- precise,
- falsifiable in principle,
- scoped,
- not overloaded with several independent claims.

Prefer one primary hypothesis plus clearly separated secondary hypotheses.

Avoid:
- vague superiority claims,
- unfalsifiable language,
- "our method is effective",
- hypotheses that simply restate the method design.

## Step 4 — Specify mechanism separately

For each mechanism claim, answer:

1. What internal state/process changes?
2. Why should that change matter for the target outcome?
3. What observation would be expected if this mechanism is active?
4. What observation would be difficult to explain if the mechanism were true?

In AI/ML, candidate mechanism dimensions may include:
- information propagation,
- feature geometry,
- gradient magnitude/direction,
- optimization stability,
- inductive bias,
- calibration/uncertainty,
- capacity allocation,
- temporal dependency,
- sparsity,
- memory/retrieval behavior,
- compute/resource allocation.

Do not infer mechanism solely from end-task performance.

## Step 5 — Derive predictions

Each hypothesis should produce one or more predictions.

Predictions should be more specific than:
"performance increases."

Prefer:
- direction,
- condition,
- observable quantity,
- comparison,
- expected pattern.

Example:

Hypothesis:
Minority-class updates are suppressed by gradient dominance from majority classes.

Predictions:
- minority-class gradient norm contribution will be lower under stronger imbalance;
- intervention X will reduce this disparity;
- improvement should be largest in the most imbalanced regime;
- if gradients are equalized by another control method, the incremental benefit of X should shrink.

The fourth prediction is especially valuable because it distinguishes mechanism from generic regularization.

## Step 6 — Generate alternatives

For every important hypothesis, generate credible alternative explanations.

Common alternatives in AI/ML:
- higher parameter count,
- extra compute,
- stronger regularization,
- data augmentation differences,
- random seed variance,
- changed optimization schedule,
- leakage,
- calibration artifacts,
- easier test distribution,
- implementation differences.

Common alternatives in empirical science:
- confounding variables,
- measurement bias,
- selection bias,
- regression to the mean,
- temporal effects,
- instrument drift,
- unmeasured covariates.

Do not invent absurd alternatives merely to appear rigorous. Prioritize plausible competitors.

## Step 7 — Design discriminating observations

For each hypothesis and main alternative, ask:

> What observation would be more likely under one explanation than the other?

Record:
- supporting observation,
- weakening observation,
- observation that distinguishes alternatives,
- evidence that would remain ambiguous.

Do not label a test "mechanism validation" if it only reproduces the end-task result.

## Step 8 — Define failure conditions in advance

Before experiments, write explicit failure conditions.

Examples:
- no predicted directional effect,
- effect disappears under fair compute control,
- mechanism variable does not change,
- alternative explanation accounts for the result equally well,
- effect appears only on one seed or one narrow benchmark,
- required system constraint cannot be met.

A failed hypothesis is a legitimate research result.

Do not redefine success after seeing results without logging the change as a new hypothesis or pivot.

## Step 9 — Manage assumptions

List assumptions that the hypothesis depends on.

Classify each:
- `SUPPORTED`
- `INFERRED`
- `HYPOTHESIZED`
- `UNKNOWN`

Ask whether any assumption is so critical that it should be tested before the main experiment.

A hidden unsupported assumption can invalidate the entire experiment plan.

## Step 10 — Prioritize hypotheses

If multiple hypotheses exist, rank by decision value.

Prefer testing hypotheses that:
- determine whether the main idea is viable,
- distinguish competing explanations,
- can kill a weak direction early,
- materially change the paper story,
- are feasible to test.

Avoid creating a large hypothesis list just because many questions are interesting.

## Step 11 — Calibrate causal language

Use causal language only when design and evidence can support it.

Before experiments:
- mechanism statements remain `HYPOTHESIZED`.

After observational association alone:
- prefer "associated with", "consistent with", "suggests".

Do not pre-authorize words such as:
- proves,
- causes,
- demonstrates mechanism,

unless the eventual design can justify them.

## Step 12 — Produce the hypothesis map

For each primary hypothesis, record:

- ID,
- linked RQ,
- statement,
- type,
- mechanism,
- assumptions,
- predictions,
- alternatives,
- discriminating tests,
- failure criteria,
- evidence status,
- priority,
- downstream experiment requirements.

Suggested structure:

```yaml
- id: H1
  linked_rq_ids: [RQ1]
  statement: "..."
  type: mechanism
  epistemic_state: HYPOTHESIZED
  mechanism:
    statement: "..."
    status: HYPOTHESIZED
  assumptions: []
  predictions:
    - id: PRED-H1-1
      statement: "..."
      discriminating_power: high
  alternatives:
    - id: ALT-H1-1
      statement: "..."
  failure_criteria: []
  priority: high
```

## Step 13 — Distinguish confirmatory from exploratory work

Before data/results are observed, mark planned hypotheses as:
- `CONFIRMATORY`
- `EXPLORATORY`

If a new hypothesis is generated after examining results:
- record it as `POST_HOC_EXPLORATORY`,
- do not rewrite history to make it appear pre-specified.

This distinction is especially important when statistical inference or strong mechanistic claims depend on pre-specification.

## Step 14 — Check publication-story coherence

Ask:

If H1 is supported, what scientific contribution follows?

If H1 fails, what remains valuable?

If only performance improves but the mechanism fails, what claim remains defensible?

This prevents a paper from depending entirely on one interpretation that the experiments cannot uniquely support.

## Hypothesis quality rubric

Evaluate each primary hypothesis on:

- clarity,
- falsifiability,
- mechanism specificity,
- prediction specificity,
- discriminating power,
- dependence on unsupported assumptions,
- feasibility,
- publication relevance.

Use:
- `STRONG`
- `USABLE_WITH_REFINEMENT`
- `WEAK`
- `NOT_TESTABLE`

Do not average these mechanically.

## Required output

For a normal run, return:

1. Research question(s).
2. Statement-type classification.
3. Primary hypothesis/objective.
4. Mechanism model.
5. Predictions.
6. Alternative explanations.
7. Discriminating evidence/tests.
8. Failure criteria.
9. Critical assumptions.
10. Confirmatory vs exploratory status.
11. Hypothesis quality assessment.
12. Highest-decision-value next test.
13. Required updates to `research_state.yaml`, `claim_ledger.yaml` if needed, and `decision_log.md`.

## State updates

Update `research_state.yaml` with:
- research questions,
- hypotheses,
- assumptions,
- blockers,
- next action.

If the hypothesis changes the research contract materially:
- add a decision-log entry.

Do not create a `SUPPORTED` claim in `claim_ledger.yaml` merely because a hypothesis was formulated.

## Handoff rules

### Back to `literature-mapper`
When:
- mechanism plausibility depends on unverified prior work,
- a supposedly novel hypothesis may already be established,
- a key assumption lacks literature support.

### To `experiment-designer`
When:
- primary hypothesis/objective is stable,
- at least one discriminating prediction exists,
- failure criteria are explicit,
- the most important assumptions are known,
- alternatives are sufficiently defined to guide controls.

### To `idea-auditor`
When:
- the only testable hypothesis leads to a weak or irrelevant contribution,
- the mechanism collapses,
- publication value changes materially.

## Failure modes to flag

- hypothesis == desired outcome,
- hypothesis == method description,
- mechanism inferred from performance alone,
- no alternative explanations,
- no failure criterion,
- predictions too vague to measure,
- multiple independent claims bundled into one hypothesis,
- causal language without causal design,
- post-hoc hypothesis rewritten as pre-specified,
- hidden critical assumptions,
- testing only conditions where the method is expected to win,
- treating null results as implementation failure without evidence.
