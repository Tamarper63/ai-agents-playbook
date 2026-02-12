---
title: Agent security
permalink: /articles/agent-security/
---

This section collects technical writeups on **agentic security**: policy boundaries, authorization semantics, orchestration controls, and monitoring/gating design.

## Scope

- Focus: security properties of LLM-driven applications and agents (controllers, routers, policy gateways, session/memory scope).
- Output style: engineering-oriented; emphasis on **testable claims**, **explicit verification limits**, and **mitigation guidance**.
- Public-safe disclosure: reports may withhold PoC strings and evidence artifacts; private evidence/repro details can be provided to maintainers under coordinated disclosure.

## What you’ll find here

- Threat models for prompt injection and authority/provenance confusion
- Control-plane vs. chat-plane separation (policy binding, signed state changes, capability tokens)
- Session hygiene and memory scope enforcement
- Monitoring that gates actions (hold/block) vs. monitoring that only alerts

## Articles and reports

- [Social engineering in AI systems: attacking the decision pipeline (not just people)]({{ '/articles/agent-security/social-engineering-ai-decision-pipeline/' | relative_url }})
- [Controller-loop attack surface]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})
- [Exploiting the Trust Boundary in Agentic Systems]({{ '/articles/agent-security/trust-boundary-checkpoints/' | relative_url }})
- [The Attack Surface Isn’t the LLM — It’s the Controller Loop]({{ '/articles/agent-security/controller-loop-attack-surface/' | relative_url }})
- [Provenance boundary failure report (client-captured artifacts)]({{ '/articles/agent-security/provenance-boundary-report/' | relative_url }})
- [How Agentic Control-Plane Failures Actually Happen]({{ '/articles/agent-security/control-plane-failures/' | relative_url }})
