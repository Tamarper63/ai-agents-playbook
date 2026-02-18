---
title: Articles
permalink: /articles/
page_class: page--articles-index
---

Long-form technical writeups (engineering-oriented): **agent architecture**, **reliability/evaluation**, **security boundaries**, and **prompt specifications as contracts**.

## Start here {#start-here}

A minimal reading path for first-time visitors (architecture → context assembly → control-plane placement → reliability → security):

1) **{% include page-title-link.html url="/articles/agent-architecture/" fallback="Agent architecture (hub)" %}**  
   The core building blocks: control flow, state/lifecycle, tool semantics, retrieval/context management.

2) **{% include page-title-link.html url="/articles/agent-architecture/llm-memory-boundary-model/" fallback="LLM memory boundary model: how context gets selected" %}**  
   Context assembly as a boundary: candidate inputs vs. control-plane selection, persistence, and gating.

3) **{% include page-title-link.html url="/articles/agent-architecture/llm-led-vs-orchestrator-led-tool-execution/" fallback="LLM-led vs orchestrator-led tool execution (architecture tradeoffs)" %}**  
   Control-plane placement tradeoffs: reliability, observability, safety, latency, and testability.

4) **{% include page-title-link.html url="/articles/model-training-and-eval/fluency-vs-factuality/" fallback="Fluency Is Not Factuality" %}**  
   Reliability vocabulary: why fluent text is not evidence of correctness, and what “grounding” means operationally.

5) **{% include page-title-link.html url="/articles/agent-security/control-plane-failures/" fallback="How Agentic Control-Plane Failures Actually Happen" %}**  
   Concrete failure patterns to audit: session binding, memory reuse, routing, tool enforcement, gating/monitoring.

## Browse by topic {#browse-by-topic}

| Topic | What it covers | Hub |
|---|---|---|
| Agent architecture | Workflow patterns, state/lifecycle, tool invocation semantics, retrieval/context management, evaluation harnesses | **[Agent architecture]({{ '/articles/agent-architecture/' | relative_url }})** |
| Model training and evaluation | Reliability, calibration, evaluation methods, benchmark interpretation limits | **[Model training and evaluation]({{ '/articles/model-training-and-eval/' | relative_url }})** |
| Prompt engineering | Prompt specs as contracts, evidence contracts, operational templates | **[Prompt engineering]({{ '/articles/prompt-engineering/' | relative_url }})** |
| Agent security | Trust boundaries, authorization semantics, orchestration controls, monitoring/gating design | **[Agent security]({{ '/articles/agent-security/' | relative_url }})** |

## Featured (manual list) {#featured}

Curated reads beyond the “Start here” path (maintain manually; keep 4–6 items; avoid duplicating the Start here list):

- **{% include page-title-link.html url="/articles/prompt-engineering/prompt-engineering-daily-work/" fallback="Prompt Engineering Guide for Daily Work (Deep Dive)" %}**  
  Prompt specs as testable contracts + evaluation patterns; complements the procedural How-to version.

- **{% include page-title-link.html url="/articles/agent-security/trust-boundary-checkpoints/" fallback="Agentic Systems: 8 Trust-Boundary Audit Checkpoints" %}**  
  A concrete checklist for auditing end-to-end agent pipelines.

- **{% include page-title-link.html url="/articles/agent-security/social-engineering-ai-decision-pipeline/" fallback="Social engineering in AI systems: attacking the decision pipeline (not just people)" %}**  
  Threat modeling the decision pipeline: routing, selection, and tool-triggering seams.

- **{% include page-title-link.html url="/articles/agent-architecture/human-vs-genai-capability-map/" fallback="Human vs GenAI capability map (engineering view)" %}**  
  Capability framing for task assignment, failure modes, and where automation breaks down.

- **{% include page-title-link.html url="/articles/model-training-and-eval/theory-of-mind-in-llms/" fallback="Theory of mind in LLMs — what benchmarks test (and what they don’t)" %}**  
  Benchmark limits and interpretation guidance.

- **{% include page-title-link.html url="/articles/agent-security/provenance-boundary-report/" fallback="Provenance boundary failure report (client-captured artifacts)" %}**  
  A boundary-focused report format when server-side verification is not possible.

## Related: accuracy policies

Policies define the normative contract for evidence-locked claims and fail-closed behavior:
- **[Policies]({{ '/policies/' | relative_url }})**
