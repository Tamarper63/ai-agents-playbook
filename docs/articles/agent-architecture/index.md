---
title: Agent architecture
permalink: /articles/agent-architecture/
show_title: false
---

This page is the **hub** for agent-architecture articles in this repository.

It focuses on engineering concerns in multi-step agent systems:
- **Control flow patterns** (orchestrator-led vs model-led)
- **State and lifecycle management** (what persists, what resets, and when)
- **Tool invocation semantics** (selection, authorization, validation, error handling)
- **Retrieval and context management** (what enters context, and why)
- **Evaluation harnesses** for multi-step workflows (tests, regressions, robustness)

## Key terms (as used in this section)

- **Orchestrator-led**: a controller sequences steps and enforces policy; the model is called for scoped sub-tasks.
- **Model-led**: the model proposes next actions/tool calls within constraints enforced by the orchestrator.

## Articles

- **[LLM memory boundary model: how context gets selected]({{ '/articles/agent-architecture/llm-memory-boundary-model/' | relative_url }})**  
  Context assembly as a boundary: candidate inputs vs. control-plane selection and persistence.

- **[Human vs GenAI capability map (engineering view)]({{ '/articles/agent-architecture/human-vs-genai-capability-map/' | relative_url }})**  
  Capability framing for task assignment, failure modes, and where automation breaks down.

- **[LLM-led vs orchestrator-led tool execution (architecture tradeoffs)]({{ '/articles/agent-architecture/llm-led-vs-orchestrator-led-tool-execution/' | relative_url }})**  
  Architecture tradeoffs: control, safety, reliability, and testability across execution styles.