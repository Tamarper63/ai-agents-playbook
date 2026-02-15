---
title: Exploiting the Trust Boundary in Agentic Systems
permalink: /articles/agent-security/trust-boundary-checkpoints/
summary: A practical audit checklist of 8 trust checkpoints where untrusted artifacts can steer routing, tool use, and write-path actions in chained LLM systems.
---

## Overview
This post treats “prompt injection” and adjacent manipulation as a **trust-boundary** problem in chained agentic pipelines:

**Ingress → context building → retrieval → orchestration → tool routing → action execution → output/egress**

The diagram is a schematic. The checklist below expands it into **8 checkpoints** you can audit in real systems.

## Core terms (as used here)
- **Trust boundary:** a point where data from a less-trusted source can affect decisions or privileged actions.
- **Untrusted artifact:** any external content (user input, tickets, docs, web pages, files, tool outputs) whose intent and integrity are not guaranteed.
- **Instruction vs data separation:** rules that prevent untrusted artifacts from being interpreted as policy, tool permissions, or routing constraints.
- **Write path:** any operation that changes state in an external system (e.g., create/update/delete, invite/reset, configuration change).

## Schematic (diagram)
<figure>
  <img
    src="{{ '/assets/img/posts/trust-boundary-checkpoints/trust-boundary.jpeg' | relative_url }}"
    alt="Schematic: exploiting the trust boundary in an agentic pipeline from untrusted artifacts through gateway, context building, orchestration, tool routing, write gating, and audit logging"
  />
  <figcaption><em>Figure 1 — Schematic view of a trust-boundary attack surface in an agentic pipeline (not raw logs).</em></figcaption>
</figure>

## Why this is a trust-boundary issue (not a “prompt trick”)
In chained systems, untrusted content can enter through multiple paths (user prompts, tickets, docs, web pages, files). Risk increases when that content can influence:
- **context selection** (what is included and how it is prioritized),
- **planning/routing** (task decomposition and tool choice),
- **tool invocation** (arguments, scopes, and targets),
- **write-path reachability** (whether the system crosses from “read” to “modify”).

OWASP lists **Prompt Injection** as a top risk category (LLM01) for LLM/GenAI applications, and OWASP’s agent guidance emphasizes least privilege, authorization for high-risk actions, and input validation.  

## Threat model (minimal)
**Attacker capability:** can control or partially control at least one untrusted artifact (direct input or retrieved/ingested content).  
**Defender mistake:** the pipeline treats parts of that artifact as decision authority (routing constraints, tool permissions, action approvals, or policy).  
**Impact class:** (a) **steering** (wrong plan/tool), (b) **exfiltration** (retrieve/export sensitive data), (c) **unauthorized write** (state change), often with (d) **audit evasion** (missing provenance/correlation).

## Defensive invariants (what you want to be true)
1) **Untrusted artifacts never become policy.** They may be summarized/quoted, but they do not define system rules, tool allowlists, or auth decisions.  
2) **Write paths require explicit authorization** and server-side enforcement (not just model compliance).  
3) **Tool access is capability-scoped** (deny-by-default, minimal permissions, explicit targets).  
4) **Provenance is preserved end-to-end** (what came from where, and what influenced which decision).

## The 8 trust checkpoints (audit checklist + deep-dive)

### 1) Ingress / Gateway
**What can go wrong**
- Identity/auth is not bound to the request context used by the orchestrator.
- Input normalization rewrites meaning (e.g., hidden instructions become “clean” text).
- Rate/abuse controls are missing for iterative probing.

**Controls**
- Bind **principal/session/tenant** to every downstream step (including retrieval and tool calls).
- Normalize in a way that **preserves provenance** (store raw + normalized + transformation metadata).
- Apply request-class policies (e.g., “read-only mode” vs “write-capable mode”).

**Audit questions / tests**
- Can a request reach tool routing without an authenticated principal?
- Do you log raw input + normalized input + policy decisions at ingress?

---

### 2) Request assembly / Context selection
**What can go wrong**
- Context builder treats retrieved text as higher-priority than system constraints.
- “Helpful instructions” embedded in artifacts are appended near the end where the model weights them strongly.
- No explicit labeling, so the model cannot distinguish **data** from **instructions**.

**Controls**
- Render context with **strict sections** (Policy/System → Developer constraints → User request → Retrieved data as QUOTED/DELIMITED).
- Add machine-checkable labels (e.g., `SOURCE=RETRIEVAL`, `TRUST=UNTRUSTED`, `ROLE=DATA`) and enforce them in the router.
- Prefer structured context objects over free-form concatenation when feasible.

**Audit questions / tests**
- Is retrieved content always enclosed/delimited and labeled as untrusted?
- Can a retrieved artifact override tool constraints or action gating in practice?

---

### 3) Retrieval / Ingestion
**What can go wrong**
- Indirect injection via docs/pages/tickets that are treated as “authoritative” because they are internal.
- Retrieval returns high-relevance malicious chunks that get promoted into the context window.
- Tool outputs (e.g., web page render) include hidden instruction channels (HTML, metadata) that get passed through.

**Controls**
- Treat **all retrieval results as untrusted** unless cryptographically verified and explicitly allowlisted.
- Apply retrieval-time filters: domain/source allowlists, MIME/type handling, max-size, strip active content, and chunk-level provenance.
- Record retrieval evidence: `query`, `source`, `timestamp`, `hash`, `chunk_ids`.

**Audit questions / tests**
- Can a single retrieved chunk steer the plan into a privileged tool path?
- Do you persist provenance for each chunk that enters context?

---

### 4) Orchestrator / Planner
**What can go wrong**
- The plan is treated as “truth” and executed without validation.
- The planner can introduce new subgoals (“also export logs”) not requested by the user.
- Multi-agent handoffs lose provenance (“agent B” cannot see what was untrusted).

**Controls**
- Treat plans as **untrusted intermediate artifacts**; validate against a policy gate before execution.
- Enforce plan schemas: allowed action types, allowed tools, allowed targets, required approvals for write intents.
- Preserve provenance across agents: attach artifact lineage to plan steps.

**Audit questions / tests**
- Can the planner add tool calls outside an allowlist?
- Is there a policy decision point (PDP) that evaluates the plan before execution?

---

### 5) LLM inference (instruction hierarchy failure modes)
**What can go wrong**
- Instruction hierarchy collapses: untrusted artifacts are interpreted as higher-priority constraints.
- The model is coaxed into producing tool arguments that violate constraints (scope expansion, target changes).
- Refusal policies degrade under multi-step decomposition.

**Controls**
- Reduce free-form authority: push critical decisions into deterministic policy checks (server-side).
- Use structured outputs for tool calls and validate strictly (schema + semantic constraints).
- Add “reason-to-act” checks: the system must justify why a tool/action is necessary, then validate that justification.

**Audit questions / tests**
- Are tool arguments accepted purely because the model produced them?
- Are there enforced constraints on tenant/target/resource IDs?

---

### 6) Tool router + tools/connectors
**What can go wrong**
- Router selects a high-privilege tool when a low-privilege tool would suffice.
- Argument manipulation: attacker steers parameters (e.g., export all, invite admin, change config).
- Connectors are over-scoped (broad OAuth scopes, shared tokens, cross-tenant reach).

**Controls**
- Capability-based routing: tools are exposed as minimal capabilities (read-only vs write) with narrow scopes.
- Deny-by-default allowlists per intent category; require explicit justification for elevated tools.
- Hard constraints on arguments: allowed endpoints, allowed fields, allowed ranges, tenant-bound resources.

**Audit questions / tests**
- Can a “read” request cause a “write” tool to be invoked?
- Are connector tokens scoped per tenant/user, and are scopes minimal?

---

### 7) Action execution (write paths)
**What can go wrong**
- Model output directly triggers writes (“just do it”) with no secondary gate.
- Human approval is cosmetic (model can reframe the question to get approval).
- No separation between “draft” and “commit”.

**Controls**
- Two-step execution: **propose** (dry-run + diff) → **authorize** → **commit**.
- Server-side authorization and policy enforcement for every write call (including rate limits and target checks).
- High-impact operations require stronger controls (step-up auth, dual control, or break-glass workflows) depending on risk tolerance.

**Audit questions / tests**
- Is there an enforceable “write gate” that the model cannot bypass?
- Do write calls require an explicit, logged authorization decision?

---

### 8) Output / Egress
**What can go wrong**
- Leakage of sensitive context (system/developer instructions, secrets, internal IDs).
- Unsafe formatting that becomes executable downstream (e.g., JSON/HTML that another system interprets as commands).
- Propagation into durable stores (tickets, KBs, chat exports) without redaction.

**Controls**
- Output filtering/redaction for sensitive classes; blocklist high-risk data types.
- Encode/escape outputs by sink (HTML, Markdown, JSON) to avoid “insecure output handling”.
- Attach provenance tags to outputs so downstream systems can treat them as untrusted by default.

**Audit questions / tests**
- Can outputs contain tool tokens, secrets, or internal policy text?
- Is there a sink-aware escaping/validation layer?

## Concrete example (pattern)
A normal support ticket embeds instruction-like text disguised as troubleshooting steps.  
If the pipeline promotes that ticket text into the decision layer (planning/routing/tool arguments), it can steer tool calls that export data, reset access, invite users, or change configuration—especially if write paths are not gated server-side.

## Minimum audit log fields (to make incidents tractable)
Capture, at least:
- **Correlation IDs**: request_id, session_id, tenant_id, principal_id
- **Artifact provenance**: source type, URI/identifier, timestamps, hashes, chunk_ids
- **Decision records**: policy evaluation results, tool selection rationale, plan validation results
- **Tool I/O**: tool name, arguments (redacted where needed), responses (bounded/redacted), status codes
- **Write gating**: authorization decision, approver identity (if any), diff/dry-run output, commit outcome

## Baseline controls (agentic systems)
- Treat retrieved/ingested content as **untrusted data** and prevent it from being interpreted as policy/instruction authority.
- Gate write/actions behind explicit authorization and **server-side** policy enforcement.
- Constrain tools by allowlisted actions/scopes (deny-by-default) with tenant-bound targets.
- Audit end-to-end: input → retrieved artifacts → plan → tool I/O → downstream action (with correlation IDs and provenance).

## References
- [OWASP Top 10 for Large Language Model Applications — Prompt Injection (LLM01)][owasp-top10]
- [OWASP GenAI Security Project — LLM01: Prompt Injection][owasp-genai-llm01]
- [OWASP Cheat Sheet Series — AI Agent Security Cheat Sheet][owasp-agent-cheatsheet]
- [NIST AI 600-1 — Generative AI Profile][nist-ai-600-1]

[owasp-top10]: https://owasp.org/www-project-top-10-for-large-language-model-applications/
[owasp-genai-llm01]: https://genai.owasp.org/llmrisk/llm01-prompt-injection/
[owasp-agent-cheatsheet]: https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html
[nist-ai-600-1]: https://doi.org/10.6028/NIST.AI.600-1