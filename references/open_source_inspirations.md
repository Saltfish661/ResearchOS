# Open-source design inspirations

ResearchOS is an original synthesis. The project does not aim to copy another skill suite verbatim.

The Discovery Layer was informed by several public research-agent projects and their workflow ideas:

## K-Dense Scientific Agent Skills

Repository:
https://github.com/K-Dense-AI/scientific-agent-skills

Relevant concepts:
- scientific brainstorming as a separate stage from evidence validation;
- independent ideation before literature exposure when practical;
- explicit separation of ideas, assumptions, predictions, evidence, and decisions;
- handoff from brainstorming to literature, hypothesis, experiment design, statistics, and peer review.

The repository reports an MIT license.

## AI4S Skills

Repository:
https://github.com/ai4s-research/ai4s-skills

Relevant concepts:
- a research-explorer stage before literature survey/experiments/paper writing;
- scanning hot topics, open problems, surveys, benchmarks, applications, cross-field opportunities, and recent breakthroughs;
- producing a topic landscape and a pre-survey rather than immediately claiming novelty.

The repository reports an MIT license.

## Academic Research Skills

Repository:
https://github.com/vincenzoimp/academic-research-skills

Relevant concepts:
- SOTA exploration as a loop of search, citation chasing, triage, and paper digestion;
- immutable submitted artifacts;
- reviewers report problems rather than silently editing the reviewed artifact.

ResearchOS uses these ideas as architectural inspiration and does not depend on this repository's file formats.

## ResearchOS-specific additions

ResearchOS adds its own:
- evidence-state model,
- decision-value routing,
- claim/experiment/paper ledgers,
- Grill mode,
- Evidence Gate,
- explicit modification authority,
- current-literature Research Radar,
- trend-vs-opportunity distinction,
- crowding risk,
- claim wording controls,
- paper audit traceability.
