---
title: The Attack Surface Starts Before Agents — The LLM Boundary
permalink: /articles/agent-security/llm-boundary-first-touch/
summary: "Why “agent-layer threat modeling” is incomplete: the first real risk boundary is the LLM boundary (before agents exist)."
---

## Core claim
Many teams start “LLM security” discussions at the agent framework layer (tools, planners, multi-step loops).
This post argues for an earlier control point: the **LLM boundary**.

**In this post, “LLM boundary” means:**
> The first interface where LLM inputs/outputs can read from or write to *real production data* or *production observability systems* (logs, telemetry, traces), directly or indirectly.

Even a “simple chat” integration can become a boundary if its inputs/outputs are:
- logged verbatim,
- stored as application state,
- reused as future context (RAG / memory),
- or used as signals for routing, flags, or downstream automation.

## Why this boundary matters (even without agents)
OWASP’s LLM Top 10 is not limited to full agentic frameworks. Several categories apply to basic LLM applications:
- **Prompt Injection (LLM01)** — untrusted inputs influencing behavior.
- **Insecure Output Handling (LLM02)** — downstream systems consuming unsafe outputs.
- **Sensitive Information Disclosure (LLM06)** — sensitive data leaking via outputs.
- **Excessive Agency (LLM08)** — granting action authority without tight constraints.
(See references.)

## Concrete example: tool access through the LLM boundary

Figure 1 illustrates a concrete tool-access flow (Gmail) where untrusted content can influence routing decisions and increase exposure risk.

<figure>
  <img
    src="{{ '/assets/img/posts/llm-boundary-first-touch/gmail-tool-access.jpeg' | relative_url }}"
    alt="Diagram: prompt injection risks in Gmail tool access at the LLM boundary"
  />
  <figcaption><em>Figure 1 — Prompt injection risks in Gmail tool access at the LLM boundary (example).</em></figcaption>
</figure>

Key takeaways for boundary threat modeling:
- Treat tool routing as a control-plane decision: gate it server-side (authz + validation), not by prompt.
- Treat logs/telemetry as an external surface: minimize sensitive content and enforce retention/access controls.
- Make replay explicit: prevent uncontrolled reuse of tool outputs and message content as future context.

## The “first-touch” mapping exercise
To threat-model the LLM boundary, start with a concrete mapping:

### Step 1 — Identify every read path into the model
List all sources that can enter the prompt/context:
- user input
- retrieved documents / web content
- tickets/CRM/email summaries
- database reads
- “system” instructions and internal policies (what is visible to the model)

For each source, record:
- trust level (untrusted / semi-trusted / trusted)
- sensitivity class (public / internal / confidential / regulated)
- transformations (redaction, summarization, chunking, filtering)

### Step 2 — Identify every write path from the model
List every place model outputs can land:
- product UI output
- logs / telemetry / traces
- analytics events
- memory/context stores
- tool calls / internal APIs (if any)
- routing decisions / feature flags (if prompts/outputs are used as signals)

For each write path, record:
- whether it’s persisted
- retention/TTL
- who can read it (operators, engineers, downstream services)
- whether it can be replayed back into future prompts

### Step 3 — Mark the boundary owner and control points
For each boundary crossing, define:
- who owns the control (AppSec? platform? product? ML?)
- what *must* be enforced server-side (not “prompted”)
- what is audited (and how)

## Minimal controls at the LLM boundary (no agent framework required)

### 1) Explicit data policy for model-visible content
Define, in enforceable terms:
- what data the model may see,
- what must be redacted (PII, secrets, credentials),
- what can be stored, for how long, and where,
- what can be replayed into context later.

### 2) Clear limits on triggers (direct and indirect)
If model outputs can influence:
- external calls,
- writes,
- routing,
- flags,
treat those as control-plane effects and gate them with explicit authorization and validation.

### 3) Controlled interfaces to *every* external system touched (including “just logs”)
Logs are not neutral: they are storage + distribution.
At minimum:
- minimize sensitive content in logs,
- separate “debug” from “audit” trails,
- enforce access controls and retention limits.

### 4) Auditability (inputs, outputs, decisions)
You need to reconstruct:
- what the model saw,
- what it produced,
- what the system did with it,
- what was blocked/allowed,
- and why.

Without this, incident response becomes guesswork.

## A minimal checklist (copy/paste)
- [ ] I can point to the **first place** LLM I/O touches production data or observability.
- [ ] Every prompt/context source is classified by trust + sensitivity.
- [ ] Every output sink (UI/logs/storage/tools/routing) is documented with retention + readers.
- [ ] Sensitive data is redacted/minimized before logging and storage.
- [ ] Any side-effectful action is gated server-side (authz + validation).
- [ ] Audit trail is sufficient to replay an incident timeline.

## References (primary)

- [OWASP Top 10 for LLM Applications (v1.1)](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [OWASP AI Agent Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html)
- [NIST AI RMF 1.0 (NIST AI 100-1)](https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf)
- [NIST GenAI Profile (NIST AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf)

## Optional vendor-specific note (example)
- [OpenAI data controls & retention](https://platform.openai.com/docs/guides/your-data)

