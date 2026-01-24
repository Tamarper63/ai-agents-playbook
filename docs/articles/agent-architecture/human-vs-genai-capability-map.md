---
title: Human vs GenAI capability map (engineering view)
permalink: /articles/agent-architecture/human-vs-genai-capability-map/
summary: A practical mapping of human cognitive capabilities to GenAI limitations, engineering substitutes, and residual gaps.
---

## Abstract

This note provides a practical “capability map” for designing agentic systems: for each target capability, it lists (1) the typical limitation in current GenAI systems, (2) an engineering substitute, (3) common implementation techniques, and (4) the residual gap that remains.

The goal is not neuroscience completeness. The goal is fast, explicit tradeoff reasoning when you design memory, retrieval, planning, and safety layers around an LLM.

## Data (CSV)

- Download the full table: [human-vs-genai-capability-map.csv]({{ '/assets/data/human-vs-genai-capability-map.csv' | relative_url }})

## How to use this map

1) **Scope your agent**
- Mark which capabilities your product actually needs (memory, planning, tool-use, grounding, etc.).
- Anything you *don’t* need becomes an explicit non-goal (reduces complexity).

2) **Choose the substitute layer**
- If the limitation is “no stable memory” → prefer retrieval + governed storage.
- If the limitation is “short horizon / drift” → prefer explicit planners, task graphs, or bounded workflows.
- If the limitation is “brittle reliability” → add verification layers (validators, tests, grounded citations).

3) **Treat “Residual gaps” as design risk**
Residual gaps are where production systems typically fail (consistency, provenance, safety, interpretability). Track them as risks, not as footnotes.

## What this table is (and is not)

- **Is:** an engineering checklist for agent architecture decisions.
- **Is not:** a claim of biological accuracy for each “Human implementation” phrase. If you need academic-grade claims, cite primary sources separately.

## Suggested next read in this repo

- Notes → Model training and evaluation → Fluency vs factuality: [Fluency Is Not Factuality]({{ '/notes/model-training-and-eval/fluency-vs-factuality/' | relative_url }})
- Policies: Facts-only / Evidence rules (when accuracy matters): [Policies]({{ '/policies/' | relative_url }})
