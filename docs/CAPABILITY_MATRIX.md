# ResearchOS Capability Matrix

Snapshot date: 2026-10-06

This document compares ResearchOS with several public research-agent / research-skill projects inspected from their repositories.

The goal is not to declare a winner. The goal is to identify:
- capabilities ResearchOS already covers well,
- capabilities where another project is clearly more mature,
- gaps worth absorbing into the next ResearchOS release,
- areas where ResearchOS should remain architecturally distinct.

## Projects inspected

1. **ResearchOS** — this repository.
2. **K-Dense Scientific Agent Skills** — `K-Dense-AI/scientific-agent-skills`.
3. **AI4S Skills** — `ai4s-research/ai4s-skills`.
4. **Academic Research Skills** — `vincenzoimp/academic-research-skills`.
5. **Research Skills (Eunomia)** — `eunomia-bpf/research-skills`.
6. **Academic Research Agent Skill** — `ngtiendong/Academic-Research-Agent-Skill`.
7. **paper-review.skill** — `jam-cc/paper-review.skill`.
8. **Paper Review Skill** — `JustAmply/paper-review-skill` (review-focused reference).

## Rating legend

- **● Strong** — explicit, first-class capability in the inspected workflow/docs.
- **◐ Partial** — capability exists but is supporting, narrower, or not yet a complete first-class module.
- **○ Not core / not observed** — not a major capability in the inspected materials.
- **—** — not meaningfully applicable to that project.

This is a design comparison, not an exhaustive benchmark. A repository may contain additional capabilities not inspected here.

## Matrix

| Capability | ResearchOS | K-Dense | AI4S | Academic Research Skills | Eunomia | Academic Research Agent | paper-review.skill |
|---|---:|---:|---:|---:|---:|---:|---:|
| Current-trend / research-radar discovery | ● | ◐ | ● | ◐ | ◐ | ◐ | ○ |
| Scientific brainstorming | ● | ● | ◐ | ○ | ◐ | ◐ | ○ |
| Structured research intake / routing | ● | ◐ | ◐ | ◐ | ● | ● | ○ |
| SOTA / literature search | ● | ● | ● | ● | ● | ● | ● |
| Citation chasing / paper digestion | ● | ● | ◐ | ● | ◐ | ● | ◐ |
| Gap / novelty audit | ● | ● | ◐ | ● | ● | ● | ● |
| Hypothesis generation / mechanism modeling | ● | ● | ◐ | ◐ | ◐ | ● | ○ |
| Math / formal claim specification | ◐ | ◐ | ○ | ◐ | ◐ | ● | ○ |
| Experiment design | ● | ● | ● | ● | ● | ● | ◐ |
| Statistics / power / assumption checks | ◐ | ● | ◐ | ◐ | ◐ | ◐ | ○ |
| Runnable experiment implementation | ○ | ◐ | ● | ◐ | ● | ● | ○ |
| Real experiment execution orchestration | ○ | ◐ | ● | ◐ | ● | ● | ○ |
| Result audit before claim promotion | ● | ◐ | ● | ◐ | ● | ● | ◐ |
| Explicit claim-evidence state machine | ● | ◐ | ◐ | ◐ | ● | ● | ◐ |
| Persistent project state / resume | ● (schema) | ◐ | ● | ● | ● | ● | ○ |
| Provenance / reproducible artifact tracking | ● (schema) | ● | ● | ● | ● | ● | ◐ |
| Figure generation | ◐ | ● | ● | ◐ | ● | ◐ | ○ |
| Figure integrity / visual QA | ◐ | ◐ | ● | ◐ | ◐ | ◐ | ○ |
| Paper story / manuscript construction | ● | ● | ● | ● | ● | ● | ○ |
| Claim-to-section traceability | ● | ◐ | ◐ | ● | ● | ● | ◐ |
| Citation verification | ● | ● | ● | ● | ● | ● | ● |
| Paper audit / reviewer simulation | ● | ● | ● | ● | ● | ● | ● |
| Numerical / image forensic integrity audit | ◐ | ◐ | ● | ○ | ◐ | ◐ | ○ |
| Rebuttal management | ○ | ◐ | ○ | ● | ◐ | ◐ | ◐ |
| Submission-round lifecycle | ○ | ○ | ○ | ● | ◐ | ◐ | ○ |
| Immutable submitted archives | ○ | ○ | ○ | ● | ◐ | ◐ | ○ |
| Camera-ready workflow | ◐ (audit policy only) | ◐ | ○ | ● | ◐ | ◐ | ○ |
| Venue packaging / artifact bundle | ○ | ◐ | ● | ● | ◐ | ◐ | ○ |
| Human approval gates | ● | ◐ | ◐ | ● | ● | ● | ○ |
| Resource / feasibility gate | ● | ● | ● | ● | ● | ● | ◐ |
| Negative-result preservation | ● | ● | ◐ | ◐ | ● | ● | ◐ |
| Domain-specific scientific tool library | ○ | ● | ◐ | ○ | ○ | ○ | ○ |
| Automated skill validation / smoke tests | ○ | ● | ● | ● | ◐ | ● | ◐ |
| Systematic review / formal evidence synthesis | ◐ | ● | ● | ● | ◐ | ◐ | ○ |

## What ResearchOS already does unusually well

### 1. Explicit epistemic-state control

ResearchOS distinguishes:

`OBSERVED -> INFERRED -> SUPPORTED`

