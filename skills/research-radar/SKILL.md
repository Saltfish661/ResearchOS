---
name: research-radar
description: Scan current literature, venues, benchmarks, open problems, emerging methods, and cross-field signals to build an evidence-linked research opportunity map before committing to a specific idea.
version: 0.1.0
---

# Research Radar

## Goal

Discover promising research directions from the current scientific landscape.

This skill is for users who have:
- a broad field but no concrete idea,
- a desire to know what is currently moving,
- a need to identify open problems or emerging opportunities,
- uncertainty about which subfield is worth entering.

It should not declare novelty or generate a final research claim.

## Core principle

Hot != important.
Popular != underexplored.
Recent != good.
Sparse literature != valuable gap.

Research Radar separates trend signals from opportunity signals.

## Inputs

At minimum:
- broad field/direction.

Optional:
- subfield,
- target venue family,
- preferred research style,
- resource constraints,
- time horizon,
- desired novelty/risk level,
- available datasets/equipment.

## Scan dimensions

Search the landscape across these dimensions:

1. Recent breakthroughs
2. Fast-growing topics
3. Open problems/challenges
4. Recent surveys/reviews
5. New benchmarks/datasets/evaluation protocols
6. New methods/architectures/tools
7. Important negative results or known bottlenecks
8. Applications with unresolved technical barriers
9. Cross-field transfer opportunities
10. Replication/reproducibility gaps

Do not require every dimension when irrelevant.

## Time windows

Use multiple recency windows when current search is available:

- pulse: last 30-90 days
- emerging: last 6-12 months
- trend: last 2-3 years
- foundation: older canonical work as needed

Always record the search date.

Do not compare raw citation counts between very recent and older papers as if they were equivalent.

## Preferred sources

Use primary and authoritative sources where possible:
- official conference/journal proceedings,
- arXiv/bioRxiv/medRxiv or relevant preprint servers,
- Semantic Scholar/OpenAlex/Crossref-style scholarly indexes,
- official benchmark/dataset pages,
- accepted-paper lists,
- authoritative surveys,
- code repositories only as implementation/adoption signals.

Search snippets and social posts are discovery signals, not scientific evidence.

## Trend signals

For each topic, inspect multiple signals:

- publication velocity,
- appearance across multiple venues/labs,
- recent survey attention,
- benchmark creation or benchmark turnover,
- repeated "open challenge" statements,
- new datasets/tools enabling previously difficult work,
- strong growth in adjacent fields,
- replication failures or unresolved contradictions,
- practical deployment pressure.

Classify:
- EMERGING
- ACCELERATING
- ESTABLISHED
- CROWDED
- UNCLEAR

Do not infer trend status from one viral paper.

## Opportunity signals

A topic becomes a research opportunity only when at least one of these is plausible:

- unresolved mechanism,
- documented failure mode,
- under-tested regime,
- benchmark blind spot,
- resource/efficiency constraint,
- cross-domain transfer gap,
- contradictory evidence,
- reproducibility gap,
- newly enabled experiment,
- new dataset/instrument/tool changes what can be tested.

Record both supporting and weakening evidence.

## Crowding risk

Estimate whether the field is moving too quickly or is already saturated.

Signals:
- many nearly identical papers in a short period,
- benchmark improvements with shrinking effect sizes,
- rapid convergence on one method family,
- high dependence on inaccessible compute/data,
- frequent simultaneous discovery.

Classify:
- LOW
- MEDIUM
- HIGH
- UNKNOWN

Crowding is not automatically bad, but it changes feasibility and novelty risk.

## Research-opportunity map

For each candidate direction record:

- title,
- problem,
- why now,
- trend status,
- evidence of importance,
- open question,
- closest method families,
- data/benchmark availability,
- feasibility,
- compute/data burden,
- crowding risk,
- likely contribution types,
- key papers,
- uncertainties,
- recommended next search.

## Search procedure

### Phase 1 — Landscape reconnaissance

Identify:
- major subfields,
- terminology,
- current venue clusters,
- canonical benchmarks,
- recent surveys.

### Phase 2 — Recent-paper pulse

Search recent papers from the pulse/emerging windows.

Prioritize:
- topically central papers,
- papers cited or discussed by multiple recent works,
- new benchmarks,
- methods changing evaluation practice,
- papers exposing limitations.

### Phase 3 — Open-problem mining

Search:
- limitations sections,
- future-work sections,
- challenge/survey papers,
- benchmark error analyses,
- negative/contradictory studies.

Treat author-stated future work as a lead, not automatically a valuable gap.

### Phase 4 — Cross-field scan

For promising bottlenecks, search 1-3 adjacent fields for:
- mature methods not yet transferred,
- similar mechanism problems under different names,
- tools or theory newly applicable to the target field.

### Phase 5 — Candidate synthesis

Produce 5-12 candidate directions.

Do not rank solely by trendiness.

## Candidate scoring

Use non-additive diagnostic dimensions:

- scientific importance,
- evidence that the problem is real,
- opportunity plausibility,
- freshness,
- crowding risk,
- feasibility,
- resource fit,
- mechanism depth,
- experimentability,
- likely publication ceiling.

Use LOW/MEDIUM/HIGH/UNKNOWN or bounded numeric scores with reasons.

A fatal feasibility or prior-art risk can dominate the decision.

## Output

Return:

1. Scope and scan date.
2. Landscape map.
3. Trend signals.
4. Open problems and bottlenecks.
5. Recent enabling developments.
6. Cross-field opportunities.
7. Candidate direction table.
8. Crowding risks.
9. 3-5 directions worth brainstorming.
10. Search blind spots.
11. Handoff to `scientific-brainstorming` or `literature-mapper`.

## Handoff

To `scientific-brainstorming` when:
- the goal is to generate candidate research concepts from the opportunity map.

To `literature-mapper` when:
- one direction is already sufficiently specific to validate prior art/gap.

To `research-intake` when:
- the user selects a direction and wants to initialize a project.

## Failure modes

- confusing social buzz with scientific trend,
- using memory-only papers for a current scan,
- treating one recent paper as a field-wide trend,
- recommending only fashionable topics,
- ignoring resource mismatch,
- presenting a future-work sentence as a validated gap,
- declaring novelty during discovery,
- hiding crowding/simultaneous-discovery risk.
