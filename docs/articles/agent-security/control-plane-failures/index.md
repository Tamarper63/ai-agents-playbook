---
title: Control-Plane Failure Patterns in Agentic Tool-Using Systems
permalink: /articles/agent-security/control-plane-failures/
summary: Two recurring control-plane failure patterns—authorization-context leakage and non-gating integrity signals—that let untrusted state steer tool execution across steps.
---

## Scope and terms
This article focuses on **control-plane failures** in multi-step, tool-using LLM systems.

In this post:

- **Control plane:** session + identity binding, context/memory handling, request assembly/routing, policy decision/enforcement for tool use, and monitoring that can *gate* execution (not only alert).
- **Data plane:** the actual external side effects (API calls, state changes) performed by tools/connectors.
- **Policy Decision Point (PDP):** where an allow/deny decision is made for a proposed step/action.
- **Policy Enforcement Point (PEP):** where the allow/deny decision is enforced *before* any side effect.

Important: the examples below are **audit patterns**, not claims about specific production traces.

## Concrete schematic (example)
<figure>
  <img
    src="{{ '/assets/img/posts/control-plane-failures/control-plane-failures.jpeg' | relative_url }}"
    alt="Schematic: control-plane failures propagating via session state, memory/context, routing, tools/capabilities, and non-gating integrity signals"
  />
  <figcaption><em>Figure 1 — Schematic (not raw logs): control-plane failure propagation across session, memory/context, routing, tool enforcement, and non-gating integrity signals.</em></figcaption>
</figure>

## Pattern 1 — Authorization-context leakage across threads (broken session boundary)

### What it is
Privileged state (identity binding, tool scopes, or “write-capable” mode) **persists or leaks** across chats/tabs/threads because the system does not enforce a hard boundary at the server and tool layers.

### Why it matters
When authorization becomes implicit state (“the UI says I’m allowed”), the boundary shifts from **per-call server-side authorization** to **state carryover**. That is a control-plane failure: the system stops applying **complete mediation** (re-checking authority on each access) and relies on cached context.

### Common root causes (audit targets)
- Reusing the same connector token across multiple threads without binding it to `principal_id + thread_id`.
- Caching an allow decision (“write-capable”) and failing to invalidate it on boundary changes (thread switch, privilege drop, TTL expiry).
- Treating client/UI state as authoritative for tool access instead of enforcing authorization at the tool gateway.

### Controls (server-side enforcement)
- **Hard boundary at conversation/thread switch:** reset privileged mode; require re-authorization for write-capable operations.
- **Thread- and principal-bound credentials:** mint tool credentials per `principal_id` (and ideally per thread), with short TTL and narrow scopes.
- **Per-call authorization:** authorize **every** tool invocation server-side (PDP decision + PEP enforcement), even when a session is “already authenticated.”
- **Least privilege:** keep tool scopes minimal; separate read vs write capabilities.

### What to test (reproducible security tests)
1) **Cross-thread downgrade test:** escalate privileges in Thread A, switch to Thread B, attempt a write. Expected: denied unless Thread B re-authorizes.
2) **Token binding test:** replay a valid tool token from Thread A in Thread B. Expected: denied due to subject/binding mismatch.
3) **Complete-mediation test:** simulate an authority change mid-session (role removed) and retry the same write. Expected: denied on the next call.

## Pattern 2 — Integrity signals without enforcement (detective-only controls)

### What it is
The system detects integrity risk (poisoned context, anomalous memory, suspicious tool output, policy-violating arguments) but continues execution (“alert only”), allowing flagged artifacts to be reused across steps.

### Why it matters
In multi-step systems, contamination compounds: the same tainted context can influence routing, tool calls, and subsequent LLM steps. A detective-only signal does not reduce the probability of a side effect if the controller loop proceeds unchanged.

### Common root causes (audit targets)
- Integrity checks run *after* tool selection or argument construction (too late in the step lifecycle).
- Alerts are emitted to logs/monitoring but do not change the execution state (no hold/quarantine).
- No circuit breaker: repeated integrity signals still allow retries, increasing exposure.

### Controls (fail-safe enforcement for high-risk signals)
- **Fail-safe defaults:** for high-risk integrity violations, prefer “hold/deny” over “continue,” and require explicit approval to resume.
- **Quarantine tainted artifacts:** prevent flagged memory/retrieval/tool outputs from re-entering context until reviewed or replaced.
- **Circuit breakers:** stop after repeated integrity signals; switch to read-only; require operator approval for any write intent.
- **Pre-execution validation:** validate tool selection and arguments (schema + semantic constraints) before any side effect.

### What to test (reproducible security tests)
1) **Poisoned-retrieval gate test:** inject a retrieval chunk that triggers an integrity rule. Expected: the step is held/blocked and the chunk is quarantined.
2) **Policy-violating args test:** craft model output that violates an argument constraint (scope/tenant/resource). Expected: rejected by the PEP before tool execution.
3) **Repeated-signal circuit-breaker test:** trigger the same integrity alert N times. Expected: execution stops or degrades to read-only.

## Minimal audit checklist (copy/paste)
- [ ] Does privileged state reset at the conversation/thread boundary (and expire via TTL)?
- [ ] Are tool credentials bound to principal (and ideally thread) and scoped to least privilege?
- [ ] Is every tool call authorized server-side per call (PDP + PEP), not inferred from UI/session state?
- [ ] Do integrity signals gate execution (hold/deny/quarantine) for high-risk cases, rather than only alert?
- [ ] Is there a circuit breaker for repeated integrity violations (stop / degrade / require approval)?
- [ ] Are tool arguments validated (schema + semantic constraints) before any side effect?

## References
- OWASP Cheat Sheet Series — AI Agent Security Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html
- NIST SP 800-207 — Zero Trust Architecture (PDP/PEP): https://doi.org/10.6028/NIST.SP.800-207
- NIST SP 800-53 Rev. 5 — Security and Privacy Controls: https://doi.org/10.6028/NIST.SP.800-53r5
- Saltzer & Schroeder (1975) — The Protection of Information in Computer Systems: https://www.cl.cam.ac.uk/teaching/1011/R01/75-protection.pdf