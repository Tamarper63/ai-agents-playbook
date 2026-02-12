---
title: "LLM memory boundary model: how context gets selected (and why answers change)"
permalink: /articles/agent-architecture/llm-memory-boundary-model/
---

This article is an **explanation** (conceptual model + design implications).  
Procedure/checklist: [Manage: LLM memory boundaries]({{ '/how-to/llm-memory-boundaries/' | relative_url }})

## Why this exists

“Memory” issues are rarely random. Most failures come from **implicit context selection**:
- what was eligible to enter the context
- what was actually selected
- what gets persisted for future sessions

OpenAI’s ChatGPT documentation is useful here because it cleanly separates:
- **Saved memories** (persistent items)
- **Chat history reference** (signals from past conversations)
- **User prompt + configuration** (what you ask now + active settings)

See:
- https://help.openai.com/en/articles/8983136-what-is-memory  
- https://help.openai.com/en/articles/11146739-how-does-reference-saved-memories-work  
- https://help.openai.com/en/articles/8590148-memory-faq  
- https://openai.com/index/memory-and-new-controls-for-chatgpt/

## A concrete boundary model (derived from ChatGPT, portable as a design pattern)

Think in two planes:

### 1) Data plane (candidate inputs)
- Saved memory items (persistent)
- Past conversation content / derived signals (history reference)
- Current user message (prompt)
- Tool outputs / retrieved documents (if the system ingests them)

### 2) Control plane (selection + enforcement)
- Eligibility rules (what sources are allowed)
- Scoping rules (project-only vs global)
- Write-back rules (what can be persisted)
- Tool permissioning / approvals (if actions exist)

The critical point: **prompts are not enforcement**. They can express intent, but cannot guarantee what enters context or what persists.

## Why “answers change” even with the same model

Using the above decomposition, answer variance typically comes from one of these:
- Different **current prompt wording** changes the selection target.
- Different **saved memory/history signals** are eligible (or toggled on/off).
- Different **scope** (e.g., project-only vs global memory) changes available candidates.

ChatGPT documents that saved memories and chat history behave differently and are controlled separately.  
(See OpenAI “What is Memory?” + “Memory FAQ”.)

## Security implication: context selection is a social-engineering surface

OpenAI’s agent safety guidance defines prompt injection as **untrusted text entering the system** and trying to override intended instructions, with end goals including misaligned actions and data exfiltration via tools.  
- https://platform.openai.com/docs/guides/agent-builder-safety

If your system:
- ingests external content (docs/web/tickets), or
- accepts tool outputs as input, or
- allows memory write-back,

then “memory” becomes part of the **decision pipeline** and must be treated as a controlled boundary.

OWASP’s AI Agent Security guidance explicitly calls out prompt injection (direct/indirect), tool abuse, and least-privilege tool access as core concerns.  
- https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html

## Design principle: separate decision from enforcement (analogy to ZTA)

NIST SP 800-207 describes an abstract access model that separates a **policy decision point (PDP)** from a **policy enforcement point (PEP)**.  
- https://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.SP.800-207.pdf (DOI: 10.6028/NIST.SP.800-207)

A useful mapping (as an analogy, not a standard) is:
- “model proposes context/actions” ≈ decision candidate
- “controller enforces eligibility, scope, write-back, permissions” ≈ enforcement

## Practical implications (what “good” looks like)

### 1) Typed, scoped memory (not free-form)
- Memory is a set of explicit fields (role, preferences, constraints), not arbitrary text blobs.
- Each item has scope (global/project) and retention (TTL or explicit removal).

### 2) Controlled write-back (privileged operation)
- Memory write-back is gated by policy and/or human approval for sensitive categories.
- Provenance is attached (source, time, workflow id).

### 3) Treat tool outputs as untrusted data
- Tool responses can carry instruction-like text.
- Handle them as data; never as authority.

### 4) Observability
- Log: what sources were eligible, what was selected, what was persisted.

## Where this repo should place follow-ups

- Procedure/checklist (already): `/how-to/llm-memory-boundaries/`
- Optional future add-ons (if you want):
  - a “Memory threat model” article under `/articles/agent-security/`
  - regression test prompts for memory/write-back boundaries under `/kits/` or `/prompts/`

## References

OpenAI:
- What is Memory? https://help.openai.com/en/articles/8983136-what-is-memory  
- Reference saved memories: https://help.openai.com/en/articles/11146739-how-does-reference-saved-memories-work  
- Memory FAQ: https://help.openai.com/en/articles/8590148-memory-faq  
- Memory and new controls: https://openai.com/index/memory-and-new-controls-for-chatgpt/  
- Safety in building agents: https://platform.openai.com/docs/guides/agent-builder-safety  

OWASP:
- AI Agent Security Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html  

NIST:
- SP 800-207 Zero Trust Architecture (DOI: 10.6028/NIST.SP.800-207)  
  https://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.SP.800-207.pdf