and keeps `HYPOTHESIZED`, `UNKNOWN`, `AMBIGUOUS`, `CONTRADICTED`, and invalid evidence separate.

This is stronger than a workflow that only stores "results" and "claims" without controlling how evidence status changes.

### 2. Modification authority

The `SAFE / CONTEXTUAL / VERIFY / EVIDENCE_REQUIRED / DO_NOT_INVENT` model is especially useful for:
- inherited projects,
- old manuscripts,
- camera-ready repairs,
- incomplete experimental records.

This is a distinctive ResearchOS feature and should remain central.

### 3. Claim-evidence-paper traceability

ResearchOS explicitly links:

`RQ -> Hypothesis/Objective -> Experiment -> Observation -> Claim -> Section -> Conclusion`

This creates a strong foundation for both writing and auditing.

### 4. Separate Result Auditor

Many workflows combine experiment execution and interpretation. ResearchOS explicitly inserts a scientific review layer before claim promotion.

That separation should be preserved even after experiment execution is added.

### 5. Discovery + adversarial gates

The combination of:
- Research Radar,
- Scientific Brainstorming,
- Idea Auditor,
- Grill mode,

creates a useful distinction between idea generation and idea validation.

## Capabilities where other projects are currently more mature

### K-Dense: scientific methods and domain tooling

K-Dense is far ahead in:
- dedicated statistical-analysis procedures,
- experimental-design variants,
- power/effect-size support,
- domain-specific databases and packages,
- specialized science workflows,
- skill validation/testing.

ResearchOS should not try to reproduce 100+ domain tools internally.

Better approach:
- build adapter/handoff contracts,
- reuse mature domain/statistics skills where available,
- keep ResearchOS as the scientific-governance layer.

### AI4S: runnable experiments, figures, provenance, resumable execution

AI4S has a mature package-oriented experiment workflow:
- data contract,
- runnable code,
- explicit `measured / simulated / illustrative` provenance,
- results JSON,
- publication figures,
- figure manifests,
- incremental execution and resume.

ResearchOS currently designs experiments but does not execute them.

This is the largest practical gap.

### Academic Research Skills: SOTA digestion and submission lifecycle

This project is especially mature in:
- citation chasing,
- triage queues,
- atomic paper digestion,
- immutable submitted versions,
- concern maps,
- rebuttal/revision/camera-ready lifecycle,
- venue artifact packaging.

ResearchOS should absorb the lifecycle ideas, not copy its repository layout.

### Eunomia: orchestration and paper-decision value

Eunomia provides strong ideas around:
- persistent outer orchestration,
- resume after context loss,
- gate ownership,
- one-way scientific authority,
- paper-decision value,
- independent result review.

ResearchOS already shares several principles but lacks a runtime-grade orchestrator and recovery protocol.

### Academic Research Agent: reality gates and formalization

Particularly valuable ideas:
- minimum formal definition needed to falsify a claim,
- reality/feasibility certificates,
- cheapest decisive falsifier,
- explicit allowed/prohibited work at each gate,
- reopening upstream gates when core assumptions change.

ResearchOS should strengthen formalization and execution authorization using these concepts.

### paper-review.skill: review evidence discipline

Useful review-specific ideas:
- every major criticism must point to a concrete claim/evidence problem,
- novelty critique should identify closest prior work,
- external references used in review should be verified,
- do not invent weaknesses merely to sound strict.

ResearchOS Paper Auditor already aligns strongly with this.

## Important architectural differences to preserve

ResearchOS should not become a monolithic autonomous paper generator.

Keep these boundaries:

1. **Discovery is not validation.**
2. **Writing cannot create scientific authority.**
3. **Execution cannot silently rewrite the research question.**
4. **Reviewers provide evidence/critique, not automatic instructions.**
5. **Failed hypotheses remain failed until a new hypothesis is explicitly created.**
6. **A later polished manuscript must not overwrite provenance of earlier scientific decisions.**
7. **Current public literature should be searched when novelty/trend claims are material.**
8. **ResearchOS should orchestrate mature external/domain skills instead of cloning all of them.**

## Recommended integration strategy

Do not import other repositories wholesale.

Use three layers:

### Layer A — ResearchOS core

Own:
- state machine,
- scientific contract,
- evidence states,
- ledgers,
- routing,
- gates,
- decision log,
- modification authority,
- claim-paper traceability.

### Layer B — ResearchOS specialist modules

Own:
- discovery,
- idea audit,
- literature mapping,
- hypothesis building,
- experiment design,
- result audit,
- paper building,
- paper audit,
- submission/rebuttal lifecycle.

### Layer C — External capability adapters

Delegate where mature tools already exist:
- statistics,
- domain-specific analysis,
- code execution,
- figure rendering,
- bibliographic lookup,
- PDF ingestion,
- dataset/model tooling,
- scientific databases.

This keeps ResearchOS small enough to remain coherent while still benefiting from the open ecosystem.

## Highest-value gaps

Ranked by impact on end-to-end research quality:

1. **Experiment execution + provenance**
2. **Statistical-analysis adapter**
3. **Source/PDF ingestion + atomic paper digestion**
4. **Runtime checkpoint / resume / validation**
5. **Submission / rebuttal / camera-ready manager**
6. **Math / claim formalizer**
7. **Figure builder + figure auditor**
8. **Venue profile / artifact packaging**
9. **Systematic review / meta-analysis mode**
10. **Domain adapters**
11. **Integrity-forensics extensions**

These priorities are used in the V0.2 roadmap.
