---
name: research-intake
description: Initialize or recover a ResearchOS project state from a rough idea, existing project, manuscript, dataset, codebase, reviewer comments, or mixed evidence. Establish goals, constraints, research type, current stage, known facts, unknowns, and the highest-value next route without pretending unresolved scientific questions are already answered.
version: 0.1.0
---

# Research Intake

## Goal

Create the smallest honest project state needed to route research work correctly.

Research Intake should answer:

- What project is this?
- What is the user trying to accomplish?
- What already exists?
- What is actually known?
- What remains unknown?
- What constraints matter?
- What stage is the work truly at?
- What is the next highest-value ResearchOS module?

This module should not perform a full novelty review, literature review, experiment design, or paper audit unless that work is necessary merely to identify the current stage.

## Core principle

Start from evidence, not ambition.

Do not convert:
- an idea into a validated gap,
- a desired contribution into novelty,
- an existing model into a successful method,
- a manuscript sentence into an established fact,
- a reviewer request into proof that the reviewer is correct.

Intake records claims about the project; later modules validate them.

## Entry scenarios

Research Intake may begin from:

### A. Rough idea
Example:
"I want to use topology in Transformer attention."

### B. Existing research project
Example:
"We have a dataset, model, and partial experiments."

### C. Existing manuscript
Example:
"This paper is already written; help me review it."

### D. Inherited project
Example:
"This is based on previous work and we do not know all experimental details."

### E. Reviewer feedback
Example:
"The paper was accepted/revised and here are reviewer comments."

### F. Data/code first
Example:
"We have this repository/dataset but no clear research question."

### G. Failed/ambiguous project
Example:
"We ran many experiments and performance is unstable."

The intake pathway should adapt to the starting artifact.

## Step 1 — Identify user objective

Classify the immediate objective.

Examples:
- explore whether an idea is worth pursuing,
- verify novelty/gap,
- formulate a hypothesis,
- design experiments,
- interpret results,
- write a paper,
- repair an existing manuscript,
- prepare submission,
- respond to reviewers,
- recover/reconstruct an inherited project.

Record:
- immediate objective,
- longer-term target,
- deadline if material,
- target output if known.

Do not assume publication is always the goal.

## Step 2 — Identify project type

Classify the project using one or more labels:

- `THEORY`
- `AI_ML`
- `SYSTEMS`
- `SOFTWARE_ENGINEERING`
- `EMPIRICAL`
- `EXPERIMENTAL_SCIENCE`
- `DATASET_RESOURCE`
- `HCI_USER_STUDY`
- `REVIEW_SYNTHESIS`
- `MIXED`
- `UNKNOWN`

The label controls later checklists, not scientific status.

## Step 3 — Determine project maturity

Use the highest stage genuinely supported by available artifacts.

Stages:

- `IDEA`
- `GAP_EXPLORATION`
- `HYPOTHESIS_FORMATION`
- `EXPERIMENT_DESIGN`
- `EXPERIMENT_RUNNING`
- `RESULT_ANALYSIS`
- `MANUSCRIPT_BUILDING`
- `MANUSCRIPT_AUDIT`
- `SUBMISSION`
- `REVIEW_REBUTTAL`
- `CAMERA_READY`
- `ARCHIVED_OR_STOPPED`

Do not assign a late stage simply because a document called "final paper" exists if central experiments are still unverified.

## Step 4 — Inventory available artifacts

Record what currently exists.

Possible artifacts:
- notes,
- proposal,
- manuscript,
- reviewer comments,
- PDFs,
- bibliography,
- source code,
- repository,
- dataset,
- trained models,
- raw experiment outputs,
- plots/tables,
- lab notebook,
- configs,
- logs,
- supplementary material,
- hardware/instrument metadata.

For each artifact, record:
- existence,
- accessibility,
- provenance,
- freshness/version if known,
- whether it can be treated as evidence.

Do not treat a screenshot of a number as equivalent to reproducible raw output when provenance matters.

## Step 5 — Separate known facts from user beliefs

Create an intake evidence table.

### `KNOWN`
Directly supported by available artifacts or explicit project records.

### `USER_REPORTED`
Reported by the researcher but not independently verified.

### `INFERRED`
Reasonably inferred from available context.

### `ASSUMED`
Working assumption.

### `UNKNOWN`
Not currently established.

Examples:

`KNOWN`: A dataset file contains 4,481 images.

`USER_REPORTED`: The split was stratified.

`INFERRED`: The project likely targets long-tail detection.

`UNKNOWN`: Whether test images were used during hyperparameter tuning.

This separation is especially important for inherited projects.

## Step 6 — Establish the preliminary research contract

Record, without over-validating:

- working problem statement,
- candidate research question,
- candidate gap,
- candidate hypothesis/objective,
- candidate contribution,
- intended evidence,
- target audience/output.

Every item may have status:
- `PROVISIONAL`
- `SUPPORTED`
- `UNKNOWN`

At intake, most scientific content may remain provisional.

## Step 7 — Record constraints

Constraints can dominate research decisions.

Record when relevant:

### Time
- deadline,
- project duration,
- experiment turnaround.

### Compute
- GPU/CPU/NPU,
- memory,
- storage,
- cloud budget.

### Data
- dataset availability,
- licensing,
- annotation,
- sample size,
- data collection feasibility.

### Equipment
- sensors,
- instruments,
- lab access.

### Team
- number of members,
- expertise,
- access to domain experts.

### Money
- cloud/API costs,
- equipment,
- publication costs,
- annotation costs.

### Administrative
- ethics/IRB,
- competition rules,
- confidentiality,
- IP,
- venue policy.

Do not recommend a research path that violates hard constraints without flagging it.

## Step 8 — Identify inherited-knowledge risk

If the project is inherited, reconstructed, or partly undocumented, explicitly classify unknown details.

Use:

- `RECOVERABLE_FROM_ARTIFACTS`
- `LIKELY_RECOVERABLE`
- `AUTHOR_CONFIRMATION_REQUIRED`
- `ORIGINAL_DATA_REQUIRED`
- `UNRECOVERABLE_CURRENTLY`

Examples:
- formula implied by code may be recoverable,
- exact instrument calibration may require original records,
- number of repeated trials should not be guessed.

Set conservative modification authority.

## Step 9 — Identify the decision bottleneck

Ask:

> What uncertainty currently prevents the next meaningful research decision?

Typical bottlenecks:
- unclear problem,
- unknown novelty,
- weak mechanism,
- no falsifiable hypothesis,
- experiment cannot identify the claim,
- result validity uncertain,
- manuscript claim-evidence mismatch,
- unknown venue requirement.

The bottleneck determines routing.

## Step 10 — Route to the smallest necessary module

Routing guide:

### To `idea-auditor`
When:
- idea value is unclear,
- feasibility/publication ceiling is uncertain,
- problem-method fit is weak.

### To `literature-mapper`
When:
- gap/novelty/prior-art uncertainty is the main blocker.

### To `hypothesis-builder`
When:
- problem/gap is stable but explanatory/testable formulation is weak.

### To `experiment-designer`
When:
- hypothesis/objective is stable and test design is the blocker.

### To `result-auditor`
When:
- experiments are complete but interpretation/validity is unresolved.

### To `paper-builder`
When:
- claims are sufficiently evidence-gated and organization/writing is the task.

### To `paper-auditor`
When:
- a complete or near-complete manuscript already exists and scientific audit is the goal.

Do not route to every module.

## Step 11 — Decide whether a Gate is already relevant

Possible gate status at intake:

- `NOT_REACHED`
- `READY_TO_EVALUATE`
- `BLOCKED`
- `ALREADY_PASSED_PROVISIONALLY`

Do not declare a Gate passed without performing the corresponding audit.

## Step 12 — Produce the Research Charter

Create a compact project charter containing:

1. Project identity.
2. Current objective.
3. Project type.
4. Current maturity stage.
5. Available artifacts.
6. Known facts.
7. User-reported facts.
8. Unknowns.
9. Preliminary problem/RQ/gap/hypothesis/contribution.
10. Constraints.
11. Current bottleneck.
12. Recommended next module.
13. Highest-value next action.

The charter should be short enough to stay useful.

## Step 13 — Initialize state files

At minimum, initialize/update:
- `research_state.yaml`
- `decision_log.md`

When relevant:
- `literature_ledger.yaml`
- `experiment_ledger.yaml`
- `claim_ledger.yaml`
- `paper_map.yaml`

Do not populate later-stage ledgers with fabricated placeholders presented as facts.

## Intake output status

Return one of:

- `ROUTABLE`: enough context exists to continue to a specific module.
- `ROUTABLE_WITH_UNKNOWNS`: work can continue, but important unknowns must remain explicit.
- `BLOCKED_BY_MISSING_ARTIFACT`: a required artifact is unavailable.
- `BLOCKED_BY_SCIENTIFIC_AMBIGUITY`: project cannot yet be routed reliably without resolving a core ambiguity.
- `ARCHIVE_OR_STOP_RECOMMENDED`: available evidence suggests continuing has little decision value.

Do not overuse blocking status; partial progress is preferable when safe.

## Required output

For a normal intake, return:

1. Project summary.
2. Immediate objective.
3. Project type.
4. Maturity stage.
5. Artifact inventory.
6. Evidence-status table: known / user-reported / inferred / unknown.
7. Preliminary research contract.
8. Constraints.
9. Inherited-knowledge risks if applicable.
10. Decision bottleneck.
11. Intake status.
12. Recommended next module.
13. Highest-decision-value next action.
14. Required updates to `research_state.yaml` and `decision_log.md`.

## Minimal intake mode

If the user only gives a short idea and wants to begin quickly:

Do not ask a long questionnaire.

Infer what can safely be inferred, mark unknowns, and route to `idea-auditor`.

Only request missing information when it materially changes the next decision.

## Existing-manuscript mode

If the user provides a completed paper:

Do not force the project back through idea/hypothesis stages.

Initialize state from the manuscript and route to `paper-auditor`, while marking unverified historical claims and methods as such.

## Reviewer-response mode

If reviewer comments are supplied:

Record:
- manuscript version,
- reviewer issue list,
- accepted/rejected/unclear concerns,
- whether new evidence is requested,
- whether the project is already accepted.

Route:
- scientific-evidence question -> relevant research module,
- manuscript correction -> `paper-builder` or `paper-auditor`,
- camera-ready -> conservative policy.

## Failure modes to flag

- asking an exhaustive questionnaire before doing useful work,
- treating user confidence as evidence,
- silently validating novelty,
- pretending inherited missing details are known,
- routing every project through every stage,
- ignoring resource constraints,
- confusing project maturity with manuscript polish,
- forcing hypothesis language onto pure engineering work,
- creating fake ledger entries,
- assuming publication is the only valid research outcome.
