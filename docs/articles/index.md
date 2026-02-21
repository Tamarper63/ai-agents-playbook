---
title: Articles
permalink: /articles/
page_class: page--articles-index
---

Long-form, engineering-oriented articles: threat models, agent/system architecture, evaluation methodology, and evidence/citation policies.

For procedures and lookup-style material:
- **How-to** (procedures/checklists): **[How-to]({{ '/how-to/' | relative_url }})**
- **Reference** (stable lookup, canonical diagrams): **[Reference]({{ '/reference/' | relative_url }})**
- **Policies** (normative operating contracts): **[Policies]({{ '/policies/' | relative_url }})**

## Terminology baseline {#terminology-baseline}

This index uses industry-standard terms where possible, and flags site-defined terms explicitly.

- **Orchestration / orchestrator / workflows / control-flow mechanisms**: intended to align with OWASP’s agentic security guidance (see *Securing Agentic Applications Guide 1.0*).
- **Control plane**: used in the networking sense (control plane vs forwarding/data plane).
- **Site-defined terms** used across multiple articles:
  - **Request assembly**: the end-to-end construction of an LLM request (instructions + user input + retrieved context + tool outputs), including ordering, truncation, and instrumentation.
  - **Verification gate**: an explicit guard (policy + checks) that must pass before an agent/workflow may proceed to the next step or tool action.
  - **Authority confusion** (site shorthand): a confused-deputy-style authority/identity propagation failure (see MITRE CWE-441).

Evidence boundary and claim policy:
- **[Choose an evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})**
- **[Policies]({{ '/policies/' | relative_url }})**

## Start here {#start-here}

A minimal reading path for first-time visitors (boundary modeling → orchestration risks → control-plane failures → request assembly → reliability):

1) **{% include page-title-link.html url="/articles/agent-security/llm-boundary-first-touch/" fallback="The Attack Surface Starts Before Agents — The LLM Boundary" %}**  
   Starts at the first LLM-to-system boundary: where model outputs can influence reads/writes to external systems (data stores, logs, telemetry, or persisted state).

2) **{% include page-title-link.html url="/articles/agent-security/controller-loop-attack-surface/" fallback="The Attack Surface Isn’t the LLM — It’s the Controller Loop" %}**  
   Focuses on how risk increases with *orchestration loops* (planning → tool invocation → evaluation → retries), not with the model in isolation.

3) **{% include page-title-link.html url="/articles/agent-security/control-plane-failures/" fallback="How Agentic Control-Plane Failures Actually Happen" %}**  
   Concrete failure patterns to audit: session binding, memory reuse, routing/selection, tool enforcement, and policy gates/monitoring.

4) **{% include page-title-link.html url="/articles/agent-security/request-assembly-threat-model/" fallback="Request assembly threat model: reading the diagram" %}**  
   Threat model for request assembly: selection/ordering/truncation, tool-loop integration, observability, and checkpoints.

5) **{% include page-title-link.html url="/articles/model-training-and-eval/fluency-vs-factuality/" fallback="Fluency Is Not Factuality" %}**  
   Reliability vocabulary: why fluent text is not evidence of correctness, and what grounding means operationally.

## Browse by topic {#browse-by-topic}

<div class="c-grid c-grid--2">
  <a class="c-card" href="{{ '/articles/agent-security/' | relative_url }}">
    <div class="c-card__content">
      <div class="c-card__title">Agent security</div>
      <div class="c-card__desc">Trust boundaries, authorization semantics, orchestration controls, policy enforcement, monitoring, and auditability</div>
    </div>
  </a>

  <a class="c-card" href="{{ '/articles/agent-architecture/' | relative_url }}">
    <div class="c-card__content">
      <div class="c-card__title">Agent architecture</div>
      <div class="c-card__desc">Workflow patterns, state/lifecycle management, tool invocation semantics, retrieval/context management, evaluation harnesses</div>
    </div>
  </a>

  <a class="c-card" href="{{ '/articles/model-training-and-eval/' | relative_url }}">
    <div class="c-card__content">
      <div class="c-card__title">Model training and evaluation</div>
      <div class="c-card__desc">Reliability, calibration, evaluation methods, and benchmark interpretation limits</div>
    </div>
  </a>

  <a class="c-card" href="{{ '/articles/prompt-engineering/' | relative_url }}">
    <div class="c-card__content">
      <div class="c-card__title">Prompt engineering</div>
      <div class="c-card__desc">Operational prompting notes, evidence contracts, and reusable templates</div>
    </div>
  </a>
</div>

## Featured (curated) {#featured}

Curated reads beyond the “Start here” path (maintain manually; keep short; avoid duplicating the Start here list):

