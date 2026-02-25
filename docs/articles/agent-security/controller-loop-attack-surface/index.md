---
title: The attack surface is the orchestration loop, not the model
permalink: /articles/agent-security/controller-loop-attack-surface/
summary: How multi-step orchestration (controller) loops change the threat model in tool-using systems, and where to enforce separation, authorization, validation, and budgets to reduce prompt injection, tool misuse, unsafe writes, and unbounded consumption.
author: Tamar Peretz
published: 2026-02-22
---

> **What this page is:** a vendor-agnostic threat model and control map for multi-step tool-using LLM systems.  
> **What this page is not:** a claim about any specific vendor trace or internal implementation.

## Executive summary

When a system introduces an **orchestration loop** (a controller loop that repeatedly plan/act/observe/decide), the attack surface shifts from “the model” to the **control plane** that:
- selects plans and tools,
- carries state across steps,
- decides stop/retry,
- and can cross into **write paths** (side effects).

This page uses OWASP GenAI categories to structure risks and controls:
- **LLM01 Prompt Injection** (including indirect injection via retrieved/tool text),
- **LLM06 Excessive Agency** (capabilities/permissions exceed what is justified),
- **LLM10 Unbounded Consumption** (loop-driven cost/availability risk).

(References at the end.)

---

## Core terms (as used here)

- **Orchestration loop (controller loop):** control logic that sequences steps (plan → act → observe → decide), including retries and stop conditions.
- **Workflow:** LLM + tools executed through predefined code paths (fixed order / graph).
- **Agent:** the model can dynamically propose its own steps and tool usage at runtime (within enforced bounds).
- **Policy decision point (PDP):** evaluates a proposed plan/action against policy and returns allow/deny.
- **Policy enforcement point (PEP):** enforces allow/deny *before* any side effect (e.g., before tool calls/writes).
- **Instruction/data separation:** prevents untrusted content from being interpreted as policy, permissions, routing constraints, approvals, or tool arguments.
- **Write path:** any operation that changes external state (create/update/delete, permissions, exports, configuration changes).
- **Loop budgets:** hard limits on steps/time/cost/retries that cannot be bypassed by the loop.

(Workflow vs agent distinctions are aligned with Anthropic and LangGraph; see References.)

---

## Where the loop lives (control plane vs data plane)

A practical split for auditing is:

- **Data plane:** user input, retrieved text, tool observations (what the model reads).
- **Control plane:** orchestration + policy decision/enforcement logic (routing, tool selection, stop/retry, write-path enforcement).

Introducing a loop increases the number of control-plane decisions per request; the control plane becomes the dominant trust boundary.

### Single-shot tool use (minimal control plane)

```text
[request + context] -> [model] -> (optional tool call) -> [model] -> [final output]
```

### Orchestration loop (expanded control plane)

```text
[request + context]
      |
      v
[orchestration loop] ---> [tool router] ---> [tools/connectors]
      |                       |
      v                       v
[PDP/PEP checks]          [tool output]
      |
      v
[stop / retry / next step]
```

---

## Execution patterns: how risk shifts by orchestration pattern

The core differentiator is **who decides the next tool/step** and **how many times** that decision happens.

<div class="c-table" role="region" aria-label="Execution patterns by orchestration" tabindex="0"><table><thead><tr><th>Pattern</th><th>Orchestration shape</th><th>Who decides the next tool/step?</th><th>Dominant risk amplifiers</th><th>Primary enforcement points</th></tr></thead><tbody>
<tr><td>Single-shot tool use</td><td>One/few tool calls, minimal iteration</td><td>Mostly application code + one model decision</td><td>Unsafe tool args; weak write-path enforcement; mishandled tool output</td><td>Tool allowlists, strict tool schemas, output handling, server-side write-path enforcement</td></tr>
<tr><td>Workflow (predetermined)</td><td>Fixed graph / code path</td><td>Graph logic</td><td>Reduced dynamism, but still exposed via tool I/O + data channels</td><td>Graph-level policy checks + tool contracts + write-path enforcement</td></tr>
<tr><td>ReAct-style loop</td><td>Iterative: reason → act → observe → repeat</td><td>Model outputs + loop logic each turn</td><td>Repeated exposure to untrusted observations; step chaining; stop-condition abuse</td><td>Step-level PDP/PEP checks, tool-arg constraints, loop budgets, provenance</td></tr>
<tr><td>Plan-and-execute</td><td>Plan first; execute step-by-step; may re-plan</td><td>Planner output + executor loop</td><td>Plan becomes an attack target; execution drift; plan/tool coupling</td><td>Plan validator + per-step PDP/PEP + write-path enforcement + budgets</td></tr>
</tbody></table></div>

Notes:
- ReAct is a published research pattern (paper in References).
- Workflow vs agent distinctions are defined by Anthropic and LangGraph (References).

---

## Minimal threat model

**Attacker capability:** can fully/partially control at least one untrusted artifact that the system ingests (prompt, retrieved page, ticket/file/email, or tool output).  
**Defender failure mode:** the system treats parts of that artifact as control-plane authority (routing constraints, tool permissions, approvals, tool arguments, stop conditions).  
**Impact classes:** (a) steering (wrong plan/tool), (b) exfiltration (retrieve/export), (c) unauthorized write (state change), often with (d) audit failure (missing provenance/correlation).

---

## Why risk scales in an orchestration loop (mechanisms)

### 1) Indirect prompt injection becomes an execution channel (LLM01)

Indirect injection is instruction-like text embedded in external sources (web/files/tickets). In a loop, the same injected directive can influence multiple steps unless instruction/data separation and PDP/PEP enforcement are real (not “prompt-only”).

### 2) Plans and intermediate artifacts become attack targets

Plans, step lists, tool observations, and “notes so far” become decision inputs. If attackers can influence those artifacts (via retrieval or tool output), they can steer execution toward exfiltration or unsafe writes.

### 3) Retry amplification multiplies exposure

Retries improve reliability but increase the number of opportunities for compromised observations/summaries to influence downstream decisions.

### 4) Stop-condition and budget manipulation creates “eventual side effects”

Stop/retry logic is control-plane authority. Without enforced stop/budget rules, the loop tends to “search” until it eventually crosses a side-effect boundary.

### 5) Unbounded consumption becomes a security risk (LLM10)

In looped systems, budgets (steps/time/cost/retries) are a first-class security control for availability and cost containment.

---

## Controls that reduce orchestration-loop risk (enforcement points)

### 1) Instruction/data separation (treat retrieval + tool outputs as untrusted)

Enforce:
- Retrieved/tool text is **data**, not policy.
- Tool selection and write approvals cannot be derived from untrusted text.
- Actionable directives must use structured, allowlisted formats.

### 2) Capability-scoped tools (least privilege) (LLM06)

- Separate read vs write capabilities.
- Bind scopes to explicit resources/tenants.
- Deny-by-default exposure of high-impact tools.

### 3) Server-side write-path enforcement (PDP → PEP per call)

Treat any external side effect as privileged. Authorize and enforce server-side **per write call**.

### 4) Strict tool schemas + validation

Validate tool selection + arguments in code (schema + semantic constraints). Do not treat model output as intrinsically valid authority.

### 5) Tool selection constraints (reduce action space)

Constrain selectable tools per run/intent category (deny-by-default) where the platform supports it.

### 6) Loop budgets + enforced stop conditions (LLM10)

Hard limits the loop cannot bypass:
- max steps / max tool calls
- time budget / retry caps per tool
- cost ceilings
- escalation rules after repeated failures (stop / approval / read-only)

### 7) End-to-end provenance and auditability

Log enough to reconstruct “what influenced what”:
- retrieved artifacts (stable references/hashes)
- plan + step history
- tool I/O (bounded/redacted)
- approvals/denials and PDP/PEP decisions
- final output

---

## Implementation sketch (PDP/PEP + budgets)

Illustrative pseudocode showing enforcement points that must not depend on model compliance:

```text
ingress(request):
  principal = authenticate_and_bind(request)        # tenant/user/session binding
  mode      = decide_mode(principal, request)       # READ_ONLY / WRITE_CAPABLE

  retrieved = retrieve(request)
  retrieved = label_and_delimit(retrieved, trust="UNTRUSTED_DATA")

  plan = model_propose_plan(request, retrieved)     # untrusted intermediate artifact

  decision = pdp_validate_plan(plan, principal, mode)
  assert decision.allow

  budgets = { max_steps:N, max_tool_calls:M, max_retries_per_tool:R, timeout_ms:T }
  state   = init_state(request, retrieved, decision)

  while budgets_ok(budgets, state):
    action = model_propose_next_action(state)       # untrusted proposal

    assert pep_validate_action(action, principal, mode, state)

    if action.type == STOP:
      return finalize(state)

    assert action.type == TOOL_CALL
    assert validate_tool_call(action, principal, state)  # schema + semantics

    if action.is_write:
      assert server_side_write_gate(action, principal, state)

    result = execute_tool(action)
    record_provenance(action, result)
    state = update_state(state, result)
```

---

## What to test (security test cases)

<div class="c-table" role="region" aria-label="Security test cases" tabindex="0">
  <table>
    <thead>
      <tr>
        <th>Test</th>
        <th>Goal</th>
        <th>Expected result</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Retrieval injection test</td>
        <td>Retrieved content cannot change tool allowlists, scopes, or authorization decisions</td>
        <td>Tool selection remains constrained; policy gates reject elevation</td>
      </tr>
      <tr>
        <td>Tool-arg validation test</td>
        <td>Invalid or policy-violating arguments are rejected</td>
        <td>Fail closed; violations logged with provenance</td>
      </tr>
      <tr>
        <td>Write-gate test</td>
        <td>Any write-capable call requires server-side authorization per call</td>
        <td>Writes blocked without explicit authorization decision</td>
      </tr>
      <tr>
        <td>Plan validation test</td>
        <td>Planner cannot introduce tools/targets outside policy/tenant binding</td>
        <td>Plan rejected or constrained by policy, not executed</td>
      </tr>
      <tr>
        <td>Budget/stop test</td>
        <td>Loops terminate under step/time/cost/retry ceilings</td>
        <td>Loop stops deterministically; escalation rules trigger</td>
      </tr>
    </tbody>
  </table>
</div>

---

## Suggested reading
- [The Attack Surface Starts Before Agents — The LLM Boundary]({{ '/articles/agent-security/llm-boundary-first-touch/' | relative_url }})
- [How Agentic Control-Plane Failures Actually Happen]({{ '/articles/agent-security/control-plane-failures/' | relative_url }})
- [Agentic Systems: 8 Trust-Boundary Audit Checkpoints]({{ '/articles/agent-security/trust-boundary-checkpoints/' | relative_url }})
- [Request assembly threat model: reading the diagram]({{ '/articles/agent-security/request-assembly-threat-model/' | relative_url }})
- [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})

## References
- [OWASP GenAI — LLM01:2025 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
- [OWASP GenAI — LLM06:2025 Excessive Agency](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/)
- [OWASP GenAI — LLM10:2025 Unbounded Consumption](https://genai.owasp.org/llmrisk/llm102025-unbounded-consumption/)
- [OWASP Cheat Sheet — LLM Prompt Injection Prevention](https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html)
- [OWASP Cheat Sheet — AI Agent Security](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html)
- [NIST SP 800-207 — Zero Trust Architecture (DOI)](https://doi.org/10.6028/NIST.SP.800-207)
- [NIST SP 800-207 — Zero Trust Architecture (PDF)](https://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.SP.800-207.pdf)
- [NIST AI 600-1 — AI RMF: Generative AI Profile (DOI)](https://doi.org/10.6028/NIST.AI.600-1)
- [NIST AI 600-1 — AI RMF: Generative AI Profile (PDF)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf)
- [OpenAI — Safety in building agents](https://developers.openai.com/api/docs/guides/agent-builder-safety/)
- [OpenAI — Function calling](https://developers.openai.com/api/docs/guides/function-calling/)
- [OpenAI — Structured outputs](https://developers.openai.com/api/docs/guides/structured-outputs/)
- [Anthropic — Building Effective Agents](https://www.anthropic.com/research/building-effective-agents)
- [LangGraph — Workflows and agents](https://docs.langchain.com/oss/python/langgraph/workflows-agents)
- [ReAct — Yao et al. (arXiv:2210.03629)](https://arxiv.org/abs/2210.03629)
