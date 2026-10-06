---
name: scientific-brainstorming
description: Generate and challenge research ideas from a broad direction, observation, or Research Radar opportunity map while keeping ideas, assumptions, evidence, predictions, and decisions separate.
version: 0.1.0
---

# Scientific Brainstorming

## Goal

Generate a diverse, traceable pool of research ideas without prematurely treating any idea as valid or novel.

This module should increase option quality before Idea Auditor begins eliminating weak directions.

## Core sequence

Preferred sequence:

`independent ideation -> cluster -> define evaluation criteria -> lightweight challenge -> literature-informed reopening -> candidate shortlist -> Idea Auditor`

When practical, generate an initial round before exposing the ideation process to a large literature set. This reduces early anchoring.

Then use current evidence to challenge and reopen ideation.

## Statement labels

Every item must be labeled as one of:

- IDEA
- ASSUMPTION
- PREDICTION
- LOCATED_EVIDENCE
- QUESTION
- DECISION

Never convert an idea into evidence.

## Inputs

Possible inputs:
- broad field,
- Research Radar opportunity map,
- one paper or observation,
- known failure mode,
- new dataset/tool,
- cross-field analogy,
- user constraints.

## Step 1 — Define the creative search space

Record:
- target field,
- desired contribution type,
- resource constraints,
- time horizon,
- risk tolerance,
- excluded directions.

Do not overconstrain if the user wants exploration.

## Step 2 — Independent generation

Generate ideas across several lenses without immediately scoring them.

Useful lenses:

- mechanism: explain a poorly understood effect,
- failure: attack a documented failure mode,
- evaluation: expose what current benchmarks miss,
- efficiency: achieve capability under tighter resource constraints,
- transfer: move a mature idea across fields,
- representation: change what information is modeled,
- optimization: change training/search/inference dynamics,
- data: exploit a newly available data regime,
- system: integrate components to unlock a new capability,
- theory: derive a new interpretation or guarantee,
- negative-result: test a widely assumed but weakly verified belief,
- replication: challenge unstable or irreproducible findings.

Aim for diversity, not many near-duplicates.

## Step 3 — Preserve provenance

Each idea gets a stable ID.

Record:
- source lens,
- originating observation/opportunity,
- whether generated before or after literature exposure,
- linked evidence IDs when any,
- unresolved assumptions.

## Step 4 — Cluster structurally

Cluster by:
- problem,
- mechanism,
- method,
- population/domain,
- evidence need,
- contribution type.

Do not merge ideas only because their wording is similar.

## Step 5 — Define evaluation criteria before scoring

Possible criteria:

- importance,
- originality plausibility,
- information gain,
- discriminating predictions,
- feasibility,
- resource fit,
- reversibility,
- methodological rigor,
- ethical/safety burden,
- crowding risk,
- publication ceiling.

Record what "high" and "low" mean for this session.

Do not automatically average all scores.

## Step 6 — Lightweight adversarial pass

For each serious candidate ask:

- What is the simplest reason this idea may already be known?
- What assumption could kill it?
- What cheaper explanation could reproduce the expected result?
- What resource dependency is hidden?
- What result would make the idea uninteresting even if technically successful?

This is not the full `idea-auditor`.

## Step 7 — Literature-informed reopening

After an initial independent round, consult:
- Research Radar,
- Literature Mapper,
- recent key papers,
- closest prior work.

Then generate a second round that may:
- refine an idea,
- combine previously separate ideas,
- abandon crowded directions,
- transfer a mechanism from an adjacent field,
- exploit a newly discovered open problem.

Mark post-literature ideas separately.

## Step 8 — Avoid convergence collapse

Actively preserve:
- minority ideas,
- high-risk/high-upside ideas,
- ideas with uncertain novelty,
- ideas that contradict the dominant framing.

Do not force consensus.

## Step 9 — Build candidate cards

Each shortlisted idea should contain:

- title,
- one-sentence concept,
- target problem,
- proposed mechanism or engineering insight,
- why now,
- expected observation,
- key assumptions,
- likely experiment,
- feasibility,
- novelty uncertainty,
- strongest objection,
- what evidence is needed next.

## Step 10 — Shortlist without declaring a winner

Use outcomes:

- ADVANCE_TO_AUDIT
- NEEDS_LITERATURE_CHECK
- PARK
- REJECT_FOR_NOW

Do not label an idea "novel" or "publishable" here.

## Output

Return:

1. Brainstorming scope.
2. Initial independent idea pool.
3. Structural clusters.
4. Evaluation criteria.
5. Adversarial notes.
6. Literature-informed second-round ideas.
7. Candidate cards.
8. Shortlist status.
9. Unresolved assumptions.
10. Recommended handoff.

## Handoff

To `idea-auditor` for candidates worth serious evaluation.

To `research-radar` when the broad field itself is unclear or stale.

To `literature-mapper` when one candidate's novelty/gap is the main uncertainty.

## Failure modes

- generating 20 cosmetic variants of one idea,
- scoring before defining criteria,
- treating popularity as quality,
- literature anchoring before any independent generation,
- calling an idea novel without verification,
- discarding minority/high-uncertainty ideas too early,
- producing a winner with false precision,
- confusing creative plausibility with scientific support.
