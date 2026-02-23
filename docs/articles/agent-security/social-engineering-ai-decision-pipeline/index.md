---
title: "Social engineering in AI systems: attacking the decision pipeline (not just people)"
permalink: /articles/agent-security/social-engineering-ai-decision-pipeline/
author: Tamar Peretz
published: 2026-02-22
---

## Why this matters

In traditional security, **social engineering** targets humans. NIST defines social engineering as “an attempt to trick someone into revealing information … that can be used to attack systems or networks.” (NIST glossary)

Modern AI products add a new target: the **AI decision pipeline** (term used here): the end-to-end chain that converts inputs into *actions* (tool calls, workflow triggers, configuration changes, data movement).

OpenAI defines **prompt injection** as a type of **social engineering** against conversational AI: malicious instructions are injected into conversation context, including via third-party content the system ingests (e.g., web pages, documents, emails). (OpenAI)

OpenAI also defines prompt injection operationally for agents: it happens when **untrusted text or data enters an AI system** and attempts to override instructions; the end goals can include **exfiltrating private data via downstream tool calls** and **taking misaligned actions**. (OpenAI Agent Builder Safety)

**Core thesis:** This is an authority / enforcement problem, not a “better prompt” problem. If controls live only inside the model’s token stream, the attacker competes in the same channel.

## The pipeline is the “victim” (threat model shift)

A typical tool-using AI application is not just “user ↔ model”. It is a chain:

1) **Ingress**: user prompt + files + retrieved content (RAG)
2) **Model generation**: the model proposes steps/actions
3) **Execution**: an orchestrator/controller authorizes and runs tool calls
4) **Downstream**: services enforce their own authorization and invariants

Prompt injection becomes possible because *untrusted text/data* can enter the pipeline and attempt to override intended instructions. (OpenAI; OWASP LLM01:2025)

## Attack mechanics (taxonomy aligned to where untrusted text enters)

### 1) Direct prompt injection (user-controlled input)
OWASP defines **direct prompt injections** as cases where a user’s prompt input directly alters model behavior in unintended ways. (OWASP LLM01:2025)

**Common outcomes**
- Tool calls that were not requested
- Attempts to bypass policy (“ignore rules”, “act as admin”)
- Data exposure via tool responses or downstream actions

### 2) Indirect prompt injection (retrieved/ingested artifacts)
OWASP defines **indirect prompt injections** as cases where the LLM accepts input from external sources (e.g., websites or files) and that content alters behavior in unintended ways. (OWASP LLM01:2025)

This is a practical risk in systems that mix user intent with external content in a shared context window. Research literature describes real-world compromise paths for LLM-integrated apps via **indirect prompt injection**. (Greshake et al.)

**Illustrative example (generic)**
A support ticket includes “troubleshooting steps” that are actually instructions aimed at the assistant. If the pipeline treats that text as authoritative, it may trigger actions such as exporting data, changing access, inviting users, or modifying configuration.

### 3) Injection carried via tool outputs (site-defined extension)
OpenAI’s agent guidance defines prompt injection as “untrusted text or data enters an AI system.” Tool outputs can be one source of untrusted text/data entering later stages of a workflow; treat tool outputs as untrusted until validated. (OpenAI Agent Builder Safety)

## Why prompts are not an enforcement boundary

An enforcement boundary is where **deterministic allow/deny decisions** are applied *before side effects occur* (e.g., before a tool call changes state).

In Zero Trust Architecture, NIST models access through a **policy decision point (PDP)** and a corresponding **policy enforcement point (PEP)**. The PEP enforces decisions for protected interactions. (NIST SP 800-207)

OWASP explicitly warns against relying on system prompts as security controls and recommends enforcing critical security controls independently from the LLM. (OWASP LLM07:2025)

## Controls that should not live only in prompts

- **Authorization & policy enforcement outside the model**
  Enforce allow/deny decisions in a controller/orchestrator (PDP→PEP) and again in downstream systems. (NIST SP 800-207; OWASP LLM07:2025; OWASP LLM01:2025)

- **Define and validate expected output formats**
  Use structured outputs (schemas/enums) and deterministic validation between steps to reduce freeform channels. (OWASP LLM01:2025; OpenAI Agent Builder Safety)

