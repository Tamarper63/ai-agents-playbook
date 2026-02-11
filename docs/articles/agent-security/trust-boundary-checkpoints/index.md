---
title: Exploiting the Trust Boundary in Agentic Systems
permalink: /articles/agent-security/trust-boundary-checkpoints/
summary: A practical checklist of 8 trust checkpoints where untrusted artifacts can steer routing and actions in chained LLM systems.
---

## Overview
This post treats “prompt injection” and adjacent manipulation as a **trust-boundary** problem in chained agentic pipelines: retrieval → orchestration → routing → tool execution → write actions.

Important: the diagram is a schematic. The checklist below expands it into **8 checkpoints** you can audit in real systems.

## Schematic (diagram)
<figure>
  <img
    src="{{ '/assets/img/posts/trust-boundary-checkpoints/trust-boundary.jpeg' | relative_url }}"
    alt="Schematic: exploiting the trust boundary in an agentic pipeline from untrusted artifacts through gateway, context building, orchestration, tool routing, write gating, and audit logging"
  />
  <figcaption><em>Figure 1 — Schematic view of a trust-boundary attack surface in an agentic pipeline (not raw logs).</em></figcaption>
</figure>

## Why this is a trust-boundary issue (not a “prompt trick”)
In chained systems, untrusted content can enter through multiple paths (user prompts, tickets, docs, web pages, files). The risk grows when that content can influence:
- what is selected as context,
- how tasks are decomposed,
- which tools are chosen,
- and whether the system reaches write paths.

OWASP explicitly treats prompt injection as a top risk category for LLM applications, and agent guidance emphasizes least privilege and explicit authorization for sensitive operations.

## The 8 trust checkpoints (audit checklist)
1) **Ingress / Gateway**  
   Normalization, auth binding, policy enforcement on what enters the system.

2) **Request assembly / context selection**  
   What enters context, ordering/priority, and any “instruction vs data” labeling.

3) **Retrieval / ingestion**  
   Indirect injection via external artifacts (tickets/docs/pages/files).

4) **Orchestrator / planner**  
   Routing and task decomposition decisions (plan outputs treated as untrusted).

5) **LLM inference**  
   Instruction hierarchy failures and policy bypass attempts.

6) **Tool router + tools/connectors**  
   Scope misuse, unsafe tool selection, and argument manipulation.

7) **Action execution (write paths)**  
   Write operations in connected systems; high-impact actions must be gated.

8) **Output / egress**  
   Leakage, redaction failures, unsafe formatting, and unintended propagation.

## Concrete example (pattern)
A normal support ticket embeds instruction-like text disguised as troubleshooting steps.
If the pipeline treats it as authoritative, it can steer tool calls that export data, reset access, invite users, or change configuration.

## Baseline controls (agentic systems)
- Treat retrieved/ingested content as **untrusted data** (never as policy/instructions).
- Gate write/actions behind explicit authorization + server-side policy enforcement.
- Constrain tools by allowlisted actions/scopes (deny-by-default).
- Audit end-to-end: input → retrieved artifacts → tool I/O → downstream action (correlation IDs).

## References
- [OWASP Top 10 for Large Language Model Applications — LLM01 Prompt Injection][owasp-top10]
- [OWASP GenAI Security Project — LLM01 Prompt Injection][owasp-genai-llm01]
- [OWASP AI Agent Security Cheat Sheet][owasp-agent-cheatsheet]
- [NIST AI 600-1 — Generative AI Profile][nist-ai-600-1]

[owasp-top10]: https://owasp.org/www-project-top-10-for-large-language-model-applications/
[owasp-genai-llm01]: https://genai.owasp.org/llmrisk/llm01-prompt-injection/
[owasp-agent-cheatsheet]: https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html
[nist-ai-600-1]: https://doi.org/10.6028/NIST.AI.600-1
