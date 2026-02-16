---
title: ChatGPT request assembly architecture
permalink: /reference/diagrams/chatgpt-request-assembly-architecture/
summary: Request assembly/context selection schematic with labeled risk injection points (R1–R8).
---

{% include diagrams/figure.html
  src="/assets/img/diagrams/chatgpt-request-assembly-architecture.png"
  alt="Request assembly architecture showing user input, policy enforcement, context selector, LLM inference, and supporting planes (tools, memory, retrieval, observability) with labeled risks R1–R8"
  caption="ChatGPT Request Assembly Architecture (schematic): request assembly/context selection with risk injection points R1–R8." %}

## Text alternative (long description)

- The diagram header reads: “ChatGPT Request Assembly Architecture.”
- Primary flow: User input → Gateway/Policy enforcement → Request assembly / context selector (pack + order + truncate) → LLM inference → Answer.
- Supporting planes depicted:
  - Execution/tools: tool router/function calling, chaining (multi-step loop / planner retries), connector/external tool.
  - Retrieval/caching: RAG/vector store; cache/replay store.
  - Memory: long-term memory (saved memory store), bio/profile attributes, user preferences, chat history, session history.
  - Streaming/observability: stream events (event bus), stream logs (telemetry sink).
- Risk labels as shown in the diagram: R1 (context injection), R4 (assembly manipulation), R6 (tool hijack), R7 (stream/log exfiltration), R3 (retrieval poisoning), R5 (replay/cache confusion), R2 (memory poisoning), R8 (profile/preference escalation).

NOT VERIFIED: This page documents only what is depicted in the schematic; it does not assert that any current production system matches this architecture or these labels.