- **Input/output filtering and separation of untrusted content**
  Separate and clearly denote untrusted external content; apply filtering to reduce injection influence. (OWASP LLM01:2025)

- **Output handling before downstream execution**
  OWASP defines **Improper Output Handling** as insufficient validation/sanitization of LLM outputs before passing them downstream; mitigate via validation/sanitization/encoding and zero-trust handling of model outputs. (OWASP LLM05:2025)

- **System prompt hygiene**
  Do not treat system prompts as secrets or security controls; avoid embedding sensitive data in system prompts; enforce controls outside the LLM. (OWASP LLM07:2025)

- **Budgets & loop breakers**
  Rate limiting, quotas, timeouts, throttling, and action limits reduce unbounded consumption and resource abuse. (OWASP LLM10:2025)

## A practical defense blueprint (architecture-first)

### Layer 1 — Boundary labeling: treat content as data, not authority
- Treat user prompts, retrieved documents, and tool outputs as **untrusted data**.
- Segregate and clearly denote external content to limit its influence. (OWASP LLM01:2025)

### Layer 2 — Tool access: least privilege by default
- Grant tools the minimum scopes required for the task.
- Prefer narrow, typed, auditable tool APIs over general command execution. (OWASP LLM01:2025)

### Layer 3 — Policy binding before action (controller/orchestrator)
- Evaluate proposed actions against policy (allow-lists, deny rules, role/attribute checks).
- Require step-up approval for high-impact operations (exports, role changes, irreversible modifications). (OWASP LLM01:2025; NIST SP 800-207)

### Layer 4 — Complete mediation at the downstream system
Do not rely on “the model’s intent”. Downstream services should authorize each request independently (“complete mediation”) and enforce invariants per request. (Saltzer & Schroeder, 1975; NIST SP 800-207)

### Layer 5 — Observability + adversarial verification
- Log proposed actions, approved actions, inputs used (including retrieved artifacts), and policy decisions.
- Run regression tests for:
  - direct injection in user prompts
  - indirect injection via retrieved/ingested content
  - injection carried via tool outputs (site-defined extension)

OWASP recommends adversarial testing and attack simulations for prompt injection resilience. (OWASP LLM01:2025)

## Where MCP fits (bounded claim)

**Model Context Protocol (MCP)** defines authorization capabilities at the transport level for HTTP-based transports, including scope-based authorization patterns (OAuth-based). Authorization is optional in MCP, and the spec defines how clients/servers negotiate and validate scopes/tokens. (MCP Authorization spec)

## Suggested next
- [Articles — Start here]({{ '/articles/#start-here' | relative_url }})
- [Agent security]({{ '/articles/agent-security/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})

## References

- NIST Glossary — “social engineering”: https://csrc.nist.gov/glossary/term/social_engineering
- OpenAI — “Understanding prompt injections: a frontier security challenge”: https://openai.com/index/prompt-injections/
- OpenAI — “Safety in building agents” (Agent Builder Safety): https://developers.openai.com/api/docs/guides/agent-builder-safety/
- OWASP LLM01:2025 — Prompt Injection: https://genai.owasp.org/llmrisk/llm01-prompt-injection/
- OWASP LLM05:2025 — Improper Output Handling: https://genai.owasp.org/llmrisk/llm052025-improper-output-handling/
- OWASP LLM07:2025 — System Prompt Leakage: https://genai.owasp.org/llmrisk/llm072025-system-prompt-leakage/
- OWASP LLM10:2025 — Unbounded Consumption: https://genai.owasp.org/llmrisk/llm102025-unbounded-consumption/
- NIST SP 800-207 — Zero Trust Architecture: https://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.SP.800-207.pdf
- Greshake et al. — “Not what you’ve signed up for: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection”: https://arxiv.org/abs/2302.12173
- MCP — Authorization specification (draft): https://modelcontextprotocol.io/specification/draft/basic/authorization
- Saltzer & Schroeder (1975) — “The Protection of Information in Computer Systems” (DOI: 10.1109/PROC.1975.9939): https://www.cl.cam.ac.uk/teaching/1011/R01/75-protection.pdf