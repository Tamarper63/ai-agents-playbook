---
title: Agent architecture
permalink: /articles/agent-architecture/
show_title: false
---

This page is the index for agent-architecture articles.

It focuses on engineering concerns in multi-step, tool-using (agentic) systems:

- **Orchestration patterns (control-flow mechanisms)** — where control flow lives and how workflows are sequenced (model-led vs orchestrator-led; terms defined below).
- **State & lifecycle management** — what state persists across steps and boundaries (session/thread/run), what resets, and when.
- **Tool invocation lifecycle** — selection, authorization/enforcement, validation, error handling, retries, timeouts, and safe fallbacks.
- **Retrieval (RAG) & context construction** — what gets retrieved, selected, and included in the model input, and why.
- **Evaluation & test harnesses** — regression suites for multi-step workflows (robustness, failure-mode coverage, attack-oriented cases).

## Start here (pick the job)

| If you need… | Start with | Then |
|---|---|---|
| A concrete model for **what enters context** and why (selection + persistence) | {% include page-title-link.html url="/articles/agent-architecture/llm-memory-boundary-model/" fallback="LLM memory boundary model" %} | {% include page-title-link.html url="/how-to/llm-memory-boundaries/" fallback="Manage: LLM memory boundaries (procedure)" %} |
| A decision on **where orchestration and policy enforcement live** (model-led vs orchestrator-led) | {% include page-title-link.html url="/articles/agent-architecture/llm-led-vs-orchestrator-led-tool-execution/" fallback="Model-led vs orchestrator-led tool execution (tradeoffs)" %} | {% include page-title-link.html url="/articles/agent-security/controller-loop-attack-surface/" fallback="Controller-loop attack surface" %} |
| A framing for **what should be automated** vs kept human-owned (capability + failure modes) | {% include page-title-link.html url="/articles/agent-architecture/human-vs-genai-capability-map/" fallback="Human vs GenAI capability map" %} | {% include page-title-link.html url="/how-to/engineering-quality-gate-procedure/" fallback="Engineering Quality Gate — Procedure" %} |

## Key terms (as used in this section)

### Industry-standard baselines
- **Orchestration (control-flow mechanisms)** / **Workflows**: control-flow mechanisms that dictate an agent’s behavior and the structured sequences of steps it follows.  
  Reference: OWASP *Securing Agentic Applications Guide 1.0*.
- **Control plane / data plane (ZTA)**: in NIST SP 800-207, ZTA logical components communicate on a separate control plane, while application data is communicated on a data plane.  
  This section uses “control plane” as shorthand for the orchestration/policy communication and decision layer.
- **Retrieval-Augmented Generation (RAG)**: retrieval-backed generation where retrieved documents are used during generation.  
  Reference: Lewis et al., NeurIPS 2020.
- **Test harness**: a test environment (e.g., stubs/drivers/test doubles) needed to execute tests.  
  Reference: ISTQB glossary.

### Section-defined labels (used for comparison)
- **Orchestrator-led**: a controller sequences steps and enforces policy; the model is called for scoped sub-tasks.
- **Model-led**: the model proposes next actions/tool calls within constraints enforced by the orchestrator.

## Articles (curated)

- **{% include page-title-link.html url="/articles/agent-architecture/llm-memory-boundary-model/" fallback="LLM memory boundary model" %}**  
  Context construction/selection as a boundary: candidate inputs vs orchestration selection, persistence, and reset semantics.

- **{% include page-title-link.html url="/articles/agent-architecture/llm-led-vs-orchestrator-led-tool-execution/" fallback="Model-led vs orchestrator-led tool execution" %}**  
  Orchestration placement tradeoffs across reliability, observability, safety, latency, cost governance, and testability.

- **{% include page-title-link.html url="/articles/agent-architecture/human-vs-genai-capability-map/" fallback="Human vs GenAI capability map" %}**  
  Capability framing for task assignment, failure modes, and where automation breaks down.

## Related (for execution + contracts)

- Procedures: {% include page-title-link.html url="/how-to/" fallback="How-to" %} · {% include page-title-link.html url="/how-to/choose-facts-only-evidence-boundary/" fallback="Choose an evidence boundary" %} · {% include page-title-link.html url="/how-to/engineering-quality-gate-procedure/" fallback="Engineering Quality Gate — Procedure" %}
- Prompt artifacts: {% include page-title-link.html url="/prompts/" fallback="Prompt blocks" %}
- Operating contracts: {% include page-title-link.html url="/policies/" fallback="Policies" %}

## External baselines (terminology)

- OWASP — Securing Agentic Applications Guide 1.0: https://genai.owasp.org/resource/securing-agentic-applications-guide-1-0/
- NIST SP 800-207 — Zero Trust Architecture (control plane vs data plane): https://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.SP.800-207.pdf
- Lewis et al. (NeurIPS 2020) — Retrieval-Augmented Generation: https://proceedings.neurips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html
- ISTQB Glossary — Test harness: https://istqb-glossary.page/test-harness/