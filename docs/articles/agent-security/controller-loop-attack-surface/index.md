---
title: Tool-Using Systems The Attack Surface Shifts to the Controller Loop
permalink: /articles/agent-security/controller-loop-attack-surface/
summary: How multi-step controller loops change the threat model in tool-using systems, and where to enforce separation, authorization, validation, and budgets to reduce prompt injection, tool misuse, unsafe writes, and unbounded consumption.
author: Tamar Peretz
published: 2026-02-22
---

## Why controller loops change the threat model
In many tool-using deployments, a large share of the practical attack surface sits in the **controller loop**: orchestration logic that selects steps, invokes tools, evaluates outcomes, retries, and decides when to stop.

This matters because a controller loop adds:
- more **decision points** (plan selection, tool selection, “try again?” decisions),
- more **tool invocations** (and therefore more opportunities for misuse),
- more **state transitions** (memory, scratchpads, “notes so far”, intermediate artifacts),
- and more opportunities to cross into **write paths** (external side effects).

OWASP’s GenAI Top 10 includes prompt injection (LLM01), excessive agency (LLM06), and unbounded consumption (LLM10). This post uses those categories to structure controller-loop risks and controls.  
(References: OWASP GenAI LLM01/LLM06/LLM10 at the end.)

---

## Core terms (as used here)
- **Controller loop:** orchestration logic that sequences steps (plan → act → observe → decide), including retries and stop conditions.
- **Workflow:** LLM + tools orchestrated through **predefined code paths** (fixed order / graph).  
- **Agent:** LLM dynamically **directs its own process and tool usage** at runtime (within whatever bounds you enforce).  
- **Policy Decision Point (PDP):** the component that evaluates a proposed plan/action against policy and returns allow/deny.
- **Policy Enforcement Point (PEP):** the component that blocks or allows execution based on policy decisions (e.g., checks before tool calls / writes).
- **Instruction/data separation:** controls that prevent untrusted content from being interpreted as policy, permissions, routing constraints, approvals, or tool arguments.
- **Write path:** any operation that changes external state (create/update/delete, invites/resets, configuration changes, permission changes, exports).
- **Loop budgets:** hard limits on steps/time/cost/retries that the controller loop cannot exceed.

(Workflows vs agents phrasing is aligned with Anthropic’s definitions and LangGraph’s documentation; see References.)


---

## Architecture: where the loop lives
A practical way to reason about “what changed” is to separate **data plane** vs **control plane** (ZTA-aligned terms used here by extension):

- **Data plane:** user input, retrieved chunks, tool observations (anything the model reads).
- **Control plane:** orchestration + policy decision/enforcement logic that decides what happens next (routing, tool selection, stop conditions, write-path enforcement).

When you introduce a controller loop, the control plane becomes a dominant trust boundary.

### Single-shot tool use (minimal control plane)
Typical shape:

```
[request + context] -> [model] -> (optional tool call) -> [model] -> [final output]
```

### Controller loop (expanded control plane)
Typical shape:

```
[request + context]
      |
      v
[controller loop] ---> [tool router] ---> [tools/connectors]
      |                     |
      v                     v
[policy checks]         [tool output]
      |
      v
[stop / retry / next step]
```

---

## Execution patterns: where risk shifts by orchestration pattern
The core differentiator is **who decides the next tool/step** and **how many times** that decision happens.

| Pattern | Orchestration shape | Who decides the next tool/step? | Dominant risk amplifiers | Primary enforcement points |
|---|---|---|---|---|
| Single-shot tool use | One/few tool calls, minimal iteration | Mostly application code + one model decision | Unsafe tool args; weak write-path enforcement; mishandled tool output | Tool allowlists, strict tool schemas, output handling, server-side write-path enforcement |
| Workflow (predetermined) | Fixed graph / code path | Graph logic | Reduced dynamism, but still exposed via tool I/O + data channels | Graph-level policy checks + tool contracts + write-path enforcement |
| ReAct-style loop | Iterative: reason → act → observe → repeat | Model outputs + loop logic each turn | Repeated exposure to untrusted observations; step chaining; stop-condition abuse | Step-level policy enforcement checks, tool-arg constraints, loop budgets, full provenance trace |
| Plan-and-execute | Plan first; execute step-by-step; may re-plan | Planner output + executor loop | Plan becomes an attack target; execution drift across steps; plan/tool coupling | Plan validator + per-step policy enforcement checks + write-path enforcement + budgets |


Notes:
- ReAct is a published research pattern (paper in References).
- Workflow vs agent distinctions are defined explicitly by Anthropic and LangGraph (References).

---

## Threat model (minimal)
**Attacker capability:** controls or partially controls at least one untrusted artifact that the system will ingest (direct prompt, retrieved page, ticket/file/email, or tool output).  
**Defender failure mode:** the system treats parts of that artifact as control-plane authority (routing constraints, tool permissions, action approvals, tool arguments, stop conditions).  
**Impact classes:** (a) **steering** (wrong plan/tool), (b) **exfiltration** (retrieve/export), (c) **unauthorized write** (state change), often with (d) **audit failure** (missing provenance/correlation).

OWASP GenAI LLM06 (“Excessive Agency”) is a useful reference category for classifying failures where autonomy and permissions exceed what is justified. Several failure modes below align with that category. (Reference: OWASP GenAI LLM06.)

---

## Why risk scales in the controller loop
### 1) Indirect prompt injection becomes an execution channel
OWASP describes **indirect prompt injection** as instructions embedded in external sources (e.g., websites/files) that alter behavior when ingested. In a controller loop, the same injected instructions can influence multiple steps unless instruction/data separation and policy enforcement are real (not “prompt-only”). (Reference: OWASP GenAI LLM01; OWASP Prompt Injection Prevention cheat sheet.)

### 2) Plans and intermediate artifacts become first-class attack targets
In looped systems, intermediate artifacts (plans, step lists, tool observations, “notes so far”) become decision inputs. If an attacker can influence these artifacts (via retrieval or tool output manipulation), they can steer execution toward exfiltration or unsafe writes.

### 3) Retry amplification (robustness → repeated exposure)
Retries increase reliability, but they also increase the number of chances for a compromised observation to influence downstream decisions—especially if the loop reuses the same untrusted artifact or summary.

### 4) Stop-condition and budget hijack
Stop conditions are control points. If the loop is allowed to “continue until done” without strict enforcement and budgets, you increase the chance that the system eventually crosses into a side effect.
### 5) Unbounded consumption (cost / availability)
OWASP LLM10 frames **unbounded consumption** as a security risk: unconstrained usage can drive excessive resource consumption. In looped systems, budgets (steps/time/cost/retries) can be used as controls to mitigate that risk. (Reference: OWASP GenAI LLM10.)

---

## Concrete examples (for clarity)

### Example A — Indirect injection via retrieved ticket → unsafe tool selection
**Vulnerable flow**
1) Retrieve a support ticket (untrusted).
2) Ticket text includes instruction-like content and is treated as authoritative.
3) The controller loop promotes it into “next steps”.
4) The tool router selects a privileged tool or a write-capable action.

**Enforcement that breaks the chain**
- Retrieval results are always labeled and delimited as **UNTRUSTED DATA** (instruction/data separation).
- The router requires **intent classification + allowlist** before any privileged tool is selectable.
- Write-capable tool calls require server-side authorization **per call**.

### Example B — Plan manipulation via tool output → execution drift
**Vulnerable flow**
1) Planner generates a plan from mixed trusted + untrusted inputs.
2) A tool output suggests extra steps (“also update permissions / export data”).
3) The loop executes the augmented plan without validation.

**Enforcement that breaks the chain**
- Treat **plans as untrusted intermediate artifacts**.
- Validate every step against:
  - allowed action types
  - allowed tools
  - allowed targets/resources (tenant/resource binding)
  - write-gate requirements

### Example C — Stop-condition/budget hijack → eventual side effect
**Vulnerable flow**
- Loop keeps iterating on partial failures without budgets (“keep trying”).
- Eventually a write-capable path is reached (or spend explodes).

**Enforcement that breaks the chain**
- Enforce hard budgets: max steps, max tool calls, timeouts, cost ceilings, retry caps per tool.
- Escalate after repeated failures: stop, require approval, or switch to read-only mode.

---

## Controls that reduce controller-loop risk (enforcement points)
The goal is to move critical decisions out of “model compliance” and into enforceable checks.

### 1) Instruction/data separation (treat retrieval + tool outputs as untrusted)
Enforce:
- Retrieved content is **data**, not policy.
- Tool selection and write approvals cannot be derived solely from untrusted text.
- Actionable directives must use structured, allowlisted formats.

(Reference: OWASP Prompt Injection Prevention cheat sheet; OWASP GenAI LLM01.)

### 2) Capability-scoped tools (least privilege)
Scope tools by capability and target:
- Separate read vs write capabilities.
- Bind scopes to explicit resources/tenants.
- Deny-by-default exposure of high-impact tools.

(Reference: OWASP GenAI LLM06; OWASP AI Agent Security cheat sheet.)

### 3) Server-side enforcement for write paths (authorization + policy per call)
Treat external side effects as privileged operations (send/post/update/upload, permission changes, exports).  
Enforce authorization and policy checks server-side for every write call.

(Reference: OWASP GenAI LLM06; OWASP AI Agent Security cheat sheet.)

### 4) Strict tool schemas + validation (reduce free-form authority)
If you use tool calling, validate tool inputs in code. OpenAI’s docs explicitly warn that models can generate invalid or non-existent arguments and that callers must validate tool-call arguments.  
(References: OpenAI Function calling guide; OpenAI Chat API reference.)

### 5) Tool selection constraints (reduce the action space)
Where the platform supports it, constrain which tools are selectable for a run or intent category (deny-by-default). OpenAI documents an “allowed tools” mechanism for constraining tool selection.  
(References: OpenAI Function calling guide; OpenAI Chat API reference.)

### 6) Loop budgets and stop conditions (security budgets)
Add hard limits the loop cannot bypass:
- max steps / max tool calls
- time budget
- cost budget
- retry caps per tool
- escalation rules after repeated failures

(Reference: OWASP GenAI LLM10.)

### 7) End-to-end provenance and auditability
Log enough to reconstruct “what influenced what”:
- retrieved artifacts (stable references/hashes)
- plan + step history
- tool I/O (bounded/redacted)
- approvals/denials and policy decisions
- final output

(Reference: OWASP AI Agent Security cheat sheet; OWASP Securing Agentic Applications Guide 1.0.)

---

## Implementation sketch (policy + router + budgets)
Illustrative pseudocode showing enforcement points that should not depend on model compliance:

ingress(request):
  principal = authenticate_and_bind(request)      # tenant/user/session binding
  mode      = decide_mode(principal, request)     # READ_ONLY / WRITE_CAPABLE

  retrieved = retrieve(request)
  retrieved = label_and_delimit(retrieved, trust="UNTRUSTED_DATA")

  # Planner output is an untrusted intermediate artifact.
  plan = model_propose_plan(request, retrieved)

  # Policy Decision Point (PDP): deny-by-default validation.
  decision = pdp_validate_plan(plan, principal, mode)
  assert decision.allow

  step_budget = {
    max_steps: N,
    max_tool_calls: M,
    max_retries_per_tool: R,
    timeout_ms: T,
  }

  state = init_state(request, retrieved, decision)

  while budgets_ok(step_budget, state):
    action = model_propose_next_action(state)

    # Policy Enforcement Point (PEP): enforce before any side effect.
    assert pep_validate_action(action, principal, mode, state)

    if action.type == STOP:
      return finalize(state)

    if action.type != TOOL_CALL:
      raise PolicyViolation("unexpected action type")

    # 1) Validate tool selection + arguments (schema + semantic constraints).
    assert validate_tool_call(action, principal, state)

    # 2) Server-side write-path enforcement for any external state change.
    if action.is_write:
      assert server_side_write_gate(action, principal, state)

    result = execute_tool(action)
    record_provenance(action, result)              # hashes/timestamps/correlation ids
    state = update_state(state, result)

---

## What to test (security test cases)
| Test | Goal | Expected result |
|---|---|---|
| Retrieval injection test | Retrieved content cannot change tool allowlists, scopes, or authorization decisions | Tool selection remains constrained; policy gates reject elevation |
| Tool-arg validation test | Invalid or policy-violating arguments are rejected | Calls fail closed; violations are logged with provenance |
| Write-gate test | Any write-capable call requires server-side authorization per call | Writes are blocked without explicit authorization decision |
| Plan validation test | Planner cannot introduce tools/targets outside policy/tenant binding | Plan rejected or rewritten by policy, not executed |
| Budget/stop test | Loops terminate under step/time/cost/retry ceilings | Loop stops deterministically; escalation rules trigger |

---

## Suggested next
- [Articles — Start here]({{ '/articles/#start-here' | relative_url }})
- [Agent architecture]({{ '/articles/agent-architecture/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})

## References
- OWASP GenAI — LLM01:2025 Prompt Injection: https://genai.owasp.org/llmrisk/llm01-prompt-injection/
- OWASP GenAI — LLM06:2025 Excessive Agency: https://genai.owasp.org/llmrisk/llm062025-excessive-agency/
- OWASP GenAI — LLM10:2025 Unbounded Consumption: https://genai.owasp.org/llmrisk/llm102025-unbounded-consumption/
- OWASP Cheat Sheet — LLM Prompt Injection Prevention: https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html
- OWASP Cheat Sheet — AI Agent Security: https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html
- OWASP GenAI — Securing Agentic Applications Guide 1.0: https://genai.owasp.org/resource/securing-agentic-applications-guide-1-0/
- NIST SP 800-207 — Zero Trust Architecture: https://doi.org/10.6028/NIST.SP.800-207
- NIST AI 600-1 — Generative AI Profile: https://doi.org/10.6028/NIST.AI.600-1
- OpenAI — Safety in building agents: https://developers.openai.com/api/docs/guides/agent-builder-safety/
- OpenAI — Function calling: https://developers.openai.com/api/docs/guides/function-calling/
- OpenAI — Structured Outputs: https://developers.openai.com/api/docs/guides/structured-outputs/
- Anthropic — Building Effective Agents (workflows vs agents): https://www.anthropic.com/engineering/building-effective-agents
- LangGraph — Workflows and agents: https://docs.langchain.com/oss/python/langgraph/workflows-agents
- ReAct: Synergizing Reasoning and Acting in Language Models (arXiv:2210.03629): https://arxiv.org/abs/2210.03629