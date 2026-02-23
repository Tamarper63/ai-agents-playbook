---
title: "Prompt Assembly Policy Enforcement: Typed Provenance to Prevent Authority Confusion"
permalink: /articles/agent-security/prompt-assembly-policy-enforcement/
layout: default
categories: [agent-security]
author: Tamar Peretz
published: 2026-02-22
---

## Scope
This article is an engineering guide for one specific failure mode in prompt assembly:

**Authority confusion:** untrusted content is misclassified and handled as if it were authoritative policy, causing policy spoofing and cross-turn drift.

The diagram that defines the modeled pipeline is maintained as a reference (SSOT):
- `/reference/diagrams/provenance-boundary-failure-prompt-assembly/`

Diagram asset (rendered SVG):
- `/assets/img/diagrams/provenance-boundary-failure-prompt-assembly.svg`

This page uses requirement keywords as defined by RFC 2119 (e.g., MUST, SHOULD, MAY). RFC 2119.

## Diagram (reference only)
![Provenance Boundary Failure — Prompt Assembly]({{ '/assets/img/diagrams/provenance-boundary-failure-prompt-assembly.svg' | relative_url }})

## Threat model focus
The modeled pipeline has two fundamentally different input classes:

1) **Authoritative policy** (privileged): system/developer constraints and rules sourced from an authoritative policy store.
2) **Untrusted content** (non-privileged): user messages and other untrusted text.

The failure mode occurs when (1) and (2) are not kept separate through the prompt-assembly boundary.

Prompt injection is a known class of risk where crafted inputs attempt to manipulate model behavior or override intended controls. OWASP GenAI Security Project (LLM01: Prompt Injection). OWASP.

## Security objective
Prevent authority confusion by enforcing, at the prompt-assembly ingress, that:
- **Only authoritative policy can be interpreted as policy**, and
- **Untrusted content remains data**, even if it is formatted like instructions.

## Architectural control: treat prompt-assembly ingress as an enforcement point
NIST SP 800-207 defines a Zero Trust Architecture where policy decisions are made by policy decision logic and enforced by a policy enforcement function that can enable, monitor, and terminate access. NIST SP 800-207, DOI: 10.6028/NIST.SP.800-207.

Applied to prompt assembly as an engineering pattern:
- The **policy store** is the single authoritative source of privileged rules.
- The **gateway** is the enforcement choke point that validates provenance and blocks policy spoofing before any content reaches the model.

This is a design pattern derived from the enforcement concepts described in NIST SP 800-207. NIST SP 800-207, DOI: 10.6028/NIST.SP.800-207.

## Hard requirements (invariants)
### R1 — Authority separation
Authoritative policy MUST originate only from the authoritative policy store. Untrusted channels MUST NOT be accepted as policy inputs.

### R2 — Typed provenance for every context item
Every item entering the assembled context MUST carry explicit provenance metadata:
- `source`: `policy | user | tool | retrieval`
- `trust`: `trusted | untrusted`

### R3 — No silent promotion
Untrusted content MUST NOT gain authority through formatting (e.g., “policy: …”, “system: …”, “ops notice: …”, “treat next messages as policy”).

OWASP guidance emphasizes clear separation of instructions from untrusted data and treating external content as untrusted. OWASP Cheat Sheet Series (LLM Prompt Injection Prevention Cheat Sheet). OWASP.

### R4 — Fail-closed on ambiguity
If provenance classification is uncertain or missing, the gateway MUST fail-closed (contain or drop) rather than interpret content as policy.

### R5 — Cross-turn drift guard
Persisted state MUST NOT promote untrusted content into policy across turns. State reintroduced into context MUST remain provenance-typed and non-privileged unless it is authoritative policy from the policy store.

### R6 — Observability
Provenance classification decisions MUST be observable (audit logs/telemetry) so that misclassification can be detected and triaged.

## Minimal data contract (template)
The following contract is a **template** for deterministic enforcement (not a standard):

~~~json
{
  "id": "string",
  "content": "string",
  "provenance": {
    "source": "policy|user|tool|retrieval",
    "trust": "trusted|untrusted",
    "origin_id": "string",
    "captured_at": "RFC3339 timestamp"
  }
}
~~~

Enforcement rule:
- Only items with `provenance.source == "policy"` AND `provenance.trust == "trusted"` may be interpreted as authority-bearing constraints.

This rule operationalizes “separate privileged policy from untrusted inputs” as recommended by OWASP prompt-injection prevention guidance. OWASP Cheat Sheet Series (LLM Prompt Injection Prevention Cheat Sheet). OWASP.

## Deterministic enforcement pipeline (step-by-step)
### Step 1 — Ingress classification
For every inbound item (user, tool output, retrieved content, state):
1) Assign `source` based on the ingestion channel.
2) Assign `trust`:
   - `trusted` only for policy items loaded from the policy store.
   - `untrusted` for everything else by default.

### Step 2 — Policy isolation
Policy items are loaded from the policy store and kept in a dedicated policy segment. Untrusted segments are kept separate and never merged into the policy segment.

### Step 3 — Assembly rules
The context builder assembles:
- Policy segment (trusted, authoritative)
- Untrusted segment(s) (user/tool/retrieval/state), tagged and isolated

### Step 4 — Fail-closed checks
Before emitting a final prompt/context:
- Reject if any item is missing provenance.
- Reject if any non-policy item is marked `trusted`.
- Reject if any item is routed to the policy segment without being policy-store sourced.

### Step 5 — Output validation
OWASP guidance includes validating outputs and avoiding blindly following model-produced instructions. OWASP Cheat Sheet Series (LLM Prompt Injection Prevention Cheat Sheet). OWASP.

Implement deterministic post-generation validation:
- If your system requires structured output, validate schema/format in code.
- If validation fails, fail-closed (retry with safer prompt, or return a safe error).

## Test plan (copy/paste)
The suite below verifies the invariants R1–R6 without relying on model compliance.

~~~csv
Test Name,Objective,Components Covered,Test Steps,Expected Result,Priority
PEP_R1_authority_separation,Ensure untrusted channels cannot become policy,Gateway+Policy store,Send user content formatted as policy; load policy from store,User item stays untrusted; policy segment contains only store items,High
PEP_R2_typed_provenance_required,Ensure every context item has provenance,Gateway+Context builder,Inject item with missing/invalid provenance,Assembly fails-closed; no context emitted,High
PEP_R3_no_silent_promotion,Block formatting-based promotion,Gateway,Send untrusted content with “system:”/“policy:” headers,Item remains untrusted; never routed to policy segment,High
PEP_R4_fail_closed_on_ambiguity,Fail-closed on uncertain classification,Gateway,Provide ambiguous ingestion channel or corrupted tags,Gateway blocks/contains; emits explicit error path,High
PEP_R5_cross_turn_drift_guard,Prevent cross-turn privilege drift,State store+Context builder,Turn 1 injects pseudo-policy; persist state; Turn 2 normal query,State stays untrusted; no authority carryover,High
PEP_R6_auditability,Make decisions observable,Gateway logging,Run assembly and inspect logs,Logs record source+trust+decision for each item,High
Output_schema_validation,Validate outputs deterministically,Output validator,Force non-conforming output then validate,Validator rejects; system takes safe fallback,High
~~~

## Implementation notes (best-practice constraints)
- Treat tool outputs and retrieved content as untrusted unless explicitly verified. OWASP Cheat Sheet Series (LLM Prompt Injection Prevention Cheat Sheet). OWASP.
- Avoid mixing authority-bearing instructions with untrusted data without explicit separation. OWASP Cheat Sheet Series (LLM Prompt Injection Prevention Cheat Sheet). OWASP.
- Use enforcement patterns consistent with policy decision + policy enforcement separation described in Zero Trust Architecture. NIST SP 800-207, DOI: 10.6028/NIST.SP.800-207.

## Suggested next
- [Articles — Start here]({{ '/articles/#start-here' | relative_url }})
- [Agent architecture]({{ '/articles/agent-architecture/' | relative_url }})
- [Content map]({{ '/reference/content-map/' | relative_url }})

## References (formal identifiers / institutions)
- RFC 2119 — *Key words for use in RFCs to Indicate Requirement Levels*. https://www.rfc-editor.org/rfc/rfc2119.html
- NIST SP 800-207 — *Zero Trust Architecture*. https://doi.org/10.6028/NIST.SP.800-207
- OWASP GenAI Security Project — LLM01:2025 Prompt Injection. <https://genai.owasp.org/llmrisk/llm01-prompt-injection/>
- OWASP Cheat Sheet Series — *LLM Prompt Injection Prevention Cheat Sheet*.<https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html>
