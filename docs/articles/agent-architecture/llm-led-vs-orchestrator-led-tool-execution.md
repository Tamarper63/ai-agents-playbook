---
title: LLM-led vs orchestrator-led tool execution (architecture tradeoffs)
permalink: /articles/agent-architecture/llm-led-vs-orchestrator-led-tool-execution/
summary: A control-plane placement comparison across reliability, observability, cost, product constraints, and security (policy binding as one dimension).
---

## Abstract

When an LLM can call tools, the architecture decision is not “agents vs no agents.” It’s **where execution authority lives**: inside the model loop, or outside it in an orchestrator/control plane.

This article compares two tool-execution patterns:

- **LLM-led execution:** the model selects and triggers tool calls inside its own loop.
- **Orchestrator-led execution:** the model proposes intents/steps; an external orchestrator validates, authorizes, and executes.

Security and policy enforcement matter, but they are **one dimension** of a broader tradeoff set that includes reliability, debugging, observability/auditability, latency, and cost governance.

## Definitions (used in this article)

- **Execution authority:** the component that can cause side effects (writes, deletes, payments, privileged actions).
- **Control plane:** the decision path (routing, validation, authorization, budgets, approvals).
- **Data plane:** the path where side effects occur (actual external calls, state changes).
- **Policy binding (operational):** the point where an allow/deny decision is enforced *before* side effects.

A useful reference for control-plane separation and policy decision/enforcement components is NIST SP 800-207 (Zero Trust Architecture) [8][9].

## Two reference architectures

### A) LLM-led execution (authority in the model loop)

<figure>
  <img
    src="{{ '/assets/img/posts/llm-led-vs-orchestrator-led-tool-execution/llm-control-plane.png' | relative_url }}"
    alt="LLM-led execution: authority in the model loop"
  />
  <figcaption><em>Figure 1 — LLM-led execution (authority in the model loop).</em></figcaption>
</figure>


### B) LLM-led execution (authority in the model loop)

<figure>
  <img
    src="{{ '/assets/img/posts/llm-led-vs-orchestrator-led-tool-execution/orchestrator-led.png' | relative_url }}"
    alt="Orchestrator-led execution: authority outside the model; control-plane gating"
  />
  <figcaption><em>Figure 2 — Orchestrator-led execution (authority outside the model).</em></figcaption>
</figure>

## Why this is an architecture decision (not a prompting decision)

Prompt text can express intent, but it is not an enforcement boundary. As systems grant the model more operational authority (tool calls with side effects), failures that would otherwise “just” produce incorrect text can translate into incorrect actions.

That risk translation is what makes **authority placement** the primary design axis.

## Tradeoffs (architecture-first)

### 1) Reliability & failure containment

**LLM-led execution**

- Failure containment depends heavily on the model behaving as intended on every step.
- When tool loops exist, recovery logic can become implicit and hard to bound without an external governor.

**Orchestrator-led execution**

- Enables deterministic containment mechanisms:
  - precondition checks (state checks, idempotency keys),
  - bounded retries/backoff,
  - deny-by-default for side-effecting actions,
  - fallback flows that are independent of model phrasing.

This is not a guarantee of correctness; it is control placement that makes deterministic containment feasible.

### 2) Debuggability & incident response

**LLM-led execution**

- Postmortems often require reconstructing behavior from model outputs, tool traces, and partial logs.

**Orchestrator-led execution**

- Centralizes structured decision evidence:
  - what the model proposed,
  - what validators returned,
  - why the request was allowed/denied,
  - what side effects were executed.

### 3) Observability & auditability

**LLM-led execution**

- Telemetry is often per-tool and uneven unless strongly standardized.

**Orchestrator-led execution**

- Makes a consistent event pipeline straightforward:
  - proposed intent → validated intent → authorization decision → executed side effects.
- Supports a policy decision/enforcement separation pattern that is widely used in security architecture (see NIST SP 800-207) [8][9].

### 4) Latency & throughput

**LLM-led execution**

- Fewer hops can reduce latency in simple flows.

**Orchestrator-led execution**

- Adds a decision hop + validations, which can increase latency.
- In return, can reduce costly cascades (loops, retries, tool churn) by stopping early and deterministically.

### 5) Cost governance (tokens, tools, and loops)

Unconstrained tool loops and inference usage are recognized as a distinct risk category by OWASP (LLM10:2025 Unbounded Consumption) [5]. Regardless of pattern, budgets must be enforced somewhere deterministic.

**Orchestrator-led execution** typically centralizes:

- token/time/tool-call caps,
- tenant quotas,
- backpressure and rate limits,

outside the model loop.

### 6) Product constraints (human-in-the-loop vs autonomy)

Where product requirements include explicit confirmations (payments, deletes, privileged writes), orchestrator-led execution supports “no side effects without verified confirmation” as a deterministic rule, independent of model compliance.

