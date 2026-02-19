---
title: Agent security
permalink: /articles/agent-security/
---

Engineering writeups on security properties of **tool-using LLM systems (“agents”)**: trust boundaries, authorization semantics, orchestration controls, and monitoring/gating design.

## Start here (pick the job)

| If you need… | Start with | Then |
|---|---|---|
| A concrete audit checklist for agent pipelines (ingress → retrieval → tools → write paths → egress) | {% include page-title-link.html url="/articles/agent-security/trust-boundary-checkpoints/" fallback="8 trust-boundary checkpoints" %} | {% include page-title-link.html url="/articles/agent-security/controller-loop-attack-surface/" fallback="Controller-loop attack surface" %} |
| Failure patterns for controllers/routers/policy gates (design + review) | {% include page-title-link.html url="/articles/agent-security/control-plane-failures/" fallback="Control-plane failure patterns" %} | {% include page-title-link.html url="/articles/agent-security/trust-boundary-checkpoints/" fallback="8 trust-boundary checkpoints" %} |
| A public-safe report template with explicit verification limits | {% include page-title-link.html url="/articles/agent-security/provenance-boundary-report/" fallback="Provenance boundary failure report" %} | {% include page-title-link.html url="/policies/web-verification-and-citations/" fallback="Web Verification & Citations Policy" %} |
| Manipulation of the decision pipeline (beyond “prompt tricks”) | {% include page-title-link.html url="/articles/agent-security/social-engineering-ai-decision-pipeline/" fallback="Social engineering: decision pipeline" %} | {% include page-title-link.html url="/articles/agent-security/trust-boundary-checkpoints/" fallback="8 trust-boundary checkpoints" %} |

## Scope

- Focus: security properties of LLM-driven applications and agents (controllers, routers, policy gateways, session/memory scope, tool routing, write-path gating).
- Output style: engineering-oriented; emphasis on **testable claims**, explicit system boundaries, and mitigation guidance.
- Public-safe disclosure: some writeups omit PoC strings and raw evidence artifacts; request private evidence under coordinated disclosure when required.

### Non-goals (out of scope for this section)

- General application security guidance that is not specific to LLM-driven control planes.
- Model-training security or claims about mechanism-level cognition.

## How to reuse this section (contracts)

- Evidence boundary chooser (facts-only): {% include page-title-link.html url="/how-to/choose-facts-only-evidence-boundary/" fallback="Choose an evidence boundary" %}
- When web claims appear: {% include page-title-link.html url="/policies/web-verification-and-citations/" fallback="Web Verification & Citations Policy" %}
- When a report separates evidence classes: some reports distinguish **client-observed artifacts** from claims that would require **server-side confirmation**; those are labeled explicitly in the report itself.  
  {% include page-title-link.html url="/articles/agent-security/provenance-boundary-report/" fallback="Provenance boundary failure report" %}
- When you want code/architecture validation (not writing verification): {% include page-title-link.html url="/how-to/engineering-quality-gate-procedure/" fallback="Engineering Quality Gate — Procedure" %}

## Pages in this section

- {% include page-title-link.html url="/articles/agent-security/llm-boundary-first-touch/" fallback="The Attack Surface Starts Before Agents — The LLM Boundary" %}
- {% include page-title-link.html url="/articles/agent-security/controller-loop-attack-surface/" fallback="Controller-loop attack surface" %}
- {% include page-title-link.html url="/articles/agent-security/trust-boundary-checkpoints/" fallback="8 trust-boundary checkpoints" %}
- {% include page-title-link.html url="/articles/agent-security/control-plane-failures/" fallback="Control-plane failure patterns" %}
- {% include page-title-link.html url="/articles/agent-security/social-engineering-ai-decision-pipeline/" fallback="Social engineering: decision pipeline" %}
- {% include page-title-link.html url="/articles/agent-security/provenance-boundary-report/" fallback="Provenance boundary failure report" %}

## External baselines (shared terminology)

- [OWASP Top 10 for Large Language Model Applications (v1.1)](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [OWASP AI Agent Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html)
- [NIST SP 800-207: Zero Trust Architecture](https://doi.org/10.6028/NIST.SP.800-207)
- [OpenAI: Safety in building agents](https://platform.openai.com/docs/guides/agent-builder-safety)
