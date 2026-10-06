---
name: idea-auditor
description: Audit an early-stage research idea for problem validity, novelty, mechanism, testability, feasibility, and publication value before substantial experiments or writing begin.
version: 0.1.0
---

# Idea Auditor

## Goal

Determine whether an idea deserves further research investment and, if so, what must be validated next.

Do not reward complexity, fashionable terminology, or module stacking by default.

## Inputs

Use whatever the researcher already has:
- topic or rough idea,
- target problem,
- proposed method,
- known literature,
- available dataset/equipment,
- compute/time budget,
- intended venue or output.

Missing information should be marked `UNKNOWN`; do not fabricate it.

## Audit dimensions

### 1. Problem audit

Ask:
- What exact problem is being solved?
- Who or what is affected by it?
- Is the difficulty documented or merely assumed?
- Is the problem scientifically meaningful, practically meaningful, or both?
- If solved, what changes?

Failure mode: a solution searching for a problem.

### 2. Gap audit

Separate:
- problem novelty,
- method novelty,
- mechanism novelty,
- application novelty,
- experimental novelty.

Do not equate "no identical paper found" with novelty.

When novelty materially affects the decision and literature has not been checked, set novelty confidence to `UNKNOWN` and hand off to `literature-mapper`.

### 3. Mechanism audit

For each proposed technical element, require a causal or functional story:

Element -> What changes internally? -> Why does that address the identified failure? -> What observable prediction follows?

For AI/ML work, useful mechanisms may involve:
- information flow,
- representation,
- optimization/gradient dynamics,
- inductive bias,
- capacity allocation,
- uncertainty,
- data efficiency,
- computational structure.

Flag pure "module stacking" where components lack a problem-specific role.

### 4. Hypothesis/testability audit

Translate the idea into falsifiable form where possible:
- hypothesis/objective,
- mechanism,
- prediction,
- alternative explanation,
- discriminating observation or experiment.

An idea is weak if success can only be defined retrospectively.

### 5. Experimental identifiability

Ask whether a successful experiment would actually support the intended claim.

Check possible confounders such as:
- increased parameter count,
- extra compute,
- longer training,
- different preprocessing,
- data leakage,
- unfair hyperparameter tuning,
- changed evaluation protocol,
- untracked random variation.

Require a plausible way to distinguish the proposed mechanism from simpler explanations.

### 6. Feasibility audit

Evaluate against actual constraints:
- dataset access,
- data quality/labels,
- compute,
- equipment,
- implementation difficulty,
- time,
- money,
- domain expertise,
- dependency risk.

A scientifically attractive idea may still receive `GO_WITH_CONDITIONS` or `PIVOT` if execution risk is unreasonable.

### 7. Publication-value audit

Ask the counterfactual:

> If all planned experiments succeed exactly as expected, what is the strongest defensible paper story?

Distinguish:
- useful engineering improvement,
- benchmark optimization,
- new method,
- new mechanism/insight,
- new empirical finding,
- new system capability.

Flag `WEAK_PAPER` when the likely final story is only "we add X and obtain a small metric increase" without a stronger insight, capability, or rigor contribution.

## Grill pass

After the structured audit, optionally perform red-team attack:
- try to kill the idea using the most consequential objections first;
- do not inflate scope with arbitrary extra experiments;
- classify additional work as either `required_for_survival` or `optional_strengthening`.

## Scoring

Scores are diagnostic, not additive. Do not compute a naive average.

Suggested dimensions (0-10 or UNKNOWN):
- problem importance,
- novelty confidence,
- mechanism plausibility,
- testability,
- experimental identifiability,
- feasibility,
- publication ceiling.

A single fatal dimension can dominate the decision.

## Verdict

Return exactly one primary verdict:
- `GO`: worth starting now; key assumptions are testable.
- `GO_WITH_CONDITIONS`: promising, but named blockers must be resolved first.
- `PIVOT`: problem is worthwhile but current method/question is not.
- `WEAK_PAPER`: feasible work, but expected contribution is currently too weak for the intended publication goal.
- `KILL`: current idea does not justify further investment.

## Required output

1. Research idea in one precise sentence.
2. Strongest reason to pursue it.
3. Strongest reason not to pursue it.
4. Audit by the seven dimensions above.
5. Unknowns that materially block judgment.
6. Minimum evidence needed before expensive work.
7. Highest-decision-value next action.
8. Verdict.
9. Updates required to `research_state.yaml` and `decision_log.md`.

## Handoff

- unresolved novelty/gap -> `literature-mapper`
- idea survives but hypothesis is vague -> `hypothesis-builder`
- hypothesis already stable -> `experiment-designer`
- idea fails -> log why; do not rescue it by silently changing the research question.
