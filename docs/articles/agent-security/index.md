---
title: Agent security
permalink: /articles/agent-security/
---

This section collects engineering writeups on security properties of **tool-using LLM systems (“agents”)**: trust boundaries, authorization semantics, orchestration controls, and monitoring/gating design.

## Start here (pick the job)

| If you need… | Start with | Then |
|---|---|---|
| A concrete audit checklist for agent pipelines (ingress → retrieval → tools → write paths → egress) | [Agentic Systems: 8 Trust-Boundary Audit Checkpoints]({{ '/articles/agent-security/trust-boundary-checkpoints/' | relative_url }}) | [Tool-Using Systems: The Attack Surface Shifts to the Controller Loop]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }}) |
| Failure patterns for controllers/routers/policy gates (design + review) | [Control-Plane Failure Patterns in Agentic Tool-Using Systems]({{ '/articles/agent-security/control-plane-failures/' | relative_url }}) | [Agentic Systems: 8 Trust-Boundary Audit Checkpoints]({{ '/articles/agent-security/trust-boundary-checkpoints/' | relative_url }}) |
| A public-safe incident/report template with explicit verification limits | [Provenance boundary failure report (client-captured artifacts)]({{ '/articles/agent-security/provenance-boundary-report/' | relative_url }}) | (Use the section contracts below for evidence labeling + disclosure hygiene) |
| Manipulation of the decision pipeline (beyond “prompt tricks”) | [Social engineering in AI systems: attacking the decision pipeline (not just people)]({{ '/articles/agent-security/social-engineering-ai-decision-pipeline/' | relative_url }}) | [Agentic Systems: 8 Trust-Boundary Audit Checkpoints]({{ '/articles/agent-security/trust-boundary-checkpoints/' | relative_url }}) |

## Scope

- Focus: security properties of LLM-driven applications and agents (controllers, routers, policy gateways, session/memory scope, tool routing, write-path gating).
- Output style: engineering-oriented; emphasis on **testable claims**, explicit system boundaries, and mitigation guidance.
- Public-safe disclosure: posts may omit PoC strings and evidence artifacts; maintainers can request private evidence under coordinated disclosure.

### Non-goals (out of scope for this section)
- General application security guidance that is not specific to LLM-driven control planes.
- Model-training security or claims about mechanism-level “Theory of Mind” or similar cognitive properties.

## Section operating contracts (how to read + how to reuse)

- **Evidence boundary chooser (facts-only)**: pick “artifacts-only” vs “authoritative sources required” before treating claims as portable.  
  [Choose a facts-only evidence boundary]({{ '/how-to/choose-facts-only-evidence-boundary/' | relative_url }})
- **When web claims appear**: source selection + citation rules are governed by the site policy.  
  [Web Verification & Citations Policy]({{ '/policies/web-verification-and-citations/' | relative_url }})
- **When posts label evidence**: some reports explicitly split statements into:
  - **Observed (client-side)** vs **NOT VERIFIED (server-side)** (vendor confirmation required).  
  (See the provenance report’s “Scope and verification limits”.)  
  [Provenance boundary failure report]({{ '/articles/agent-security/provenance-boundary-report/' | relative_url }})
- **When you want code/architecture validation** (not writing verification): use the engineering gate procedure.  
  [Engineering Quality Gate — Procedure]({{ '/how-to/engineering-quality-gate-procedure/' | relative_url }})

## Topic map (what lives where)

| Theme | What it covers (section-level) | Primary entry points |
|---|---|---|
| Trust boundaries & instruction-vs-data separation | Untrusted artifacts influencing planning/routing/tool invocation/write paths | [Trust-Boundary Audit Checkpoints]({{ '/articles/agent-security/trust-boundary-checkpoints/' | relative_url }}) |
| Controller/router attack surface | Why the “attack surface” shifts to orchestration + enforcement layers | [Attack Surface Shifts to Controller Loop]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }}) |
| Control-plane failures | Policy binding failures, enforcement gaps, and auditability breaks in tool-using systems | [Control-Plane Failure Patterns]({{ '/articles/agent-security/control-plane-failures/' | relative_url }}) |
| Evidence/provenance boundaries | What can/can’t be asserted from client artifacts; public-safe reporting | [Provenance boundary failure report]({{ '/articles/agent-security/provenance-boundary-report/' | relative_url }}) |
| Decision-pipeline manipulation | Social engineering patterns targeting the system’s decision pipeline | [Social engineering: decision pipeline]({{ '/articles/agent-security/social-engineering-ai-decision-pipeline/' | relative_url }}) |

## Articles and reports

- [The Attack Surface Starts Before Agents — The LLM Boundary]({{ '/articles/agent-security/llm-boundary-first-touch/' | relative_url }})
- [Social engineering in AI systems: attacking the decision pipeline (not just people)]({{ '/articles/agent-security/social-engineering-ai-decision-pipeline/' | relative_url }})
- [Tool-Using Systems: The Attack Surface Shifts to the Controller Loop]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})
- [Agentic Systems: 8 Trust-Boundary Audit Checkpoints]({{ '/articles/agent-security/trust-boundary-checkpoints/' | relative_url }})
- [Provenance boundary failure report (client-captured artifacts)]({{ '/articles/agent-security/provenance-boundary-report/' | relative_url }})
- [Control-Plane Failure Patterns in Agentic Tool-Using Systems]({{ '/articles/agent-security/control-plane-failures/' | relative_url }})

## External baselines referenced in this section (for shared terminology)

- OWASP Top 10 for Large Language Model Applications (current edition): https://owasp.org/www-project-top-10-for-large-language-model-applications/  
- OWASP AI Agent Security Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html  
- NIST SP 800-207 (Zero Trust Architecture): https://doi.org/10.6028/NIST.SP.800-207  
- OpenAI guidance for agent builders (prompt-injection framing + mitigations): https://platform.openai.com/docs/guides/agent-builder-safety