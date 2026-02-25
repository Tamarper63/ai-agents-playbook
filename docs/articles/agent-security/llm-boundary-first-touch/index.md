---
title: "The attack surface starts before agents: the LLM integration trust boundary"
permalink: /articles/agent-security/llm-boundary-first-touch/
summary: "Why agent-layer threat modeling is incomplete: the first high-leverage control point is the LLM integration trust boundary (before agent frameworks exist)."
author: Tamar Peretz
published: 2026-02-22
---

> **What this page is:** a vendor-agnostic threat-modeling worksheet for the earliest trust boundary where LLM I/O can touch production systems.  
> **What this page is not:** a claim about LLM internals or any specific vendor trace.

## Executive summary

Before you adopt an agent framework, many high-leverage security controls are decided at the **LLM integration trust boundary**: the first interface where model inputs/outputs can (a) read production data, (b) write to production systems, or (c) enter production observability (logs/telemetry/traces).

This page treats that interface as a **trust boundary** and maps it to OWASP GenAI LLM Top 10 (2025) risk categories.

## How to use this worksheet

1) Fill the **read paths** table with every source that can enter context (including retrieval and tool outputs).  
2) Fill the **write paths** table with every sink where model outputs can land (including observability and persistence).  
3) For each boundary crossing, record the **owner**, the **server-side enforcement point**, and the **minimum audit evidence** required to reconstruct an incident.

## Scope and evidence boundary

This article is a threat-modeling guide for a specific control point **before** agent frameworks: the earliest interface where LLM I/O can touch production data or production observability.

It does **not** claim mechanism-level properties about LLMs. Where risk categories are referenced, they are pinned to **OWASP GenAI LLM Top 10 (2025)** (see References).

## Definition: the LLM integration trust boundary

**LLM integration trust boundary** = the first interface where LLM inputs/outputs can **read from** or **write to**:
- production data stores, or
- production observability systems (logs / telemetry / traces), or
- tool/API surfaces that can cause side effects.

Operationally, this is the trust boundary between model I/O and production systems.

## Why this boundary matters (even without agents)

OWASP’s LLM Top 10 (2025) includes risks that apply to non-agent LLM apps when model I/O is connected to real systems:

- **LLM01:2025 Prompt Injection** — untrusted inputs steer behavior/output.
- **LLM02:2025 Sensitive Information Disclosure** — sensitive data leaks via outputs or context handling.
- **LLM05:2025 Improper Output Handling** — unsafe downstream consumption of model outputs.
- **LLM06:2025 Excessive Agency** — the system grants tools/permissions/autonomy beyond minimum needed.

## Threat scenarios at the trust boundary (protocol-level)

### Scenario A — indirect prompt injection via external content + tool access
If the system ingests untrusted content (email/docs/web) and also enables tool calls, an attacker can place instruction-like payloads in that content.

OWASP’s Excessive Agency guidance includes mailbox-assistant scenarios where untrusted inputs can trigger sensitive-data access and exfiltration. Mitigations include minimizing extensions, least-privilege scopes, and requiring user approval for high-impact actions.

### Scenario B — improper output handling downstream
If model output is passed into:
- command execution,
- templating/HTML rendering,
- policy/routing decisions,
- database writes,
without strict validation/sanitization, the output becomes an injection surface (even if the user never sees it).

### Scenario C — sensitive data exposure via stored artifacts
If sensitive inputs/outputs are stored (logs/telemetry/analytics/memory/RAG indexes), the exposure surface includes retention, access control, and replay into future prompts.

## Mapping worksheet

### 1) Read paths into the model (inputs)
Document every source that can enter context:

<div class="c-table" role="region" aria-label="Read paths into the model (inputs)" tabindex="0"><table><thead><tr><th>Source</th><th>Trust level</th><th>Sensitivity</th><th>Transformations before model</th><th>Notes</th></tr></thead><tbody>
<tr><td>User message</td><td>Untrusted</td><td>Varies</td><td>Redaction?</td><td></td></tr>
<tr><td>Retrieved docs / web</td><td>Untrusted</td><td>Varies</td><td>Filtering / allowlist</td><td></td></tr>
<tr><td>Tickets/CRM/email summaries</td><td>Untrusted (default)</td><td>Often sensitive</td><td>Redaction + minimization</td><td></td></tr>
<tr><td>Database reads</td><td>Trusted (system)</td><td>Often sensitive</td><td>Field-level selection</td><td></td></tr>
<tr><td>Tool outputs (if re-injected)</td><td>Untrusted (default)</td><td>Varies</td><td>Sanitization + provenance tags</td><td></td></tr>
</tbody></table></div>

### 2) Write paths from the model (outputs)
Document where outputs can land:

