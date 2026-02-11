---
title: Human vs GenAI capability map (engineering view)
permalink: /articles/agent-architecture/human-vs-genai-capability-map/
summary: A practical mapping of human cognitive capabilities to GenAI limitations, engineering substitutes, and residual gaps.
---

## Abstract

This note provides a practical “capability map” for designing agentic systems: for each target capability, it lists (1) the typical limitation in current GenAI systems, (2) an engineering substitute, (3) common implementation techniques, and (4) the residual gap that remains.

The goal is not neuroscience completeness. The goal is fast, explicit tradeoff reasoning when you design memory, retrieval, planning, and safety layers around an LLM.

## Capability map

This page renders the table from an internal `_data` file at build time (no CSV download link is published).

{% assign rows = site.data["human-vs-genai-capability-map"] %}

{% assign rows = site.data["human-vs-genai-capability-map"] %}

<div class="capability-map-wrapper" role="region" aria-label="Human vs GenAI capability map">
  <table class="capability-map">
    <caption class="capability-map__caption">Human vs GenAI capability map</caption>
    <thead>
      <tr>
        <th>Target capability</th>
        <th>Human implementation</th>
        <th>GenAI limitation</th>
        <th>GenAI alternative</th>
        <th>Techniques/tools</th>
        <th>Residual gaps</th>
      </tr>
    </thead>
    <tbody>
      {% for row in rows %}
        <tr>
          <td data-label="Target capability">{{ row["Target capability"] | escape }}</td>
          <td data-label="Human implementation">{{ row["Human implementation"] | escape }}</td>
          <td data-label="GenAI limitation">{{ row["GenAI limitation"] | escape }}</td>
          <td data-label="GenAI alternative">{{ row["GenAI alternative"] | escape }}</td>
          <td data-label="Techniques/tools">{{ row["Techniques/tools"] | escape }}</td>
          <td data-label="Residual gaps">{{ row["Residual gaps"] | escape }}</td>
        </tr>
      {% endfor %}
    </tbody>
  </table>
</div>

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

- Articles → Model training and evaluation → Fluency vs factuality: [Fluency Is Not Factuality]({{ '/articles/model-training-and-eval/fluency-vs-factuality/' | relative_url }})
- Policies: Facts-only / Evidence rules (when accuracy matters): [Policies]({{ '/policies/' | relative_url }})