- {% include page-title-link.html url="/articles/agent-security/trust-boundary-checkpoints/" fallback="Agentic Systems: 8 Trust-Boundary Audit Checkpoints" %}
- {% include page-title-link.html url="/articles/agent-security/provenance-boundary-report/" fallback="Provenance boundary failure report (client-captured artifacts)" %}
- {% include page-title-link.html url="/articles/agent-security/social-engineering-ai-decision-pipeline/" fallback="Social engineering in AI systems: attacking the decision pipeline (not just people)" %}
- {% include page-title-link.html url="/articles/agent-security/prompt-assembly-policy-enforcement/" fallback="Prompt Assembly Policy Enforcement: Typed Provenance to Prevent Authority Confusion" %}
- {% include page-title-link.html url="/articles/agent-architecture/llm-led-vs-orchestrator-led-tool-execution/" fallback="LLM-led vs orchestrator-led tool execution (architecture tradeoffs)" %}
- {% include page-title-link.html url="/articles/model-training-and-eval/theory-of-mind-in-llms/" fallback="Theory of mind in LLMs — what benchmarks test (and what they don’t)" %}
- {% include page-title-link.html url="/articles/prompt-engineering/prompt-engineering-daily-work/" fallback="Prompt Engineering Guide for Daily Work (Deep Dive)" %}

## All articles {#all-articles}

<details class="c-disclosure" markdown="block">  
<summary>
  <span class="c-disclosure__label c-disclosure__label--closed">Show full list (by topic)</span>
  <span class="c-disclosure__label c-disclosure__label--open">Hide full list (by topic)</span>
</summary>
<div class="c-disclosure__body" markdown="block">

### Agent security
- [The Attack Surface Starts Before Agents — The LLM Boundary]({{ '/articles/agent-security/llm-boundary-first-touch/' | relative_url }})
- [The Attack Surface Isn’t the LLM — It’s the Controller Loop]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})
- [How Agentic Control-Plane Failures Actually Happen]({{ '/articles/agent-security/control-plane-failures/' | relative_url }})
- [Request assembly threat model: reading the diagram]({{ '/articles/agent-security/request-assembly-threat-model/' | relative_url }})
- [Prompt Assembly Policy Enforcement: Typed Provenance to Prevent Authority Confusion]({{ '/articles/agent-security/prompt-assembly-policy-enforcement/' | relative_url }})
- [Agentic Systems: 8 Trust-Boundary Audit Checkpoints]({{ '/articles/agent-security/trust-boundary-checkpoints/' | relative_url }})
- [Provenance boundary failure report (client-captured artifacts)]({{ '/articles/agent-security/provenance-boundary-report/' | relative_url }})
- [Social engineering in AI systems: attacking the decision pipeline (not just people)]({{ '/articles/agent-security/social-engineering-ai-decision-pipeline/' | relative_url }})

### Agent architecture
- [LLM memory boundary model: how context gets selected]({{ '/articles/agent-architecture/llm-memory-boundary-model/' | relative_url }})
- [Human vs GenAI capability map (engineering view)]({{ '/articles/agent-architecture/human-vs-genai-capability-map/' | relative_url }})
- [LLM-led vs orchestrator-led tool execution (architecture tradeoffs)]({{ '/articles/agent-architecture/llm-led-vs-orchestrator-led-tool-execution/' | relative_url }})

### Model training and evaluation
- [Fluency Is Not Factuality]({{ '/articles/model-training-and-eval/fluency-vs-factuality/' | relative_url }})
- [Theory of mind in LLMs — what benchmarks test (and what they don’t)]({{ '/articles/model-training-and-eval/theory-of-mind-in-llms/' | relative_url }})
- [Orders of intentionality / recursive mindreading (LLMs)]({{ '/articles/model-training-and-eval/orders-of-intentionality-recursive-mindreading/' | relative_url }})

### Prompt engineering
- [Prompt Engineering Guide for Daily Work (Deep Dive)]({{ '/articles/prompt-engineering/prompt-engineering-daily-work/' | relative_url }})

</div>
</details>

## Related: evidence and policies {#related-evidence-and-policies}

- **[Choose an evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})**
- **[Policies]({{ '/policies/' | relative_url }})**

## References (terminology) {#references-terminology}

- OWASP GenAI Security Project — *Securing Agentic Applications Guide 1.0*: https://genai.owasp.org/resource/securing-agentic-applications-guide-1-0/
- IETF — RFC 7426 (*Software-Defined Networking (SDN): Layers and Architecture Terminology*): https://datatracker.ietf.org/doc/html/rfc7426
- MITRE — CWE-441 (*Unintended Proxy or Intermediary — Confused Deputy*): https://cwe.mitre.org/data/definitions/441.html