<div class="c-table" role="region" aria-label="Write paths from the model (outputs)" tabindex="0"><table><thead><tr><th>Sink</th><th>Persisted?</th><th>Retention/TTL</th><th>Readers</th><th>Replay into prompts?</th><th>Controls</th></tr></thead><tbody>
<tr><td>Product UI</td><td>No/Yes</td><td>—</td><td>End user</td><td>Maybe</td><td>Output policies</td></tr>
<tr><td>Logs / telemetry / traces</td><td>Yes</td><td>Defined TTL</td><td>Operators</td><td>Possible</td><td>Redaction + access controls</td></tr>
<tr><td>Analytics events</td><td>Yes</td><td>Defined TTL</td><td>Analysts</td><td>Possible</td><td>Minimization</td></tr>
<tr><td>Memory / context store</td><td>Yes</td><td>Defined TTL</td><td>System</td><td>Yes</td><td>Scoped + gated writes</td></tr>
<tr><td>Tools / internal APIs</td><td>Yes</td><td>—</td><td>Systems</td><td>—</td><td>Server-side authz + validation</td></tr>
<tr><td>Routing / feature flags</td><td>Yes</td><td>—</td><td>System</td><td>Yes</td><td>Deterministic gating</td></tr>
</tbody></table></div>

### 3) Owner, enforcement, and audit evidence
For each boundary crossing, record:
- **Owner** (accountable control owner),
- **Server-side enforcement** (not “prompted”),
- **Audit evidence** (minimum data required to reconstruct an incident).

## Minimum controls at the trust boundary (vendor-agnostic)

### Control 1 — data policy for model-visible content (enforced)
Define:
- what the model may see,
- what must be redacted/minimized,
- what can be stored, where, and for how long,
- what can be replayed into future prompts.

### Control 2 — server-side authorization and validation for any side effects
If outputs can influence tools, writes, routing, or flags:
- enforce authorization + validation outside the prompt,
- minimize permissions and available functions,
- require user review/approval for high-impact actions.

### Control 3 — treat retrieved content and tool outputs as untrusted data
- maintain a strict instruction hierarchy (policy/controller > tool data > user data),
- constrain untrusted content so it cannot act as policy or permissions,
- attach provenance (source, time, workflow) when re-injecting content into context.

### Control 4 — auditability without over-collection
You should be able to reconstruct:
- what entered context (at least pointers + provenance),
- what output was produced,
- what actions were requested/performed/blocked,
- why.

## What you should have when done

- A complete inventory of **context inputs** (sources + trust level + transformations).
- A complete inventory of **output sinks** (persistence + retention + readers + replay risk).
- A list of **server-side enforcement points** for side effects (authz + validation + least privilege).
- A minimum **audit evidence set** sufficient to reconstruct a timeline (inputs → decisions → outputs → actions).

## Copy/paste checklist
- [ ] I can point to the **first place** model I/O touches production data, observability, or tools.
- [ ] Every context source is classified (trust + sensitivity) and transformed before ingestion.
- [ ] Every output sink is documented (persistence, retention, readers, replay risk).
- [ ] Side-effect actions are gated server-side (authz + validation + least privilege).
- [ ] High-impact actions require explicit review/approval.
- [ ] Audit evidence exists to reconstruct an incident timeline.

## Suggested reading
- [The attack surface is the orchestration loop, not the model]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})
- [Request assembly threat model: reading the diagram]({{ '/articles/agent-security/request-assembly-threat-model/' | relative_url }})
- [How Agentic Control-Plane Failures Actually Happen]({{ '/articles/agent-security/control-plane-failures/' | relative_url }})
- [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})

## References (pinned)

OWASP GenAI (2025):
- [LLM Top 10 index (2025)](https://genai.owasp.org/llm-top-10/)
- [LLM01:2025 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
- [LLM02:2025 Sensitive Information Disclosure](https://genai.owasp.org/llmrisk/llm022025-sensitive-information-disclosure/)
- [LLM05:2025 Improper Output Handling](https://genai.owasp.org/llmrisk/llm052025-improper-output-handling/)
- [LLM06:2025 Excessive Agency](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/)

OWASP (legacy v1.1 — numbering differs from the GenAI 2025 list):
- [Top 10 for Large Language Model Applications (v1.1)](https://owasp.org/www-project-top-10-for-large-language-model-applications/)

OWASP cheat sheets:
- [AI Agent Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html)

OpenAI:
- [Safety in building agents](https://developers.openai.com/api/docs/guides/agent-builder-safety/)

NIST:
- [SP 800-207 Zero Trust Architecture (PDF)](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-207.pdf)
- [SP 800-92 Log Management (landing)](https://csrc.nist.gov/pubs/sp/800/92/final)
- [AI RMF 1.0 (AI 100-1) (PDF)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf)
- [GenAI Profile (AI 600-1) (PDF)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf)