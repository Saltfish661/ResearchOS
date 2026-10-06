---
name: paper-builder
description: Convert validated research state, literature, experiments, and evidence-gated claims into a coherent manuscript structure and draft without creating new scientific facts. Build the paper story, contribution map, section responsibilities, figure/table plan, claim-to-evidence traceability, and calibrated prose.
version: 0.1.0
---

# Paper Builder

## Goal

Construct a manuscript from accepted scientific state.

This module is a writing and organization layer. It has no authority to invent:
- experiments,
- data,
- sample sizes,
- metrics,
- statistical significance,
- methods,
- citations,
- mechanism evidence,
- limitations that were not actually assessed,
- claims stronger than those approved by the evidence state.

Core rule:

`Writing has no scientific authority.`

Preferred chain:

`Research state -> accepted claims -> evidence map -> paper story -> section plan -> figure/table plan -> paragraph plan -> prose`

Never reverse this chain by inventing evidence to fill a narrative gap.

## Entry conditions

Use this module when:
- the research question and contribution are sufficiently stable;
- central claims have passed the Evidence Gate or are explicitly marked provisional;
- literature support exists for background/gap claims;
- experiment/result records are traceable;
- unresolved scientific blockers are known.

If central claims are still ambiguous or unsupported, route to `result-auditor`.

If novelty/gap framing is still uncertain, route to `literature-mapper`.

## Writing authority levels

Every manuscript statement should derive from one of:

- `SOURCE_BACKED`: supported by literature.
- `EVIDENCE_BACKED`: supported by project evidence.
- `METHOD_DESCRIPTION`: describes an implemented method/protocol.
- `INTERPRETATION`: allowed inference from accepted claims.
- `LIMITATION`: bounded statement of known uncertainty.
- `TRANSITION`: rhetorical glue with no scientific content.

Statements requiring unavailable evidence must be marked:
- `BLOCKED`
- `VERIFY`
- `EVIDENCE_REQUIRED`

Do not silently write around them.

## Step 1 — Define the paper type and audience

Determine:
- journal / conference / thesis / report / workshop / short paper,
- field and subfield,
- target audience,
- expected contribution style,
- expected section structure,
- length constraints if known,
- venue requirements if known.

Do not hard-code venue rules; use a later venue/submission module or current official guidance when needed.

## Step 2 — Define the paper's one-sentence story

Write one sentence answering:

> What did this research discover, establish, or enable that matters?

Prefer scientific value over implementation chronology.

Weak:
"We propose Model X with modules A, B, and C."

Stronger:
"We show that failure mode F under condition C can be mitigated by intervention X, with evidence supporting mechanism M under the evaluated settings."

For systems work:
"We demonstrate a system architecture that achieves capability X under constraint Y while preserving Z."

If a convincing one-sentence story cannot be written from supported claims, stop and surface the scientific gap rather than manufacturing a narrative.

## Step 3 — Build the contribution map

Every contribution must be classified.

Possible types:
- problem characterization,
- methodological,
- mechanistic,
- empirical,
- system/integration,
- dataset/resource,
- evaluation/protocol,
- theoretical,
- application.

For each contribution record:
- contribution statement,
- linked claim IDs,
- linked evidence IDs,
- novelty basis,
- manuscript section,
- strength/boundary,
- unresolved risk.

Avoid contribution lists where every bullet is merely a feature of the method.

## Step 4 — Build the argument skeleton

Construct the paper as an argument.

Recommended logic:

`Problem -> Gap -> Insight/Hypothesis -> Method/Approach -> Evidence -> Interpretation -> Implication`

Map each section to a responsibility.

### Title
Signal the central contribution without overclaim.

### Abstract
Answer:
- problem,
- gap,
- approach,
- key evidence,
- bounded conclusion.

### Introduction
Establish:
- why the problem matters,
- what existing work does,
- what remains unresolved,
- what this paper does,
- what is contributed.

### Related Work / Background
Position the project against relevant method/problem families.
Do not turn it into a chronological bibliography dump.

### Methods
Describe what was actually implemented or executed.
Do not mix result interpretation into the method.

### Results
Report observations and evidence.
Do not hide negative or contradictory findings required to interpret the claims.

### Discussion
Interpret results, compare alternatives/prior work, state limitations, and bound generalization.

### Conclusion
Answer the original research question at the same strength supported by evidence.

## Step 5 — Create claim-to-section traceability

For every central claim, map:
- claim ID,
- evidence IDs,
- section(s) where it appears,
- first point of introduction,
- result location,
- discussion location,
- conclusion wording.

A central claim that appears in Abstract/Conclusion but has no Results evidence link is a blocking defect.

Do not duplicate a claim with gradually stronger wording across sections.

## Step 6 — Build the figure and table plan

Figures and tables should carry evidence or explain necessary structure.

For each item define:
- ID,
- purpose,
- message,
- linked claims,
- source data/artifact,
- expected caption content,
- whether it is evidential or explanatory.

Possible roles:
- system/method overview,
- data flow,
- experiment setup,
- main quantitative evidence,
- ablation,
- mechanism evidence,
- robustness,
- qualitative/failure cases,
- resource/system tradeoff.

Avoid decorative figures that do not support comprehension or evidence.

Every quantitative figure/table must be traceable to experiment artifacts.

## Step 7 — Build paragraph-level evidence plans

Before drafting important paragraphs, define:

- paragraph purpose,
- primary claim,
- supporting evidence/source,
- qualifier/boundary,
- transition.

Suggested structure:

`Claim -> Evidence -> Interpretation -> Boundary -> Link to next point`

Not every paragraph needs all elements, but scientific assertions must not float without support.

## Step 8 — Draft the Introduction from the gap chain

Build:

1. broad problem,
2. concrete consequence,
3. current solution landscape,
4. documented limitation/gap,
5. project insight or question,
6. high-level approach,
7. contribution list.

Check that the gap is literature-backed.

Do not write:
"However, no existing studies..."
unless the literature map justifies it.

Prefer:
"Existing work has primarily focused on X, while Y remains insufficiently evaluated under Z."

## Step 9 — Draft Related Work by comparison dimensions

Organize by meaningful research families, not paper-by-paper chronology.

For each family:
- what it solves,
- how it works,
- strengths,
- unresolved limitations,
- relation to current work.

End with a precise positioning statement.

Avoid adversarial misrepresentation of prior work merely to make novelty look stronger.

## Step 10 — Draft Methods with implementation fidelity

Methods must match what was actually done.

Check:
- terminology consistency,
- algorithm steps,
- parameters,
- equations,
- preprocessing,
- data split,
- environment,
- instrumentation,
- baselines,
- evaluation protocol.

If an implementation detail is unknown:
- mark `VERIFY` or `EVIDENCE_REQUIRED`;
- do not invent a conventional default.

Distinguish:
- conceptual method,
- implementation choices,
- experimental protocol.

## Step 11 — Draft Results evidence-first

Use the order that best answers the RQs, not necessarily experiment execution chronology.

For each result subsection:

1. question,
2. experiment reference,
3. direct observations,
4. uncertainty,
5. bounded interpretation.

Do not lead with interpretation before reporting the observation.

Do not selectively omit valid negative results when they materially affect the claim.

## Step 12 — Draft Discussion as interpretation, not repetition

Discussion should address:
- what the evidence means,
- why the result may have occurred,
- which alternatives remain,
- relation to prior work,
- failure cases,
- limitations,
- generalization boundary,
- implications.

Mechanism language must respect the mechanism-evidence level from `claim_ledger.yaml`.

M0-M1 evidence should not become a strong mechanistic conclusion in Discussion.

## Step 13 — Draft limitations honestly

A limitation is not a ceremonial paragraph.

Prioritize limitations that affect:
- identification,
- generalization,
- measurement,
- sample/data scope,
- implementation,
- external validity,
- resource assumptions,
- reproducibility.

For each limitation, state:
- what is limited,
- how it affects interpretation,
- what remains defensible despite it.

Do not add generic limitations that are not actually relevant.

## Step 14 — Draft the Conclusion by answering RQs

Conclusion should:
- answer the original question,
- summarize strongest supported contributions,
- preserve evidence boundaries,
- avoid introducing new results or claims.

Check:
`conclusion strength <= evidence strength`

## Step 15 — Calibrate wording globally

Use allowed/forbidden wording from `claim_ledger.yaml`.

Examples:

If claim is `INFERRED / MODERATE`:
- prefer "suggests", "supports", "is consistent with".

If evidence is bounded to one benchmark:
- use "under the evaluated setting".

Avoid global phrases like:
- "universally",
- "proves",
- "fully solves",
- "state-of-the-art" without verified comparison,
- "significant" when statistical significance is not established or when only practical significance is meant.

## Step 16 — Check contribution consistency

Ensure contribution statements match across:
- Abstract,
- Introduction,
- Methods,
- Results,
- Discussion,
- Conclusion.

If Introduction promises four contributions but Results only support three, do not hide the mismatch.

Either:
- provide evidence,
- narrow the contribution,
- remove it,
- mark the manuscript blocked.

## Step 17 — Preserve uncertainty and negative evidence

Do not polish away:
- null results,
- contradictory findings,
- ambiguous mechanism evidence,
- failed generalization,
- unexplained variance.

The narrative may prioritize central findings, but material counterevidence must remain visible where it affects interpretation.

## Step 18 — Citation discipline

For each literature-backed statement:
- use verified literature entries where possible,
- cite the closest primary evidence,
- avoid citation laundering through secondary sources,
- ensure the cited source actually supports the sentence.

Do not fabricate citations.

If citation identity/support is uncertain:
- mark `VERIFY`.

## Step 19 — Equation and notation discipline

For technical manuscripts:
- define symbols at first use,
- use stable variable names,
- ensure equations correspond to implemented methods,
- distinguish definitions from derived results,
- define nonstandard metrics mathematically when they support important conclusions.

Do not add equations merely to make the paper appear rigorous.

## Step 20 — Build manuscript traceability map

Maintain a paper map that links:

`Section -> Paragraph -> Claim -> Evidence/Source -> Figure/Table -> Epistemic state`

At minimum, central claims must be traceable.

This map is the handoff artifact for `paper-auditor`.

## Step 21 — Drafting sequence

Preferred sequence for evidence-driven manuscripts:

1. Results figures/tables,
2. Results text,
3. Methods,
4. Discussion,
5. Introduction/Related Work,
6. Conclusion,
7. Abstract,
8. Title.

This is a recommendation, not a rigid requirement.

Rationale:
the paper story should be constrained by actual evidence rather than by an early abstract promise.

## Step 22 — Manuscript readiness status

Classify:

- `DRAFTABLE`: core evidence sufficient; manuscript can be written.
- `DRAFTABLE_WITH_BLOCKERS`: writing can proceed but named scientific gaps remain.
- `NOT_DRAFTABLE`: central claims lack sufficient evidence or traceability.
- `READY_FOR_AUDIT`: full draft exists and central claim/evidence links are established.

## Required output

For a normal paper-building run, return:

1. Paper type and intended audience.
2. One-sentence paper story.
3. Research question -> answer map.
4. Contribution map.
5. Section responsibility map.
6. Claim-to-section traceability.
7. Figure/table plan.
8. Paragraph-level evidence plan for major sections.
9. Draft or revision of requested sections.
10. Blocked statements requiring verification/evidence.
11. Global wording/overclaim constraints.
12. Manuscript readiness status.
13. Updates required to `paper_map.yaml`, `claim_ledger.yaml`, and `decision_log.md`.

## Paper map discipline

Create or update `paper_map.yaml`.

Do not create duplicate scientific claims simply because the same result appears in multiple sections. Reuse stable claim IDs.

A wording change that materially strengthens scientific meaning must trigger claim review.

## Handoff rules

### Back to `result-auditor`
When:
- a desired manuscript statement exceeds evidence strength,
- a core claim lacks Evidence Gate approval,
- an interpretation requires unresolved alternative explanations.

### Back to `literature-mapper`
When:
- Introduction/Related Work needs a stronger gap basis,
- novelty positioning is unsupported,
- a citation does not actually support the manuscript statement.

### Back to `experiment-designer`
When:
- the manuscript exposes a truly essential missing experiment.

Do not request extra experiments merely to make the paper look more complete.

### To `paper-auditor`
When:
- a complete or near-complete manuscript exists,
- central claims are traceable,
- unresolved blockers are explicitly marked.

## Failure modes to flag

- writing invents facts,
- Abstract promises unsupported contributions,
- Introduction overstates novelty,
- Methods contain guessed implementation details,
- Results mix observation and speculation,
- Discussion upgrades correlations into mechanisms,
- valid negative evidence is hidden,
- Conclusion is stronger than Results,
- citations do not support their sentences,
- figures lack evidence provenance,
- contribution list does not match evidence,
- terminology changes across sections,
- paper story is optimized for novelty at the expense of truth.