## Security & governance (policy binding as one dimension)

This section is intentionally not the thesis; it is one tradeoff dimension that becomes critical when tools have side effects.

### Controls that should not live only in the prompt

OWASP’s LLM Top 10 frames several common failure modes as application/system responsibilities:

- **Authorization before action:** enforce RBAC/ABAC, explicit allowlists, and approval/deny gates outside the model loop.
- **Output handling:** validate/sanitize model outputs before downstream execution (LLM05:2025 Improper Output Handling) [3].
- **Context hygiene:** do not rely on system prompts as secrets; reduce leakage exposure (LLM07:2025 System Prompt Leakage) [4].
- **Budgets / loop breakers:** constrain tokens/time/tool calls to reduce runaway resource consumption (LLM10:2025 Unbounded Consumption) [5].

### Why authority placement affects injection-to-action risk

- OWASP defines **Prompt Injection** as a primary risk category (LLM01:2025) and notes that RAG and fine-tuning do not fully mitigate it [1].
- The OWASP prompt-injection prevention guidance emphasizes that LLM apps often process instructions and data together without strong separation [2].
- Research on **indirect prompt injection** analyzes how external content can embed instructions that are treated as if they were directives [10].

If the model can directly execute tools, injection-style failures are more likely to reach the “action layer” unless deterministic gates exist.

## Where MCP fits (integration layer ≠ governance layer)

MCP standardizes how tools/resources connect to AI applications, but MCP is not a full governance system.

- MCP’s specification provides the protocol contract and transport details [6].
- MCP includes security guidance/best-practice material [7].
- MCP authorization is defined at the transport level (HTTP-based transports) [11].

Practical implication: MCP can simplify tool connectivity, but enforcement still needs an orchestrator/policy layer: allowlists, approvals, argument validation, budgets, and auditable decisions.

## Decision matrix (summary)

| Dimension | LLM-led execution | Orchestrator-led execution |
| --- | --- | --- |
| Where authority lives | In the model loop | External controller / control plane |
| Reliability containment | Harder to make deterministic | Deterministic gates + preconditions |
| Debuggability | Harder to reconstruct | Explicit decision evidence possible |
| Observability/audit | Often uneven | Centralized decision logging possible |
| Latency | Often lower in simple flows | Extra hop + validations |
| Cost governance | Must be added externally anyway | Natural centralization point |
| Security blast radius | Tends to expand with powerful tools | Can be constrained via gates |

## Minimal implementation checklist (tool execution)

- Inventory tools; remove unused capabilities (reduce surface).
- Default-deny for side-effecting tools; require explicit allowlists per action.
- Enforce authorization outside the model (RBAC/ABAC, approvals).
- Validate tool arguments (schema, bounds, canonicalization).
- Validate/sanitize outputs before downstream execution (especially if executing, rendering, or storing).
- Treat retrieved content/tool metadata as untrusted input; defend against indirect prompt injection.
- Add budgets: token/time/tool-call limits and tenant quotas.
- Record a decision trail: proposed → validated → allowed/denied → executed.

## Suggested next reads in this repo

- [The Attack Surface Isn’t the LLM — It’s the Controller Loop]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})
- [How Agentic Control-Plane Failures Actually Happen]({{ '/articles/agent-security/control-plane-failures/' | relative_url }})

## References

[1] OWASP GenAI Security Project — LLM01:2025 Prompt Injection  
https://genai.owasp.org/llmrisk/llm01-prompt-injection/

[2] OWASP Cheat Sheet Series — LLM Prompt Injection Prevention Cheat Sheet  
https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html

[3] OWASP GenAI Security Project — LLM05:2025 Improper Output Handling  
https://genai.owasp.org/llmrisk/llm05-supply-chain-vulnerabilities/

[4] OWASP GenAI Security Project — LLM07:2025 System Prompt Leakage  
https://genai.owasp.org/llmrisk/llm07-insecure-plugin-design/

[5] OWASP GenAI Security Project — LLM10:2025 Unbounded Consumption  
https://genai.owasp.org/llmrisk/llm102025-unbounded-consumption/

[6] Model Context Protocol — Specification (2025-03-26)  
https://modelcontextprotocol.io/specification/2025-03-26

[7] Model Context Protocol — Security Best Practices (draft)  
https://modelcontextprotocol.io/specification/draft/basic/security_best_practices

[8] NIST SP 800-207 — Zero Trust Architecture (DOI)  
https://doi.org/10.6028/NIST.SP.800-207

[9] NIST SP 800-207 — PDF  
https://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.SP.800-207.pdf

[10] Greshake et al. (2023) — “Not what you’ve signed up for” (Indirect Prompt Injection), arXiv  
https://arxiv.org/abs/2302.12173

[11] Model Context Protocol — Authorization (2025-06-18)  
https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization



