---
title: "LLM memory boundary model: how context gets selected (and why answers change)"
permalink: /articles/agent-architecture/llm-memory-boundary-model/
summary: A boundary model for context assembly (memory + chat history + prompt + tool inputs) and the control-plane controls that govern eligibility, persistence, and security.
author: Tamar Peretz
published: 2026-02-22
---

This article is an **explanation** (conceptual model + design implications).
Procedure/checklist: [Manage: LLM memory boundaries]({{ '/how-to/llm-memory-boundaries/' | relative_url }})

## Scope and evidence boundary

- Product-specific statements about **ChatGPT Memory** are grounded in OpenAI documentation (see References).
- The “boundary model” sections are an **engineering decomposition** for troubleshooting and design. Where this text uses analogies (e.g., ZTA), it is labeled as such.

## Why this exists

“Memory” is an overloaded term. In practice, failures that look like “memory bugs” often reduce to:
1) what information was **eligible** to enter context,
2) what was **selected** for this response, and
3) what (if anything) was **persisted** for later.

This page provides a boundary model for that pipeline.

## What OpenAI documents about ChatGPT “Memory”

OpenAI documents two independent controls that shape what can be referenced between chats:
- **Reference saved memories** (persistent “saved memories”)
- **Reference chat history** (using information from past chats; not guaranteed to include every detail, and may change over time)

OpenAI also documents **Temporary Chat** as a mode that does not reference memories and does not create new memories.

(See References.)

## A boundary model for context assembly (portable design pattern)

This decomposition uses two planes:

### 1) Data plane (candidate inputs)
- **Saved memories** (if enabled)
- **Information recalled from chat history** (if enabled)
- **Current user message** (the live prompt)
- **Tool outputs / retrieved documents** (when the system ingests external content)
- **System/developer instructions and product configuration** (implementation-dependent)

### 2) Control plane (selection + enforcement)
- Eligibility rules (what sources are allowed)
- Scoping rules (project-only vs global vs per-tenant)
- Write-back rules (what may be persisted and under what conditions)
- Tool permissioning / approvals (if actions exist)
- Output constraints (schemas, structured outputs, filtering)

**Design note:** Prompts express intent; enforcement requires control-plane mechanisms.

## Why “answers change” (even with the same model)

Answer variance can result from changes in one or more of:
- **Prompt wording** (changes the selection target)
- **Memory settings** (saved memories / chat history toggles)
- **What is recalled from chat history** (not all details are retained; what’s recalled can change)
- **Scope** (project-only vs global memory/state)
- **External content ingestion** (different retrieved docs/tool outputs)

## Security implication: context assembly is a prompt-injection surface

OpenAI safety guidance describes **prompt injection** as untrusted text entering a system and attempting to override intended instructions.

If your system ingests external content (docs/web/tickets), accepts tool outputs as input, or allows memory write-back, treat all such text as **untrusted data** and enforce boundaries in the control plane.

OWASP guidance for AI agent security highlights prompt injection defenses, tool security/least-privilege, and memory/context security as core concerns.

## Design principle: separate decision from enforcement (analogy to ZTA)

NIST SP 800-207 (Zero Trust Architecture) distinguishes a **policy decision point (PDP)** and a **policy enforcement point (PEP)**, and uses a **control plane vs data plane** framing.

**Analogy (not a standard mapping):**
- “Model proposes an answer / candidates” ≈ decision candidate
- “Controller/orchestrator enforces eligibility, scope, write-back, permissions” ≈ enforcement

## Practical controls (mapped to common guidance)

### 1) Typed, scoped memory (avoid free-form blobs)
- Represent memory as explicit fields (preferences, constraints, project state), not arbitrary text.
- Attach scope (global/project/tenant) and retention (TTL or explicit removal).

### 2) Controlled write-back (privileged operation)
- Gate write-back with policy (and optional human approval for sensitive categories).
- Attach provenance (source, time, workflow ID).

### 3) Treat tool outputs and retrieved text as untrusted inputs
- Validate/normalize inputs.
- Constrain data flow with schemas/structured outputs when possible.

### 4) Observability
- Log what sources were eligible, what was selected, and what was persisted (with identifiers).

## Where this repo should place follow-ups (recommendations)

- Procedure/checklist: `/how-to/llm-memory-boundaries/`
- If you want deeper security coverage:
  - “Memory threat model” under `/articles/agent-security/`
  - Regression prompts for memory/write-back boundaries under `/prompts/` or `/kits/`

## References

OpenAI:
- Memory FAQ (Reference saved memories / Reference chat history / Temporary Chat): https://help.openai.com/en/articles/8590148-memory-faq
- What is Memory?: https://help.openai.com/en/articles/8983136-what-is-memory
- Reference saved memories: https://help.openai.com/en/articles/11146739-how-does-reference-saved-memories-work
- Safety in building agents (prompt injection guidance): https://developers.openai.com/api/docs/guides/agent-builder-safety/

OWASP:
- AI Agent Security Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html

NIST:
- SP 800-207 Zero Trust Architecture (PDP/PEP; control plane/data plane): https://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.SP.800-207.pdf