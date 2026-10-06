# ResearchOS

ResearchOS is an evidence-first, human-guided research skill framework for carrying a research project from idea formation to manuscript audit and submission readiness.

Its central goal is not to automate science end-to-end. Instead, it keeps research questions, literature, hypotheses, experiments, claims, decisions, and manuscript text connected through an auditable research state.

## V0.1 principles

1. Evidence before prose.
2. Writing has no scientific authority: manuscript generation may express accepted claims but may not create facts.
3. Scientific claims must be traceable to literature, observation, experiment, analysis, or an explicit human decision.
4. AI may propose pivots but must not silently change the scientific contract.
5. Negative and failed experiments remain part of the research record.
6. Research facts move through explicit epistemic states: `HYPOTHESIZED -> OBSERVED -> SUPPORTED` when warranted.
7. Uncertainty must be preserved rather than polished away.
8. Red-team review attacks the current research contract; it should not expand scope merely because more work is possible.

## Core workflow

Research Intake -> Idea Audit -> Literature Map -> Hypothesis Builder -> Experiment Designer -> Result Auditor -> Paper Builder -> Paper Auditor

Cross-stage mode: `Grill / Red Team`

Planned downstream modules: venue/submission and review/rebuttal/camera-ready.

## State files

- `templates/research_state.yaml`
- `templates/literature_ledger.yaml`
- `templates/claim_ledger.yaml`
- `templates/experiment_ledger.yaml`
- `templates/decision_log.md`

## Status

V0.1 scaffold. The first fully specified module is `skills/idea-auditor/`.
