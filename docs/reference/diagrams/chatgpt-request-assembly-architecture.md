---
title: ChatGPT request assembly architecture
permalink: /reference/diagrams/chatgpt-request-assembly-architecture/
summary: Request assembly/context selection schematic with annotated risk points across tools, memory, retrieval/caching, and observability.
---

{% include diagrams/figure.html
  src="/assets/img/diagrams/chatgpt-request-assembly-architecture.png"
  src_2x="/assets/img/diagrams/chatgpt-request-assembly-architecture@2x.png"
  width="1600"
  height="890"
  alt="..."
  caption="..." %}

## Text alternative (long description)

- The diagram header reads: “ChatGPT Request Assembly Architecture.”
- Primary flow: User input → Gateway/Policy enforcement → Request assembly / context selector (pack + order + truncate) → LLM inference → Answer.
- Supporting planes depicted:
  - Execution/tools: tool router/function calling, chaining (multi-step loop / planner retries), connector/external tool.
  - Retrieval/caching: RAG/vector store; cache/replay store.
  - Memory: long-term memory (saved memory store), bio/profile attributes, user preferences, chat history, session history.
  - Streaming/observability: stream events (event bus), stream logs (telemetry sink).
- Risk callouts shown in the diagram: context injection; request assembly manipulation (ordering/truncation bias); tool hijack (tool selection + argument injection); stream/log exfiltration (prompts/outputs/user data); retrieval poisoning (RAG corpus/embeddings); replay/cache confusion (stale/wrong session state); memory poisoning (long-term memory write); profile/preference escalation (bio/prefs become control-plane).

NOT VERIFIED: This page documents only what is depicted in the schematic; it does not assert that any current production system matches this architecture or these annotations.