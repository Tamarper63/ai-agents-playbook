---
title: "Social engineering in AI systems: attacking the decision pipeline (not just people)"
permalink: /articles/agent-security/social-engineering-ai-decision-pipeline/
---

## Why this matters

In traditional security, **social engineering** targets humans: an attacker tricks someone into revealing information that can be used to attack systems or networks (e.g., passwords). (NIST glossary)

Modern AI products add a new target: the **AI decision pipeline** that turns inputs into *actions* (tool calls, workflow triggers, configuration changes, data movement).

OpenAI frames **prompt injection** as a type of **social engineering** against conversational AI: attackers try to mislead an AI system by injecting malicious instructions into the conversation context—sometimes through third-party content the system ingests (e.g., web pages). (OpenAI)

**Core thesis:** This is an authority problem, not a “better prompt” problem. If enforcement lives only inside the model’s token stream, the attacker is competing in the same channel.

## The pipeline is the “victim” (threat model shift)

A typical tool-using AI application is not just “user ↔ model”. It is a chain:

1) **Ingress**: user prompt + files + retrieved content (RAG)  
2) **Reasoning**: model proposes steps/actions  
3) **Execution**: orchestrator/controller authorizes, shapes, and runs tool calls  
4) **Downstream**: services enforce their own authorization and invariants

Prompt injection becomes possible because *untrusted text/data* can enter the pipeline and attempt to override intended instructions. OpenAI notes the end goals vary, including **exfiltrating private data via downstream tool calls** and **taking misaligned actions**. (OpenAI Agent Builder Safety)

## Attack mechanics (taxonomy aligned to “where the untrusted text enters”)

### 1) Direct prompt injection (user-controlled input)
The attacker inserts instruction-like text directly into the user prompt to override intent.

**Common outcomes**
- Tool calls that were not requested
- Attempts to bypass policy (“ignore rules”, “act as admin”)
- Data exposure via tool responses or downstream actions

(See: OWASP Top 10 for LLM Applications v2025; OpenAI Agent Builder Safety)

### 2) Indirect prompt injection (retrieved/ingested artifacts)
The attacker plants instruction-like text in an artifact the system later ingests: webpages, documents, tickets, knowledge base pages.

This is a practical risk in systems that mix user intent with external content in a shared context window. Research literature describes real-world compromise paths for LLM-integrated apps via **indirect prompt injection**. (Greshake et al.)

**Illustrative example (generic)**
A support ticket includes “troubleshooting steps” that are actually instructions aimed at the assistant. If the pipeline treats that text as authoritative, it may trigger actions such as exporting data, changing access, inviting users, or modifying configuration.

### 3) Prompt injection carried via tool outputs (untrusted tool responses)
Even if user prompts are constrained, **tool outputs** can contain instruction-like text. If the system does not consistently treat tool responses as *untrusted data*, tool outputs can act as an injection carrier.

(Conceptually covered by OpenAI’s definition: “untrusted text or data enters an AI system”.)

## Why “prompts are not a control plane”

A **control plane** is where enforceable decisions are made—before side effects occur.

Prompts are not enforceable boundaries. They are interpreted inside the same channel that can include attacker-controlled text or attacker-controlled artifacts.

Controls that should not live *only* in prompts:

- **Authorization & policy enforcement outside the model**  
  Enforce allow/deny decisions in a controller/orchestrator, and again in downstream systems. (OpenAI Agent Builder Safety; OWASP LLM Top 10 v2025)

- **Output validation / sanitization before downstream use**  
  Treat model outputs as untrusted until validated against strict schemas/allow-lists. (OWASP LLM Top 10 v2025)

- **Instruction confidentiality & context hygiene**  
  Minimize exposure of privileged instructions; reduce leakage surfaces. (OWASP LLM Top 10 v2025)

- **Budgets & loop breakers**  
  Rate limits, tool limits, timeouts, token/cost budgets to reduce runaway execution and resource abuse. (OWASP LLM Top 10 v2025)

## A practical defense blueprint (architecture-first)

### Layer 1 — Boundary labeling: treat content as data, not authority
- Treat user prompts, retrieved documents, and tool outputs as **untrusted data**.
- Keep privileged policy outside the same content channel used for ingestion.

### Layer 2 — Tool access: least privilege by default
- Grant tools the minimum scopes required for the task.
- Prefer narrow, typed, auditable tool APIs over “general command execution”.

### Layer 3 — Policy binding before action (controller/orchestrator)
- Evaluate proposed actions against policy (RBAC/ABAC, allow-lists, deny rules).
- Require explicit step-up approval for high-impact operations (exports, role changes, irreversible modifications).

### Layer 4 — Complete mediation at the downstream system
Do not rely on “the model’s intent”. Downstream services should authorize each request independently (“complete mediation”) and enforce invariants per request. (NIST secure design principles; NIST ZTA)

### Layer 5 — Observability + adversarial verification
- Log proposed actions, approved actions, inputs used (including retrieved artifacts), and policy decisions.
- Run regression tests for:
  - direct injection in user prompts
  - indirect injection via retrieved/ingested content
  - injection carried via tool outputs

OpenAI describes prompt injection as a major and persistent risk for agents, including scenarios where external content steers tool-using workflows. (OpenAI)

## Where MCP fits (bounded claim)

**Model Context Protocol (MCP)** standardizes how AI applications connect to external tools and data sources, including authorization-related mechanisms at the protocol/transport layer. It does not define your product’s authorization policy (what should be allowed). Policy ownership remains in your application/controller and your downstream systems. (MCP spec; OpenAI Agent Builder Safety)

## References

- NIST Glossary — “social engineering”: https://csrc.nist.gov/glossary/term/social_engineering
- OpenAI — “Understanding prompt injections: a frontier security challenge”: https://openai.com/index/prompt-injections/
- OpenAI — “Safety in building agents” (Agent Builder Safety): https://developers.openai.com/api/docs/guides/agent-builder-safety/
- OWASP — Top 10 for LLM Applications v2025 (PDF): https://owasp.org/www-project-top-10-for-large-language-model-applications/assets/PDF/OWASP-Top-10-for-LLMs-v2025.pdf
- NIST SP 800-207 — Zero Trust Architecture: https://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.SP.800-207.pdf
- Greshake et al. — “Not what you’ve signed up for: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection” (arXiv): https://arxiv.org/abs/2302.12173
- MCP — Specification / Authorization: https://modelcontextprotocol.io/
