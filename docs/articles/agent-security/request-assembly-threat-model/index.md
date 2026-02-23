---
title: "Request Assembly Threat Model (Author-Mapped): Reading the “ChatGPT Request Assembly Architecture” Diagram"
permalink: /articles/agent-security/request-assembly-threat-model/
summary: "A reviewer-oriented explanation of the request path (S1–S5), context sources, and R1–R8 checkpoints in an author-mapped request-assembly model."
author: Tamar Peretz
published: 2026-02-22
---

> **Scope & provenance (read first):**  
> This page explains an **author-mapped reference model**. It is **not** a vendor-published internal architecture diagram.  
> The diagram should be treated as a **review map** (a stable mental model) for security analysis—**not** as a claim about any specific product’s internal placement.

> **Canonical diagram (SSOT):**  
> See: [/reference/diagrams/chatgpt-request-assembly-architecture/]({{ '/reference/diagrams/chatgpt-request-assembly-architecture/' | relative_url }})

{% include diagrams/figure.html
  src="/assets/img/diagrams/chatgpt-request-assembly-architecture-detailed.svg"
  width="1600"
  height="900"
  alt="Author-mapped request assembly threat model diagram showing S1–S5 request path, context inputs hub, planes (memory, retrieval/caching, tools, observability), optional persistence loops (L1–L3), and risk checkpoints (R1–R8)."
  caption="Author-mapped request assembly threat model (detailed). Not a vendor internal placement diagram." %}


## Why this model exists (for security review)
This model is a reviewer-oriented scaffold for assessing end-to-end request handling beyond the inference step. It focuses on the control points where a system:
- selects and merges context,
- binds authorization to the request,
- routes tools and apps/connectors,
- records telemetry and logs,
- persists state across time (memory/caches).

The goal is to make these control points explicit, reviewable, and easy to audit against policy and authorization boundaries.

## Evidence boundary (what is and isn’t being claimed)
- **This page describes a conceptual review model** aligned to the diagram’s labels (S1–S5, planes, R1–R8).
- **It does not claim internal placement** of components for any vendor or product.
- **Feature-level statements** about memory, tools, and connectors are supported only by the external references listed at the end of this page.
- Any implementation-specific behaviors must be validated in the target system’s documentation, configuration, and logs before being treated as fact.

---
## At a glance (what reviewers can do with this page)
Use this page to:
- **Inventory context sources** that can influence assembly (memory, retrieval, cache/replay, session state).
- **Locate enforcement boundaries** (policy binding, auth binding, tool allowlists).
- **Audit the assembly step** (selection, ordering, truncation) as a first-class risk surface.
- **Assess tool and connector exposure** (approval, argument validation, server-side authorization).
- **Check observability exposure scope** (what is emitted, where it lands, who can access it, retention/redaction).

This is written for **security review and threat modeling**, not for end-user onboarding or product marketing.

## Reviewer workflow (recommended)
1) **Confirm the variant** (pre-assembly retrieval, tool-mediated retrieval, hybrid).  
2) **Enumerate all context inputs** that can reach S3 (including session state, caches, and profile/prefs).  
3) **Locate binding points**: where identity and authorization are bound to the request and to each tool invocation.  
4) **Evaluate S3 determinism**: ordering rules, truncation rules, and “must-include” constraints (fail-closed vs best-effort).  
5) **Enumerate tools/apps/connectors**: scopes, allowlists, approval policy, and argument validation.  
6) **Audit observability**: what content is emitted (inputs/outputs/tool I/O), retention, access control, and redaction.

If you can’t obtain evidence for a step, record it explicitly as a review gap.

## Artifacts to request (audit-ready evidence)
Request equivalents of the following (names vary by system):
- **Policy and routing configuration:** allowlists/denylists, tool/app/connectors enablement, approval gates.
- **Authorization model:** identity binding, scopes/tenancy rules, server-side checks for tool calls.
- **Assembly evidence (S3):** what inputs were eligible, what was selected, ordering policy, truncation outcomes.
- **Memory controls:** enablement, write policy, user visibility/controls, retention/TTL.
- **Retrieval/corpus controls:** ingestion sources, provenance metadata, access-control enforcement at retrieval time.
- **Cache/replay controls:** cache keys (auth-bound), TTL/invalidation, replay eligibility rules.
- **Observability controls:** log/event schemas, redaction rules, retention, and access-control to telemetry sinks.

This list is intentionally system-agnostic; treat it as a checklist for “show me the proof” during review.



## Diagram recap (S1–S5)
### S1 — User Input
Where untrusted instructions enter. This includes plain text, uploaded documents, and any user-controlled content that can influence downstream selection/routing.

### S2 — Gateway / Policy Enforcement
A control-plane step that can enforce:
- allowlists/denylists,
- redaction,
- authorization binding (who is asking, what they are allowed to access),
- policy constraints.

**Reviewer focus:** is S2 a *real* enforcement point (fail-closed), or mostly an annotation layer?

### S3 — Request Assembly / Context Selector
A packaging step that (conceptually):
- selects eligible context sources,
- orders them,
- truncates to constraints,
- produces the final model request payload.

**Reviewer focus:** S3 is where “truth” can be lost (truncation) and where subtle bias can be introduced (ordering/precedence).

### Context Inputs Hub (conceptual merge point)
In the diagram, the **Context Inputs Hub** represents a conceptual merge point: multiple eligible sources (memory, retrieval, cache/replay, session state, and optionally tool results) can be combined **before** the system performs request assembly (S3).

**Reviewer focus:** confirm which sources can reach the hub, what eligibility rules apply, and whether any source can influence ordering/truncation outcomes in S3.

### S4 — LLM Inference
Model generates outputs and may decide to call tools (depending on your system design).

### S5 — Answer
The user-visible output. Depending on system design, post-processing **may** occur here (filters, policy checks, formatting, safety transforms). Reviewers should confirm whether post-processing exists, what it modifies, and whether it is fail-closed.

---

## Planes (what can influence S3 and what can happen after S4)
### Memory plane (green)
For review purposes, treat memory-related inputs as **two distinct mechanisms**:
- **Saved memories** (items intended for reuse across future interactions),
- **Chat history** (prior thread content that can be referenced as context).

The diagram also breaks out memory-adjacent inputs that often behave like “memory” in practice:
- **Bio/profile attributes**
- **User preferences**
- **Session history** (session state/metadata)

**Reviewer focus:** which of these are treated as *data* vs *control-plane* (i.e., do they change tool permissions, system prompts, routing rules)?

### Retrieval / caching (blue)
- **RAG / vector store** (retrieval corpus/embeddings),
- **Cache / replay store** (stale-state and cross-session confusion risks).

**Reviewer focus:** what is “retrieval eligibility” and how is provenance tracked (source, freshness, access control)?

### Execution / tools (purple)
In the diagram, tool execution is triggered from S4 via a **Tool Router / Function Calling** stage, which can invoke **Apps/Connectors / External Tools**.

**Chaining loop (important):** the diagram models chaining as a multi-step loop that can return to **S3 (re-assemble)** before the next inference step. In other words: tool outputs and intermediate state can cause the system to **re-run assembly** (selection/ordering/truncation) for the next turn in the loop.

**Tool-mediated retrieval variant:** retrieval can also occur as a tool action after S4, with results returning through the tool router and (optionally) re-entering context via the hub.

**Reviewer focus:**
- tool-call approval and allowlists,
- server-side authorization per invocation (not only “model choice”),
- argument/schema validation,
- where tool/app/connector outputs can **re-enter** assembly inputs (hub) or influence S3 outcomes.

**Scope note:** treat apps/connectors and MCP-based integrations (Model Context Protocol; MCP) as a tool-access boundary. Reviewers should confirm:
- whether tool use requires explicit approval / allowlisting,
- how URLs and external content returned by tools are validated and attributed,
- whether authorization is enforced server-side for every tool invocation.

Terminology note: Model Context Protocol (MCP) is an open specification for connecting LLM clients to external tools and resources.

### Streaming / observability (orange)
In the diagram, observability is modeled as:
- **Stream Events (event bus)** emitted from **S3 (Request Assembly)** and from **Tool Router / Function Calling**,
- which then flows into **Stream Logs (telemetry sink)**.

**Reviewer focus:** whether prompts, selected context, retrieved docs, tool I/O, and user data can leak into telemetry; who can read it; retention; and redaction **before** persistence/fan-out.

---
## Optional persistence loops (implementation-dependent)
The diagram includes three **optional** persistence loops. These are **implementation-dependent** and must be validated in the target system before being treated as present:

- **L1 (optional write):** apps/connectors/external tools may write into **Saved Memories Store** (or an equivalent memory store).
- **L2 (optional feedback):** the **Answer** may produce signals that influence **RAG / Vector Store** (feedback-to-retrieval loop).
- **L3 (optional feed):** **Stream Logs (telemetry sink)** may influence **Cache / Replay Store** behavior (for example, cache warming or replay eligibility).

**Reviewer focus:** if any loop exists, require explicit policy, authorization binding, and auditability for that loop.


## Variants (explicitly not assumed)
This model supports multiple real-world implementations. Reviewers should confirm which variant applies:

1) **Pre-assembly retrieval:** retrieval happens before S3 and is merged via the **Context Inputs Hub** into assembly inputs.  
2) **Tool-mediated retrieval:** retrieval happens after S4 as a tool action; results return through the tool router and may **optionally** re-enter assembly inputs via the hub.  
3) **Hybrid:** both exist, with different policy controls and potentially different authorization boundaries.

This page does **not** assume which variant is used; the diagram is a **review scaffold**.

---

## The R1–R8 risk checkpoints (reviewer-oriented)
> The red boxes are **analysis anchors**, not claims about a vendor implementation.

Each checkpoint is written in a consistent audit template:
- **Failure mode** (what can go wrong)
- **Evidence to request** (what to ask for)
- **Controls to verify** (what to validate)

### R1 — Context Injection (prompt-level steering)
**Failure mode:** Untrusted input changes behavior, routing, or policy interpretation.

**Evidence to request:**
- Policy decisions and any “blocked/allowed” traces at S2/S3.
- Tool/app/connector invocation records associated with the request (if applicable).
- Any separation mechanism between instructions and untrusted data (if implemented).

**Controls to verify:**
- Policy binding is fail-closed when violations occur.
- Tool/app/connector use is allowlisted and authorization-bound (not “model-suggested only”).
- Untrusted content cannot directly become tool arguments without validation.

### R2 — Memory Poisoning (long-term memory write)
**Failure mode:** Untrusted content becomes persistent state and re-enters later sessions.

**Evidence to request:**
- Memory enablement and write policy (who/what can write, when).
- Visibility/controls for saved memories and chat-history use (as supported by the product).
- Retention/TTL behavior for saved memories (if configured).

**Controls to verify:**
- Memory writes are constrained by explicit policy and scope.
- Review/auditability exists for memory writes (or an explicit gap is recorded).
- Memory cannot silently elevate permissions or tool access.

(Feature context: OpenAI distinguishes saved memories vs chat history in its Memory documentation.)  

### R3 — Retrieval Poisoning (RAG corpus / embeddings)
**Failure mode:** Retrieval returns attacker-controlled or low-integrity content as trusted context.

**Evidence to request:**
- Corpus ingestion rules and allowed sources.
- Provenance metadata available at retrieval time (source, freshness, access control).
- Retrieval-time filtering and authorization checks.

**Controls to verify:**
- Ingestion is controlled and auditable.
- Retrieval enforces authorization (not only ranking).
- Provenance is visible enough for reviewers to assess trust.

### R4 — Assembly Manipulation (ordering + truncation bias)
**Failure mode:** Selection/ordering/truncation changes effective constraints or deletes critical context.

**Evidence to request:**
- Deterministic ordering rules (or explicit statement that ordering is heuristic).
- Truncation outcomes (what was dropped) in a review-safe form.
- Any “must-include” constraints (policy, auth, system constraints) and how they are preserved.

**Controls to verify:**
- Safety/policy constraints cannot be truncated below enforceable thresholds.
- Assembly is explainable enough to audit (inputs → selected → dropped).

### R5 — Replay / Cache Confusion (stale/wrong session state)
**Failure mode:** Wrong cached context is served, causing disclosure or authorization confusion.

**Evidence to request:**
- Cache keying strategy (user/tenant/auth scope/time).
- TTL/invalidation policy; replay eligibility rules.
- Evidence of auth-binding for cache lookups (if caching exists).

**Controls to verify:**
- Cache keys are authorization-bound.
- Sensitive contexts are excluded from replay or require explicit re-validation.
- TTL/invalidation is defined and tested.

### R6 — Tool Hijack (tool selection + argument injection)
**Failure mode:** Model is induced to call unsafe tools or pass unsafe arguments.

**Evidence to request:**
- Tool/app/connector allowlist and scope definitions.
- Approval policy for sensitive tools (if implemented).
- Argument schema validation rules; server-side authorization checks.

**Controls to verify:**
- Tools run under least privilege; sensitive tools require stronger gates.
- Least-privilege is enforced and auditable for tool execution, including logging privileged function use (align to NIST SP 800-53 AC-6 / AC-6(9)).
- Arguments are validated server-side; authorization is enforced per invocation.
- Tool outputs are treated as untrusted unless explicitly trusted.

(Feature context: OpenAI documents tools/function calling and connector/app surfaces; treat these as review surfaces, not internal placement claims.)


### R7 — Stream/Log Exfiltration (prompts/outputs/tool I/O/user data)
**Failure mode:** Sensitive data leaks into logs/telemetry/event buses, widening exposure scope.ֿ

**Evidence to request:**
- What is emitted (events/logs) and whether it includes prompts, retrieval contents, tool I/O.
- Redaction rules applied before emission.
- Access control and retention for telemetry sinks.

**Controls to verify:**
- Redaction happens before persistence and before fan-out.
- Telemetry access is tightly controlled and retention is bounded.
- Audit record content requirements are explicit (event type, timestamp, component/location, source, outcome, identity) and validated (align to NIST SP 800-53 AU-3).
- Log management requirements are documented and enforced (collection, protection, retention, access control), aligned to an organizational log management program (align to NIST SP 800-92).
- Reviewers can verify what is captured without exposing sensitive payloads.

### R8 — Profile/Preference Escalation (bio/prefs become control-plane)
**Failure mode:** Profile attributes/preferences change routing, tool access, or policy decisions beyond intended scope.

**Evidence to request:**
- Schema of profile/preferences and documented influence paths (what they can affect).
- Audit logs for changes to profile/preferences (if available).
- Policy boundaries separating “presentation prefs” from “permissioning.”

**Controls to verify:**
- Preferences are typed and constrained (presentation-only vs control-plane).
- No preference/profile field can silently grant tool access or bypass policy.
- Any control-plane effect is explicit, allowlisted, and auditable.

---

## Minimal reviewer checklist (use with the diagram)

1. Identify all context sources feeding S3; classify them by integrity and authorization.
2. Confirm where authorization is bound and where it can be bypassed (S2/S3/tool/app/connector layer).
3. Enumerate tools and apps/connectors: scopes, approval policy, and server-side enforcement.
4. Review persistence: saved memory writes, retrieval feedback loops, cache/replay behavior, and retention.
5. Audit observability: what is emitted (events/logs), who can read it, and how it is redacted.

---

## Suggested reading
- [The Attack Surface Starts Before Agents — The LLM Boundary]({{ '/articles/agent-security/llm-boundary-first-touch/' | relative_url }})
- [The Attack Surface Isn’t the Model — It’s the Orchestration Loop]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})
- [Prompt Assembly Policy Enforcement: Typed Provenance to Prevent Authority Confusion]({{ '/articles/agent-security/prompt-assembly-policy-enforcement/' | relative_url }})
- [How Agentic Control-Plane Failures Actually Happen]({{ '/articles/agent-security/control-plane-failures/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})

## References (official feature docs; not internal placement claims)
- OpenAI — Memory (saved memories / chat history): https://help.openai.com/en/articles/8983136-what-is-memory
- OpenAI — Memory FAQ: https://help.openai.com/en/articles/8590148-memory-faq
- OpenAI API — Function/tool calling: https://developers.openai.com/api/docs/guides/function-calling/
- OpenAI API — Tools overview: https://developers.openai.com/api/docs/guides/tools/
- OpenAI — Apps in ChatGPT (formerly “Connectors”): https://help.openai.com/en/articles/11487775-connectors-in-chatgpt
- OpenAI API — Connectors and MCP servers (risks/safety/approvals): https://developers.openai.com/api/docs/guides/tools-connectors-mcp/

- NIST SP 800-30 Rev. 1 — Guide for Conducting Risk Assessments: https://nvlpubs.nist.gov/nistpubs/legacy/sp/nistspecialpublication800-30r1.pdf
- NIST SP 800-154 (IPD) — Guide to Data-Centric System Threat Modeling: https://csrc.nist.gov/files/pubs/sp/800/154/ipd/docs/sp800_154_draft.pdf
- NIST SP 800-92 — Guide to Computer Security Log Management: https://nvlpubs.nist.gov/nistpubs/legacy/sp/nistspecialpublication800-92.pdf
- NIST SP 800-53 Rev. 5 — Security and Privacy Controls for Information Systems and Organizations: https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf
- NIST AI 100-1 — AI RMF 1.0: https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf

- OWASP — Top 10 for LLM Applications: https://owasp.org/www-project-top-10-for-large-language-model-applications/
- NIST — AI RMF Generative AI Profile (NIST AI 600-1): https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf