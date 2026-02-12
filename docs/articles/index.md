---
title: Articles
permalink: /articles/
---

Long-form technical writeups (engineering-oriented): threat models, architecture notes, evaluation methodology, and evidence/verification contracts.

If you are looking for step-by-step procedures and templates, go to **[How-to]({{ '/how-to/' | relative_url }})**.  
If you need normative constraints for evidence/accuracy claims, go to **[Policies]({{ '/policies/' | relative_url }})**.

<nav class="page-toc" aria-label="On this page">
  <p class="page-toc__title">On this page</p>
  <ul class="page-toc__list">
    <li><a href="#start-here">Start here</a></li>
    <li><a href="#browse-by-topic">Browse by topic</a></li>
    <li><a href="#featured-updates">Featured updates (manual list)</a></li>
    <li><a href="#all-articles">All articles</a></li>
    <li><a href="#related-accuracy-policies">Related: accuracy policies</a></li>
  </ul>
</nav>

## Start here

A minimal reading path for first-time visitors (foundational concepts → control-plane risks → reliability):

1) **[The Attack Surface Starts Before Agents — The LLM Boundary]({{ '/articles/agent-security/llm-boundary-first-touch/' | relative_url }})**  
   Where “LLM security” begins: the first read/write boundary to production data, logs, telemetry, or persisted state.

2) **[The Attack Surface Isn’t the LLM — It’s the Controller Loop]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})**  
   Why risk scales with orchestration loops (planning → tools → evaluation → retries), not with the model in isolation.

3) **[How Agentic Control-Plane Failures Actually Happen]({{ '/articles/agent-security/control-plane-failures/' | relative_url }})**  
   Concrete control-plane failure patterns to audit: session binding, memory reuse, routing, tool enforcement, and gating monitors.

4) **[Fluency Is Not Factuality]({{ '/articles/model-training-and-eval/fluency-vs-factuality/' | relative_url }})**  
   Reliability vocabulary: why fluent text is not evidence of correctness, and what “grounding” means operationally.

5) **[Prompt Engineering Guide for Daily Work (Deep Dive)]({{ '/articles/prompt-engineering/prompt-engineering-daily-work/' | relative_url }})**  
   Prompt specs as testable contracts + evaluation patterns; complements the procedural How-to version.

## Browse by topic

| Topic | What it covers | Hub |
|---|---|---|
| Agent security | Policy boundaries, authorization semantics, orchestration controls, monitoring/gating design | **[Agent security]({{ '/articles/agent-security/' | relative_url }})** |
| Agent architecture | Workflow patterns, state/lifecycle management, tool invocation semantics, retrieval/context management, evaluation harnesses | **[Agent architecture]({{ '/articles/agent-architecture/' | relative_url }})** |
| Model training and evaluation | Reliability, calibration, evaluation methods, benchmark interpretation limits | **[Model training and evaluation]({{ '/articles/model-training-and-eval/' | relative_url }})** |
| Prompt engineering | Practical prompting notes, evidence contracts, operational templates | **[Prompt engineering]({{ '/articles/prompt-engineering/' | relative_url }})** |

## Featured updates (manual list)

<!-- Maintain manually. Keep 3–7 items. Order: newest/most-relevant first. -->

- [Provenance boundary failure report (client-captured artifacts)]({{ '/articles/agent-security/provenance-boundary-report/' | relative_url }})
- [The Attack Surface Isn’t the LLM — It’s the Controller Loop]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})
- [Prompt Engineering Guide for Daily Work (Deep Dive)]({{ '/articles/prompt-engineering/prompt-engineering-daily-work/' | relative_url }})
- [The Attack Surface Starts Before Agents — The LLM Boundary]({{ '/articles/agent-security/llm-boundary-first-touch/' | relative_url }})
- [How Agentic Control-Plane Failures Actually Happen]({{ '/articles/agent-security/control-plane-failures/' | relative_url }})

## All articles

### Agent security
- [The Attack Surface Starts Before Agents — The LLM Boundary]({{ '/articles/agent-security/llm-boundary-first-touch/' | relative_url }})
- [The Attack Surface Isn’t the LLM — It’s the Controller Loop]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})
- [How Agentic Control-Plane Failures Actually Happen]({{ '/articles/agent-security/control-plane-failures/' | relative_url }})
- [Exploiting the Trust Boundary in Agentic Systems]({{ '/articles/agent-security/trust-boundary-checkpoints/' | relative_url }})
- [Provenance boundary failure report (client-captured artifacts)]({{ '/articles/agent-security/provenance-boundary-report/' | relative_url }})
- [Social engineering in AI systems: attacking the decision pipeline (not just people)]({{ '/articles/agent-security/social-engineering-ai-decision-pipeline/' | relative_url }})

### Agent architecture
- [LLM memory boundary model: how context gets selected]({{ '/articles/agent-architecture/llm-memory-boundary-model/' | relative_url }})
- [Human vs GenAI capability map (engineering view)]({{ '/articles/agent-architecture/human-vs-genai-capability-map/' | relative_url }})
- [LLM-led vs orchestrator-led tool execution (architecture tradeoffs)]({{ '/articles/agent-architecture/llm-led-vs-orchestrator-led-tool-execution/' | relative_url }})

### Model training and evaluation
- [Fluency Is Not Factuality - Why LLMs Can Sound Right and Be Wrong]({{ '/articles/model-training-and-eval/fluency-vs-factuality/' | relative_url }})
- [Theory of mind in LLMs — what benchmarks test (and what they don’t)]({{ '/articles/model-training-and-eval/theory-of-mind-in-llms/' | relative_url }})
- [Orders of intentionality / recursive mindreading (LLMs)]({{ '/articles/model-training-and-eval/orders-of-intentionality-recursive-mindreading/' | relative_url }})

### Prompt engineering
- [Prompt Engineering Guide for Daily Work (Deep Dive)]({{ '/articles/prompt-engineering/prompt-engineering-daily-work/' | relative_url }})

## Related: accuracy policies

Policies define the normative contract for evidence-locked claims and fail-closed behavior:
- **[Policies]({{ '/policies/' | relative_url }})**
