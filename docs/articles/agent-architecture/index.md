---
title: Agent architecture
permalink: /articles/agent-architecture/
show_title: false
---

This page is the **hub** for agent-architecture articles.

It focuses on engineering concerns in multi-step tool-using systems:
- **Control flow patterns** (orchestrator-led vs model-led)
- **State and lifecycle management** (what persists, what resets, and when)
- **Tool invocation semantics** (selection, authorization, validation, error handling)
- **Retrieval and context management** (what enters context, and why)
- **Evaluation harnesses** for multi-step workflows (tests, regressions, robustness)

## Start here (pick the job)

| If you need… | Start with | Then |
|---|---|---|
| A concrete model for **what enters context** and why (selection + persistence) | {% include page-title-link.html url="/articles/agent-architecture/llm-memory-boundary-model/" fallback="LLM memory boundary model" %} | {% include page-title-link.html url="/how-to/llm-memory-boundaries/" fallback="Manage: LLM memory boundaries (procedure)" %} |
| A decision on **where the control plane lives** (LLM-led vs orchestrator-led) | {% include page-title-link.html url="/articles/agent-architecture/llm-led-vs-orchestrator-led-tool-execution/" fallback="LLM-led vs orchestrator-led tool execution (tradeoffs)" %} | {% include page-title-link.html url="/articles/agent-security/controller-loop-attack-surface/" fallback="Controller-loop attack surface" %} |
| A framing for **what should be automated** vs kept human-owned (capability + failure modes) | {% include page-title-link.html url="/articles/agent-architecture/human-vs-genai-capability-map/" fallback="Human vs GenAI capability map" %} | {% include page-title-link.html url="/how-to/engineering-quality-gate-procedure/" fallback="Engineering Quality Gate — Procedure" %} |

## Key terms (as used in this section)

- **Orchestrator-led**: a controller sequences steps and enforces policy; the model is called for scoped sub-tasks.
- **Model-led**: the model proposes next actions/tool calls within constraints enforced by the orchestrator.
- **Control plane**: where routing/authorization/validation decisions are enforced (model vs controller vs middleware).

## Articles (curated)

- **{% include page-title-link.html url="/articles/agent-architecture/llm-memory-boundary-model/" fallback="LLM memory boundary model" %}**  
  Context assembly as a boundary: candidate inputs vs control-plane selection and persistence.

- **{% include page-title-link.html url="/articles/agent-architecture/llm-led-vs-orchestrator-led-tool-execution/" fallback="LLM-led vs orchestrator-led tool execution" %}**  
  Control-plane placement tradeoffs across reliability, observability, safety, latency, cost governance, and testability.

- **{% include page-title-link.html url="/articles/agent-architecture/human-vs-genai-capability-map/" fallback="Human vs GenAI capability map" %}**  
  Capability framing for task assignment, failure modes, and where automation breaks down.

## Related (for execution + contracts)

- Procedures: {% include page-title-link.html url="/how-to/" fallback="How-to" %} · {% include page-title-link.html url="/how-to/choose-facts-only-evidence-boundary/" fallback="Choose an evidence boundary" %} · {% include page-title-link.html url="/how-to/engineering-quality-gate-procedure/" fallback="Engineering Quality Gate — Procedure" %}
- Prompt artifacts: {% include page-title-link.html url="/prompts/" fallback="Prompt blocks" %}
- Operating contracts: {% include page-title-link.html url="/policies/" fallback="Policies" %}
