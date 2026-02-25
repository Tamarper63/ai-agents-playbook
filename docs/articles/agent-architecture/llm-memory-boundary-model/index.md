---
title: "LLM Memory Boundary Model: Context Construction (Eligibility, Selection, Persistence) and Why Answers Change"
permalink: /articles/agent-architecture/llm-memory-boundary-model/
summary: A vendor-agnostic model of context construction—what can enter context (eligibility), what gets used per response (selection), and what is retained for later (persistence)—and the security controls that must live outside the prompt.
author: Tamar Peretz
published: 2026-02-22
---

This article is an **explanation** (conceptual model + design implications).  
Procedure/checklist: [Manage: LLM memory boundaries]({{ '/how-to/llm-memory-boundaries/' | relative_url }})

## Executive summary

In many production incidents, “memory problems” in LLM systems are not about storage. They are about **context construction**—how the system builds the model input for a given request:

- **Eligibility:** what information is allowed to influence a response.
- **Selection:** what subset is actually used for this specific response.
- **Persistence:** what (if anything) is retained to influence future responses.

When these steps are implicit, you tend to get: answer drift, non-reproducible behavior, and expanded security exposure (prompt injection + uncontrolled persistence/write-back).

**Evidence boundary:** vendor-specific statements in this page are limited to what OpenAI documents (see References). Everything else is a **vendor-agnostic system model** for engineering and auditing.

## Scope and terminology

### What “context construction” means (terminology used here)

**Context construction** is the process of constructing the input context for a single model invocation from multiple sources (user input, retrieved text, tool outputs, system/developer instructions, and optional memory/history features).  
(In this repo you may also see “request assembly” used as an equivalent term; this page uses “context construction” as the primary term.)

### What “memory” means operationally (terminology used here)

In production discussions, “memory” often conflates three different mechanisms:

1) **Persistent memory** (explicit saved items intended to carry across sessions)  
2) **History reference / recall** (signals pulled from prior chats; not guaranteed to be complete)  
3) **Current-request state** (the current prompt + active settings/instructions + tool/retrieval inputs)

This article keeps them separate because they fail differently and require different controls.

## What OpenAI documents about ChatGPT “Memory”

OpenAI documents two independent controls that shape what can be referenced between chats:
- **Reference saved memories** (persistent “saved memories”)
- **Reference chat history** (using information from past chats; not guaranteed to include every detail, and may change over time)

OpenAI also documents **Temporary Chat** as a mode that does not reference memories and does not create new memories.

(See References.)

## System model: context construction as a pipeline

This model separates **inputs** (candidate sources) from **controls** (policy + enforcement).  
Operationally: sources determine what *could* influence the response; controls determine what *may* influence it (and what can persist).

### 1) Candidate sources (what could influence the response)

Typical candidates include:
- **Saved memories** (if enabled)
- **History reference / recall** (if enabled)
- **Current user message** (the live prompt)
- **Tool outputs / retrieved documents** (RAG, connectors, browsing, logs, tickets)
- **System/developer instructions and product configuration** (implementation-dependent)

### 2) Controls (what must be enforced outside the prompt)

Controls that determine eligibility/selection/persistence commonly include:
- **Eligibility rules:** which sources are allowed for this request (and which are forbidden)
- **Scope rules:** project-only vs global vs tenant boundary
- **Selection policy:** prioritization and quotas (what gets included when context is constrained)
- **Persistence policy (write-back):** what may be retained, and under what conditions
- **Tool permissioning / approvals:** least-privilege for side effects
- **Output constraints:** schemas/structured outputs, filtering, redaction rules

**Engineering rule:** prompts express intent; enforcement must be implemented as control logic (policy decision + policy enforcement), not as advisory text.

## Why answers change (even with the same model)

Answer variance often comes from changes in context construction, for example:
- **Prompt wording changes** (different selection target and framing)
- **Memory/history toggles change** (different eligible sources)
- **Recall differs across time** (history reference is not guaranteed to include every detail)
- **Scope differs** (project-only vs global state; different boundary)
- **Retrieved/tool inputs differ** (different documents, different tool outputs)

If you cannot explain a behavior change via one of the above, treat it as an observability gap and instrument the controls (see Observability below).

## Security implication: context construction is a prompt-injection surface

OpenAI safety guidance describes **prompt injection** as untrusted text entering a system and attempting to override intended instructions.

Operationally: any retrieved document, ticket, webpage, email, or tool output that is fed into context is **untrusted input**. If you also allow persistence/write-back, you additionally create a path for **untrusted input to become durable state**.

OWASP guidance for agentic security highlights prompt injection defenses, tool security/least-privilege, and memory/context security as core concerns.

## Design anchor: decision vs enforcement (ZTA-aligned terminology)

NIST SP 800-207 (Zero Trust Architecture) describes **policy decision** and **policy enforcement** components (PDP/PEP) and uses a control-plane vs data-plane framing.

**Use here (by extension):**
- **Decision:** decide whether a candidate source/action is allowed for this request.
- **Enforcement:** guarantee that forbidden sources/actions cannot affect the request or cause side effects.

(See References.)

## Controls you can implement (vendor-agnostic)

### 1) Typed, scoped memory (avoid free-form blobs)
- Represent memory as explicit fields (preferences, constraints, project state), not arbitrary text.
- Attach scope (global/project/tenant) and retention (TTL or explicit removal).

### 2) Persistence/write-back as a privileged operation
- Gate write-back with policy (and optional human approval for sensitive categories).
- Attach provenance (source, time, workflow ID).

### 3) Treat retrieved text and tool outputs as untrusted inputs
- Validate/normalize inputs.
- Constrain ingestion with schemas/structured outputs when possible.

### 4) Observability for debugging and audit
- Log what sources were eligible, what was selected, and what was persisted (with identifiers).

## Key takeaways
- Model “memory issues” as **eligibility vs selection vs persistence**, not as a single blob.
- Put controls **outside the prompt**: decision + enforcement + observability.
- Treat all retrieved/tool text as **untrusted input**; prevent it from becoming durable state without policy.
- Make behavior explainable by logging **eligible sources**, **selected sources**, and **persistence events**.

## Suggested reading
- [Manage: LLM memory boundaries]({{ '/how-to/llm-memory-boundaries/' | relative_url }})
- [Request assembly threat model]({{ '/articles/agent-security/request-assembly-threat-model/' | relative_url }})
- [The Attack Surface Isn’t the LLM — It’s the Controller Loop]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})

## References

OpenAI:
- Memory FAQ (Reference saved memories / Reference chat history / Temporary Chat): https://help.openai.com/en/articles/8590148-memory-faq
- What is Memory?: https://help.openai.com/en/articles/8983136-what-is-memory
- How does “Reference saved memories” work?: https://help.openai.com/en/articles/11146739-how-does-reference-saved-memories-work
- Temporary Chat FAQ: https://help.openai.com/en/articles/8914046-temporary-chat-faq
- Memory and new controls for ChatGPT (OpenAI blog): https://openai.com/index/memory-and-new-controls-for-chatgpt/
- Safety in building agents (prompt injection guidance): https://developers.openai.com/api/docs/guides/agent-builder-safety/

OWASP:
- AI Agent Security Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html
- LLM Prompt Injection Prevention Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html

NIST:
- SP 800-207 Zero Trust Architecture (PDP/PEP; control plane/data plane), doi:10.6028/NIST.SP.800-207: https://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.SP.800-207.pdf