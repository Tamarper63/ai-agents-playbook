---
title: "Request assembly / context selection — attack surface (summary)"
permalink: /reference/diagrams/request-assembly-context-selection-attack-surface/
summary: "Summary schematic of the request-assembly boundary highlighting common failure modes: instruction injection, precedence confusion, truncation, provenance loss, and memory poisoning."
---

{% include diagrams/figure.html
  src="/assets/img/diagrams/request-assembly-context-selection-attack-surface.png"
  width="1536"
  height="1024"
  alt="Summary diagram of a request-assembly boundary: user input flows into a context pool, a context selector, and a final assembled request before reaching the LLM core and tool routing; callouts highlight instruction injection, memory poisoning, truncation dropping constraints, provenance loss, and precedence confusion."
  caption="Request assembly / context selection as an attack surface — summary schematic." %}

## Overview
A generic reference model for the **request-assembly boundary** (context aggregation → selection/ranking → truncation) that precedes an LLM call.

## Text alternative (long description)
- Left-to-right flow: **User input** → **Context pool** → **Context selector** → **Final assembled request** → **LLM core** → **Tool router** → **Tools / external systems**.
- A dashed rectangle labeled **Request assembly boundary** encloses: Context pool, Context selector, Final assembled request.
- Risk callouts:
  - **Instruction injection (retrieval/tool output)** pointing into the context pool.
  - **Memory poisoning (persistence)** pointing into the context pool and the context selector.
  - **Precedence confusion (authority vs content)** pointing into the context pool.
  - **Truncation drops constraints** pointing into the final assembled request.
  - **Provenance loss (source unclear)** pointing near the handoff to the LLM core.

## Scope and limitations
- Vendor-agnostic reference model; not a claim about any specific product implementation.
- Risk labels are review targets (checklist), not assertions.

## Related reference diagrams
- [ChatGPT request assembly architecture]({{ "/reference/diagrams/chatgpt-request-assembly-architecture/" | relative_url }})
- [Provenance Boundary Failure — Prompt Assembly Diagram]({{ "/reference/diagrams/provenance-boundary-failure-prompt-assembly/" | relative_url }})