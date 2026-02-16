---
title: The Attack Surface Starts Before Agents — The LLM Boundary
permalink: /articles/agent-security/llm-boundary-first-touch/
summary: "Why agent-layer threat modeling is incomplete: the first high-leverage control point is the LLM boundary (before agents exist)."
---

## Scope and evidence boundary

This article is a threat-modeling guide for a specific *control point* **before** agent frameworks: the earliest interface where LLM I/O can touch production data or production observability.

It does **not** claim mechanism-level properties about LLMs. Where risk categories are referenced, they are pinned to **OWASP GenAI LLM Top 10 (2025)** (see References).

## Definition: “LLM boundary” (local label)

**LLM boundary (local label)** = the first interface where LLM inputs/outputs can **read from** or **write to**:
- production data stores, or
- production observability systems (logs / telemetry / traces), or
- tool/API surfaces that can cause side effects.

This is a *local* term used for this repo (not a standardized taxonomy item).

## Why this boundary matters even without “agents”

OWASP’s LLM Top 10 (2025) includes risks that apply to non-agent LLM apps when model I/O is connected to real systems:

- **LLM01:2025 Prompt Injection** — untrusted inputs steer behavior/output.
- **LLM02:2025 Sensitive Information Disclosure** — sensitive data leaks via outputs or context handling.
- **LLM05:2025 Improper Output Handling** — unsafe downstream consumption of model outputs.
- **LLM06:2025 Excessive Agency** — the system grants tools/permissions/autonomy beyond minimum needed.

## Threat scenarios at the LLM boundary (concrete, protocol-level)

### Scenario A — Indirect prompt injection via external content + tool access
If the system ingests untrusted content (email/docs/web) and also enables tool calls, an attacker can place instruction-like payloads in that content.
OWASP’s Excessive Agency guidance includes a mailbox-assistant scenario where a malicious email triggers the system to scan for sensitive data and exfiltrate it, with mitigations: minimize extensions, least-privilege scopes, and require human review for high-impact actions.

### Scenario B — Improper output handling in downstream systems
If model output is passed into:
- command execution,
- templating/HTML rendering,
- policy/routing decisions,
- database writes,
without strict validation/sanitization, the output becomes an injection surface (even if the user never sees it).

### Scenario C — Sensitive information disclosure via outputs and stored artifacts
If sensitive inputs/outputs are stored (logs/telemetry/analytics/memory/RAG indexes), the exposure surface includes retention, access control, and replay into future prompts.

## First-touch mapping worksheet (what to write down)

### 1) Read paths into the model (inputs)
Document every source that can enter context:

| Source | Trust level | Sensitivity | Transformations before model | Notes |
|---|---|---|---|---|
| User message | Untrusted | Varies | Redaction? | |
| Retrieved docs / web | Untrusted | Varies | Filtering / allowlist | |
| Tickets/CRM/email summaries | Semi-trusted | Often sensitive | Redaction + minimization | |
| Database reads | Trusted (system) | Often sensitive | Field-level selection | |
| Tool outputs (if re-injected) | Untrusted-by-default | Varies | Sanitization + provenance tags | |

### 2) Write paths from the model (outputs)
Document where outputs can land:

| Sink | Persisted? | Retention/TTL | Readers | Replay into prompts? | Controls |
|---|---:|---|---|---:|---|
| Product UI | No/Yes | — | End user | Maybe | Output policies |
| Logs / telemetry / traces | Yes | Defined TTL | Operators | Possible | Redaction + access controls |
| Analytics events | Yes | Defined TTL | Analysts | Possible | Minimization |
| Memory / context store | Yes | Defined TTL | System | Yes | Scoped + gated writes |
| Tools / internal APIs | Yes | — | Systems | — | Server-side authz + validation |
| Routing / feature flags | Yes | — | System | Yes | Deterministic gating |

### 3) Boundary owner and enforcement points
For each boundary crossing, record:
- **Owner** (who is accountable for the control),
- **What is enforced server-side** (not “prompted”),
- **What is audited** (minimum evidence for incident reconstruction).

## Minimum controls at the LLM boundary (vendor-agnostic)

### Control 1 — Data policy for model-visible content (enforced)
Define:
- what the model may see,
- what must be redacted/minimized,
- what can be stored, where, and for how long,
- what can be replayed into future prompts.

### Control 2 — Server-side authorization and validation for any side effects
If outputs can influence tools, writes, routing, or flags:
- enforce authorization + validation outside the prompt,
- minimize permissions and available functions,
- require human review for high-impact actions.

### Control 3 — Treat tool outputs and retrieved content as untrusted
- keep instruction hierarchy explicit (system/controller > tool data > user),
- strip/contain instruction-like text from untrusted sources,
- attach provenance (source, time, workflow) if re-injecting content into context.

### Control 4 — Auditability without over-collection
You should be able to reconstruct:
- what entered context (at least pointers + provenance),
- what output was produced,
- what actions were requested/performed/blocked,
- why.

## Copy/paste checklist
- [ ] I can point to the **first place** LLM I/O touches production data, observability, or tools.
- [ ] Every context source is classified (trust + sensitivity) and transformed before ingestion.
- [ ] Every output sink is documented (persistence, retention, readers, replay risk).
- [ ] Side-effect actions are gated server-side (authz + validation + least privilege).
- [ ] High-impact actions require explicit review/approval.
- [ ] Audit evidence exists to reconstruct an incident timeline.

## References (pinned)
OWASP (GenAI, 2025):
- LLM Top 10 index (2025): https://genai.owasp.org/llm-top-10/
- LLM06:2025 Excessive Agency: https://genai.owasp.org/llmrisk/llm062025-excessive-agency/

OWASP (legacy, v1.1 — for older pages only; note numbering differs):
- https://owasp.org/www-project-top-10-for-large-language-model-applications/

OWASP cheat sheets:
- AI Agent Security Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html

OpenAI:
- Agent/Builder safety guidance: https://platform.openai.com/docs/guides/agent-builder-safety

NIST:
- SP 800-207 Zero Trust Architecture: https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-207.pdf
- SP 800-92 Log Management: https://csrc.nist.gov/publications/detail/sp/800-92/final
- AI RMF 1.0 (AI 100-1): https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf
- GenAI Profile (AI 600-1): https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf