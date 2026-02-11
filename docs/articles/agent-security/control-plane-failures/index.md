---
title: How Agentic Control-Plane Failures Actually Happen
permalink: /articles/agent-security/control-plane-failures/
summary: Two audit patterns in session/memory and tool enforcement that turn agent incidents into control-plane boundary failures.
---

## Scope and definitions
This article focuses on **control-plane failures** in tool-using or multi-step LLM systems.

In this post, **control-plane** means:
- session and identity binding
- memory/context persistence and reuse
- request assembly & routing
- tool/capability enforcement
- monitoring that can *gate* execution (not only alert)

Important: the examples below are **patterns to audit**. Any statements about “observed traces” are out of scope unless you publish reproducible evidence artifacts.

## Concrete schematic (example)
<figure>
  <img
    src="{{ '/assets/img/posts/control-plane-failures/control-plane-failures.jpeg' | relative_url }}"
    alt="Schematic: how control-plane failures propagate via session state, shared memory/context, routing, tools/capabilities, and non-gating integrity alerts"
  />
  <figcaption><em>Figure 1 — Schematic (not raw logs): control-plane failure propagation across session, memory/context, routing, tool enforcement, and non-gating integrity alerts.</em></figcaption>
</figure>

## Pattern 1 — Cross-thread privilege carryover (broken session boundary)
### What it is
Privileged state (identity, tool scope, elevated capabilities) **persists or leaks** across chats/tabs/threads when the system fails to enforce a hard boundary.

### Why it matters
When authorization becomes implicit state (“the UI says I’m allowed”), the boundary shifts from **server-enforced authz** to **state carryover** — a control-plane failure mode.

### Controls (server-side)
- Hard reset at conversation boundary + TTL/expiry for any privileged state.
- Thread-scoped privileges (no cross-thread reuse).
- Server-side authorization on **every** tool invocation (never trust client/UI state).
- Least privilege + per-tool permission scoping for sensitive tools.

(See OWASP agent guidance on least privilege, explicit tool authorization, and memory isolation/expiration.)

## Pattern 2 — Integrity alerts without execution gating (detective-only)
### What it is
The system detects integrity risk (poisoned context, anomalous memory, suspicious tool output) but continues execution (“alert only, no hold/no gate”), allowing flagged context to be reused across steps.

### Why it matters
In multi-step workflows, contamination compounds: the same tainted context can influence routing, tool calls, and subsequent LLM steps.

### Controls (fail-closed by default)
- Gate/hold on integrity violations (block or require explicit approval).
- Circuit breaker on repeated integrity signals.
- Escalation / operator confirmation for high-impact actions.
- Output validation before execution of side-effectful operations.

(These controls align with OWASP recommendations for approvals/guardrails and with classical security principles: secure failure and fail-safe defaults.)

## Minimal audit checklist (copy/paste)
- [ ] Does privileged state expire and reset at the conversation boundary?
- [ ] Are memory/context stores isolated per user/session and bounded by TTL/limits?
- [ ] Is every tool call authorized server-side (per-call), not inferred from UI/session state?
- [ ] Do integrity alerts *gate* execution (hold/block) rather than only alert?
- [ ] Is there a circuit breaker for repeated integrity violations?

## References
- OWASP AI Agent Security Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html
- NIST SP 800-53 Rev. 5 (Secure failure and recovery): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf
- Saltzer & Schroeder (1975), The Protection of Information in Computer Systems: https://www.cs.virginia.edu/~evans/cs551/saltzer/
