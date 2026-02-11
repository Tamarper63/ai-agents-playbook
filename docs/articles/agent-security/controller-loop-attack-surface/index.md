---
title: The Attack Surface Isn’t the LLM — It’s the Controller Loop
permalink: /articles/agent-security/controller-loop-attack-surface/
summary: Why planner/controller loops amplify risk in tool-using systems, and which controls actually reduce it.
---

## Thesis
In tool-using systems, the primary attack surface is not the language model itself. The risk scales in the **controller loop** (the orchestration layer that plans, calls tools, evaluates outcomes, retries, and decides when to stop).

## Two execution shapes (single-shot vs. loop)
Many deployments have a “tool-use” capability. The security shift happens when tool-use is wrapped in a **multi-step control loop**.

### Single-shot tool use (one tool call, minimal iteration)
Typical shape:

- context (including memory/state)
- model inference
- optional tool call
- model inference → final output

### Agentic tool use (planner/controller loop with retries)
Typical shape:

- model inference (propose intent/plan)
- **planner/controller** (select next step)
- executor/tools (perform step)
- evaluate result
- **stop?** if not, retry/iterate

**Key point:** as soon as you introduce a loop, you introduce more *decision points*, more *tool invocations*, and more *opportunities for steering*.

## Why risk scales in the loop
### 1) Indirect prompt injection gains leverage
When untrusted content is retrieved (web pages, files, tickets, emails), it can function as an **instruction channel** unless you enforce instruction/data separation. In a loop, that “instruction” can be acted on repeatedly across steps.

### 2) Plan manipulation becomes a target
If an attacker can influence the plan (explicitly or via tool outputs), they can redirect execution toward unsafe actions (e.g., exfiltration, privilege abuse, unintended writes).

### 3) Retry amplification (“recursive tool abuse”)
Retries are a safety feature for robustness—but they can amplify a single bad step. One compromised tool output can get re-used or reinforced across iterations.

### 4) Stop-condition hijack
The stop condition is a control point. If the system can be made to “continue until done” without strict gating, an attacker can push the loop to keep acting until a side effect occurs.

## Practical failure pattern: untrusted content → instruction channel → chained actions
A common pattern is:

1) system retrieves untrusted content (web/file)
2) content includes instruction-like text
3) controller loop treats it as actionable
4) loop chains actions across tools (especially external writes)

This is a form of **indirect prompt injection**.

## Controls that matter (not “better prompting”)
### 1) Scoped capabilities (least privilege, short-lived)
Use **least privilege** per tool/action. Prefer **short-lived, scoped authorization** (capability-style grants) over broad, long-lived permissions.

### 2) Server-side gates for external writes
Treat external side effects as high-risk operations:
- send/post/update/upload
- permission changes
- data exports

Enforce server-side authorization checks and policy gates for each write.

### 3) Treat retrieved content as untrusted by default
Implement **instruction/data separation**:
- retrieved content is data, not policy
- no tool-call decisions should be made solely from untrusted text
- require explicit allowlists or structured “safe” schemas for actionable directives

### 4) Full audit trail (end-to-end provenance)
Log (and retain) enough to reconstruct what happened:
- retrieved chunks (or stable references/hashes)
- plan/steps
- tool I/O
- approvals/denials
- final output

Without this, incident response and debugging are guesswork.

## Minimal checklist
- [ ] Tool permissions are scoped per action (least privilege)
- [ ] External writes require explicit server-side gates
- [ ] Retrieved content is treated as untrusted data
- [ ] Controller-loop steps + tool I/O are fully auditable
