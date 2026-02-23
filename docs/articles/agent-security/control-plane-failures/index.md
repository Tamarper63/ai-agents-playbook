---
title: Control-Plane Failure Patterns in Agentic Tool-Using Systems
permalink: /articles/agent-security/control-plane-failures/
summary: Two recurring control-plane failure patterns—privilege persistence across interaction boundaries and monitoring-only integrity signals (detect without enforcement)—that let untrusted state steer tool execution across steps.
author: Tamar Peretz
published: 2026-02-22
---

## Executive summary

This article describes two **control-plane failure patterns** observed as *audit categories* in multi-step, tool-using LLM systems:

<div class="c-table" role="region" aria-label="Executive summary: control-plane failure patterns" tabindex="0" markdown="1">

| Pattern | What fails | Typical impact | What “good” looks like |
|---|---|---|---|
| 1) Privilege persistence across interaction boundaries | Authorization context is treated as carryover state instead of being re-validated per call | Cross-thread/tab/conversation privilege bleed; writes in the wrong boundary | Per-call authorization at a server-side enforcement point; credentials scoped + bound + short-lived |
| 2) Monitoring-only integrity signals (detect without enforcement) | Integrity risk is detected but does not change execution state | Tainted artifacts keep influencing routing/tools across steps | High-risk signals trigger enforcement actions (hold/deny/quarantine) + circuit breakers |

</div>

**Evidence boundary:** these are **audit patterns**, not claims about a specific vendor trace.

---

## Scope and terms

This article focuses on **control-plane failures** in multi-step, tool-using LLM systems.

### System model (terminology used here)

- **Control plane (ZTA-aligned; used here by extension):** the policy + orchestration layer: session + identity binding, context/memory handling, LLM request construction + routing/selection, policy decision/enforcement for tool use, and monitoring that can trigger enforcement actions (not only alert).  
  (NIST SP 800-207 uses a “control plane” to describe how ZTA logical components communicate, while application data is communicated on a “data plane”; see Section 3.4.)  
- **Data plane (ZTA-aligned; used here by extension):** the external side effects (API calls, state changes) performed by tools/connectors.

### Orchestration terminology (agentic)

- **Orchestration / workflows / control-flow mechanisms**: used as baseline terminology for agentic control flow (see OWASP Securing Agentic Applications Guide 1.0).

### Policy decision vs enforcement (ZTA-aligned)

NIST SP 800-207 describes an abstract access model where access is granted through a **policy decision point (PDP)** and a corresponding **policy enforcement point (PEP)**. In NIST’s model, the PDP decomposes into the **policy engine (PE)** and **policy administrator (PA)**, while the PEP enforces the decision.  
(See References.)

In this article’s vocabulary:
- **PDP (PE+PA):** where an allow/deny decision is made for a proposed step/action.
- **PEP:** where the allow/deny decision is enforced *before* any side effect.

### Design principle anchor (security engineering)

- **Complete mediation:** “Every access to every object must be checked for authority.”  
- **Fail-safe defaults:** access should default to denial unless explicitly permitted.  

(See References.)

---

## Concrete schematic (example)

<figure>
  <img
    src="{{ '/assets/img/posts/control-plane-failures/control-plane-failures.jpeg' | relative_url }}"
    alt="Schematic (illustrative): control-plane failure propagation via session binding, memory/context, routing, tool enforcement, and non-enforcing integrity signals"
  />
  <figcaption><em>Figure 1 — Schematic (illustrative, not raw logs): propagation across session binding, memory/context, routing, tool enforcement, and integrity signals.</em></figcaption>
</figure>

---

## Pattern 1 — Privilege persistence across interaction boundaries (broken boundary semantics)

### What it is
Privileged authorization context (identity binding, tool scopes, “write-capable” mode, or equivalent) **persists across an interaction boundary** (e.g., thread/tab/conversation switch) because the system does not enforce a hard server-side boundary at the policy/enforcement layer.

**Key distinction:** a UI boundary (“Thread A vs Thread B”) is not a security boundary unless the backend and tool gateway treat it as one.

### Why it matters (bounded, testable)
If authorization becomes implicit carryover state, the system stops enforcing **complete mediation** at the moment it matters most: *the next tool call*. That converts “I am allowed” from a per-call server decision into cached context that can drift across steps and boundaries.

### Common root causes (audit targets)
- Reusing the same tool/connector credential across multiple threads without binding it to the relevant subject + interaction boundary (e.g., `principal_id` + `conversation_id/thread_id`).
- Caching an allow decision (“write-capable”) without invalidation on boundary changes (thread switch), privilege drops, or TTL expiry.
- Treating client/UI state as authoritative for tool access instead of enforcing authorization at a server-side gateway.

### Controls (server-side enforcement)
- **Hard boundary on interaction switch:** privileged modes reset on boundary change; write-capable operations require re-authorization within the target boundary.
- **Bound, scoped, short-lived credentials:** credentials minted per principal (and, when applicable, per boundary), with short TTL and minimal scopes (read vs write separated).
- **Per-call authorization (PDP → PEP):** every tool invocation is authorized server-side and enforced before side effects.
- **Least privilege by construction:** smallest feasible tool surface and scope for the workflow.

### What to test (authorized security regression tests)
1) **Cross-boundary privilege bleed test:** obtain write authorization in Boundary A, switch to Boundary B, attempt a write.  
   Expected: **deny/hold** unless Boundary B re-authorizes.
2) **Credential binding test:** replay a valid credential from Boundary A in Boundary B.  
   Expected: **deny** due to binding mismatch.
3) **Authority change test:** revoke role/scope mid-session and repeat the same write.  
   Expected: **deny** on the next call (no stale authorization).

---

## Pattern 2 — Monitoring-only integrity signals (detect without enforcement)

### What it is
The system detects integrity risk (poisoned context, anomalous memory, suspicious tool output, policy-violating arguments) but continues execution (“alert only”), allowing flagged artifacts to be reused across steps.

### Why it matters (bounded, testable)
In multi-step controller loops, contaminated artifacts can influence:
- routing and tool selection,
- argument construction,
- subsequent LLM steps.

A monitoring-only signal does not reduce the likelihood of side effects if the controller proceeds unchanged.

### Common root causes (audit targets)
- Integrity checks run **after** tool selection or argument construction (too late in the lifecycle).
- Alerts are emitted, but execution state does not change (no hold/quarantine/deny path).
- No circuit breaker: repeated integrity signals still allow retries, increasing exposure.

### Controls (fail-safe enforcement for high-risk signals)
- **Fail-safe defaults for high-risk signals:** prefer **hold/deny** over “continue,” and require explicit approval to resume.
- **Quarantine tainted artifacts:** flagged memory/retrieval/tool outputs are prevented from re-entering context until reviewed or replaced.
- **Circuit breakers:** repeated integrity violations stop execution or degrade to read-only; write intent requires operator approval.
- **Pre-execution validation:** tool selection + arguments validated (schema + semantic constraints) before side effects.

### What to test (authorized security regression tests)
1) **Poisoned-input enforcement test:** inject an untrusted chunk that triggers an integrity rule.  
   Expected: the step is **held/blocked** and the chunk is quarantined.
2) **Policy-violating args test:** craft model output that violates an argument constraint (tenant/scope/resource).  
   Expected: rejected by the **PEP** before tool execution.
3) **Repeated-signal circuit-breaker test:** trigger the same integrity signal N times.  
   Expected: execution **stops** or degrades to **read-only**.

---

## Test matrix (copy/paste)

<div class="c-table" role="region" aria-label="Test matrix: control-plane failure patterns" tabindex="0" markdown="1">

| Pattern | Test | Expected enforcement point | Expected result |
|---|---|---|---|
| 1 | Cross-boundary privilege bleed | PEP (server-side) | Deny/hold unless boundary re-authorizes |
| 1 | Credential binding replay | PEP (server-side) | Deny on binding mismatch |
| 1 | Authority change mid-session | PDP+PEP on next call | Deny on next invocation |
| 2 | Poisoned input triggers rule | Controller enforcement / PEP | Hold/deny + quarantine artifact |
| 2 | Policy-violating args | PEP pre-execution | Reject before side effect |
| 2 | Repeated integrity signals | Circuit breaker | Stop or degrade to read-only |

</div>

---

## Minimal audit checklist (copy/paste)

- [ ] Is privileged context invalidated on interaction boundary change (and via TTL)?
- [ ] Are credentials scoped to least privilege and bound to the right subject (and boundary where applicable)?
- [ ] Is every tool call authorized per call (PDP) and enforced pre-side-effect (PEP), not inferred from UI/session carryover?
- [ ] Do integrity signals change execution state for high-risk cases (hold/deny/quarantine), rather than only alert?
- [ ] Is there a circuit breaker for repeated integrity violations (stop / degrade / require approval)?
- [ ] Are tool arguments validated (schema + semantic constraints) before any side effect?

---

## References

- OWASP Cheat Sheet Series — AI Agent Security Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html
- OWASP — Securing Agentic Applications Guide 1.0 (orchestration / workflows / control-flow mechanisms): <https://genai.owasp.org/resource/securing-agentic-applications-guide-1-0/>
- OWASP — Top 10 for LLM Applications (2025): https://genai.owasp.org/llm-top-10/
- NIST SP 800-207 — Zero Trust Architecture (PDP/PEP; PE/PA; control plane vs data plane): https://doi.org/10.6028/NIST.SP.800-207
- NIST SP 800-53 Rev. 5 — Security and Privacy Controls: https://doi.org/10.6028/NIST.SP.800-53r5
- Saltzer & Schroeder (1975) — The Protection of Information in Computer Systems: https://www.cl.cam.ac.uk/teaching/1011/R01/75-protection.pdf

## Suggested reading

- Orchestration risk (controller loop): [The Attack Surface Isn’t the LLM — It’s the Controller Loop]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})
- Request construction checkpoints: [Request assembly threat model: reading the diagram]({{ '/articles/agent-security/request-assembly-threat-model/' | relative_url }})
- Trust boundary audit checklist: [Agentic Systems: 8 Trust-Boundary Audit Checkpoints]({{ '/articles/agent-security/trust-boundary-checkpoints/' | relative_url }})
- Procedure (enforcement gate): [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})