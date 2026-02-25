---
title: Manage LLM memory boundaries (ChatGPT + agentic systems) — procedure
description: Checklist and procedure for making LLM memory behavior predictable and auditable across ChatGPT and agentic systems.
permalink: /how-to/llm-memory-boundaries/
---

## Purpose
Use this page to make **cross-session influence** predictable and auditable by defining **what can be recalled**, **what must never persist**, and **where enforcement lives** (product memory vs application memory).

Use this procedure in AI workflows when:
- You see **session drift** (the assistant references prior chats/memories in ways you did not intend).
- You need a **“no persistence” workflow** (e.g., sensitive work, regulated data, client data).
- You are building an **agent with memory write-back** and must prevent **memory poisoning** and uncontrolled accumulation.
- You need auditability: “what influenced this answer?” across **saved memories**, **chat history**, and **current instructions**.

Related (explanation): [LLM memory boundary model — how context gets selected]({{ '/articles/agent-architecture/llm-memory-boundary-model/' | relative_url }})

**Reference model (ChatGPT terminology)**
ChatGPT describes memory as two separate mechanisms: **Saved memories** and **Chat history** (with separate controls).

## Canonical links
{% include catalog/howto-canonical-links.html %}

## Choose a mode
- **Option 1 (ChatGPT-only):** align product settings (Saved memories / Chat history) to your policy.
- **Option 2 (Agentic system):** implement application memory controls (validation, isolation, TTL, audits).
- **Option 3 (Both):** apply Option 1 for ChatGPT usage + Option 2 for your agent runtime.

## Setup
1) Write a one-paragraph **memory policy** (before prompts):
   - **Allowed to persist:** (e.g., role + stable preferences only)
   - **Must never persist:** secrets, credentials, one-time tokens, customer data, regulated data
   - **Enforcement location:** ChatGPT Memory toggles / app memory store / none

2) Decompose “memory” into 3 input sources (portable model):
   - **Saved memory** (explicit/persisted items)
   - **Chat history reference** (signals derived from past chats; not guaranteed complete)
   - **Current prompt + active configuration** (what you ask now + active instruction layer)

3) In ChatGPT: align settings with your policy:
   - Settings → Personalization → **Reference saved memories**
   - Settings → Personalization → **Reference chat history**
   - To avoid using or updating memory for a workflow, use **Temporary Chat**.
   - To remove memory, use **Manage memories** (and note: deleting a chat does not necessarily remove saved memory).

4) Pin scope in the first message of the workflow (context pinning):
   - Task scope (what to do / not do)
   - Minimum stable constraints (audience, allowed sources, formatting rules)
   - If applicable: “Do not store any customer data or secrets as memory.”

5) If building an agent: treat memory write-back as a security boundary:
   - Validate/sanitize before storing; **audit for sensitive data** before persistence.
   - Isolate memory by user/session/tenant; apply **expiration/TTL** and size limits.
   - Treat external content as **untrusted input**; reduce prompt injection risk paths into memory.

## Verify (smoke test)
1) “No persistence” test (ChatGPT):
- Start a Temporary Chat and ask a question that would normally benefit from remembered context.
- Expected: behavior does not rely on saved memory or chat history.

2) “Predictable recall” test (ChatGPT):
- Toggle **Reference saved memories** and **Reference chat history** on/off (one at a time), then repeat the same request.
- Expected: observable differences match your policy (saved memories vs chat history behavior).

3) “Safe write-back” test (agentic system):
- Attempt to store an injection-like payload or sensitive token in memory.
- Expected: validation/audit blocks or redacts, and memory remains scoped + expiring.

## Options

### Option 1 — ChatGPT-only (product memory controls)
**Checklist**
- [ ] Memory policy written (allowed / forbidden / enforcement location)
- [ ] Settings → Personalization configured:
  - [ ] Reference saved memories
  - [ ] Reference chat history
- [ ] Temporary Chat used for “no persistence” workflows
- [ ] Deletion verified via Manage memories (and relevant chats if required)

### Option 2 — Agentic system (application memory store)
**Checklist (minimum controls)**
- [ ] Validate/sanitize before persistence; audit for sensitive data
- [ ] Isolation per user/tenant/session
- [ ] TTL/expiration + size limits
- [ ] Treat retrieved/tool content as untrusted input; protect against prompt injection paths

### Option 3 — Both (recommended for mixed ChatGPT + agents)
Apply Option 1 for ChatGPT usage and Option 2 for agent runtime memory.

## Common mistakes
- Relying on “chat history” as complete ground truth (it is not guaranteed complete).
- Using memory for sensitive data or credentials (policy violation; increases leakage risk).
- Allowing untrusted external content to flow into memory without validation/sanitization (memory poisoning risk).
- Assuming deleting a chat deletes saved memory (you must manage saved memories explicitly).

## Related indexes
- [Policies]({{ '/policies/' | relative_url }})
- [How-to]({{ '/how-to/' | relative_url }})
- [Prompt templates]({{ '/prompts/' | relative_url }})
- [Start]({{ '/how-to/start-here-by-role/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})