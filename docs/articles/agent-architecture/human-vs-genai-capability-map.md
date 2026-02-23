---
title: Human vs GenAI capability map (engineering view)
permalink: /articles/agent-architecture/human-vs-genai-capability-map/
summary: A practical mapping of human cognitive capabilities to GenAI limitations, engineering substitutes, and residual gaps.
author: Tamar Peretz
published: 2026-02-22
---

## Abstract

This note is an **engineering-facing capability map** for designing LLM/agent-adjacent systems. For each target capability, it summarizes:

1) the typical limitation in current LLM/GenAI systems,  
2) an engineering substitute layer,  
3) common implementation techniques, and  
4) the residual gap that remains in production.

This is not a neuroscience reference. The “Human implementation” column is a compact **informal analogue** intended to support engineering tradeoffs.

## Capability map

This page renders the table from an internal `_data` file at build time (no CSV download link is published).

{% assign rows = site.data["human-vs-genai-capability-map"] %}

<div class="capability-map-wrapper" role="region" aria-label="Human vs GenAI capability map">
  <table class="capability-map">
    <caption class="capability-map__caption">Human vs GenAI capability map</caption>
    <thead>
      <tr>
        <th scope="col">Target capability</th>
        <th scope="col">Human implementation (informal)</th>
        <th scope="col">GenAI limitation</th>
        <th scope="col">GenAI alternative</th>
        <th scope="col">Techniques/tools</th>
        <th scope="col">Residual gaps</th>
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

1) **Scope your system**
- Mark which capabilities your product actually needs (memory, planning, tool-use, grounding, provenance, robustness).
- Anything you don’t need becomes an explicit non-goal (reduces complexity and attack surface).

2) **Choose the substitute layer explicitly**
- If the limitation is “no stable memory” → prefer retrieval + governed storage.
- If the limitation is “short horizon / drift” → prefer explicit task graphs, bounded workflows, or controller-enforced state machines.
- If the limitation is “brittle reliability” → add verification layers (validators, tests, grounded citations, structured outputs).

3) **Treat “Residual gaps” as tracked design risk**
Residual gaps are where production systems typically fail (consistency, provenance, safety, interpretability). Track them as explicit risks with mitigations, not as footnotes.

## What this table is (and is not)

- **Is:** an engineering checklist for architecture decisions.
- **Is not:** a mechanistic claim about human cognition, and not evidence that LLMs “possess” the human capability. It is a tradeoff map.

## Terminology (to avoid “internal language”)

- **RAG (Retrieval-Augmented Generation):** retrieval + generation pattern for knowledge-intensive tasks.
- **BM25:** a standard probabilistic lexical retrieval scoring function used in classical IR.
- **ReAct:** prompting/agent pattern combining reasoning traces with tool/action steps.
- **MC-dropout:** Monte-Carlo dropout used as an approximate uncertainty estimation technique (common in deep learning literature).
- **CAS:** computer algebra system.
- **SMT:** satisfiability modulo theories solver.
- **OOD:** out-of-distribution.

## References (primary / formal)

- Lewis et al. (2020). *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks.* arXiv:2005.11401. https://arxiv.org/abs/2005.11401
- Yao et al. (2022). *ReAct: Synergizing Reasoning and Acting in Language Models.* arXiv:2210.03629. https://arxiv.org/abs/2210.03629
- Gal & Ghahramani (2016). *Dropout as a Bayesian Approximation: Representing Model Uncertainty in Deep Learning.* arXiv:1506.02142. https://arxiv.org/abs/1506.02142
- Robertson & Zaragoza (2009). *The Probabilistic Relevance Framework: BM25 and Beyond.* https://doi.org/10.1561/1500000019
- OWASP Cheat Sheet Series. *AI Agent Security Cheat Sheet.* https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html
- OpenAI Docs. *Safety in building agents (prompt injection guidance).* https://developers.openai.com/api/docs/guides/agent-builder-safety/
- NIST. *NIST AI 600-1: Generative AI Profile.* https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf

## Suggested next read in this repo

- Articles → Model training and evaluation → Fluency vs factuality: [Fluency Is Not Factuality]({{ '/articles/model-training-and-eval/fluency-vs-factuality/' | relative_url }})
- Articles → Model training and evaluation → Sycophancy: [Sycophancy in LLM Assistants]({{ '/articles/model-training-and-eval/sycophancy-agreement-bias/' | relative_url }})
- Policies: Facts-only / Evidence rules (when accuracy matters): [Policies]({{ '/policies/' | relative_url }})